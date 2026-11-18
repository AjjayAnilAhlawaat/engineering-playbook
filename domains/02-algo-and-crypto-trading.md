# Domain Category 02: Algorithmic & Crypto Trading Systems Overlay

*Synthesized from Dual-Agent Consensus: **Quant & Systems Experts** (Marcos López de Prado, Ernest Chan, NautilusTrader, Hummingbot, Freqtrade) + **AI-Native Quant Practitioners** (Fixed-point `Decimal` contracts, Point-in-Time backtest shift audits, `ClOrdID` idempotency, Exchange Cancel-on-Disconnect & Multi-Layer Circuit Breakers).*

Load this domain overlay alongside the active lifecycle playbook (`playbooks/01..06`) whenever building algorithmic trading, market-making, backtesting, or crypto execution systems.

---

## Phase 01: Strategy Hypothesis & Backtest Spec
- **Consensus Standards:**
  - **Structural Hypothesis & Low Degrees of Freedom (Ernest Chan):** Specify the economic/microstructure mechanism (who is on the other side of the trade and why) with minimal free parameters before touching historical data.
  - **Deflated Sharpe Ratio (DSR) & Purged Cross-Validation (López de Prado):** Log every parameter trial ($N$) and evaluate strategies using **Combinatorial Purged Cross-Validation (CPCV)** with embargo windows and the **Deflated Sharpe Ratio** to penalize multiple-testing selection bias.
  - **Point-in-Time (PIT) & Survivorship-Free Data:** Include delisted/bankrupt symbols and enforce strict point-in-time timestamps on OHLCV bars, funding rates, and orderbook snapshots.
  - **Realistic Microstructure Friction:** Require maker/taker fee tiers, funding/borrow costs, network latency, and L2 orderbook queue/impact slippage in the spec.
- **Hard Bans:**
  - **NO** random K-Fold cross-validation on time-series data or fitting scalers/models across the full dataset before train/test splitting.
  - **NO** reporting gross backtest Sharpe/CAGR without deducting fees, slippage, funding, and logging total trial count $N$.

## Phase 02: Execution & Risk Dashboard UI/UX
- **Consensus Standards:**
  - **Read-Only Control Plane Isolation:** Decouple dashboard UI rendering from the hot execution event loop so browser activity never blocks order processing or risk checks.
  - **Full OMS State & Venue Truth Visibility (`tabular-nums`):** Display real-time OMS lifecycle states (`Submitted -> Accepted -> PartiallyFilled -> Filled/Canceled/Rejected`), net vs. gross exposure, liquidation distance, WebSocket sequence health, ACK latency ($p50/p99$), and rate-limit bucket usage (`X-MBX-USED-WEIGHT`).
  - **High-Friction Global Flatten / Kill Switch:** Provide one unmistakable **Cancel-All & Flatten** control gated behind intentional operator confirmation, plus a prominent `PAPER` vs. `LIVE` environment banner.
- **Hard Bans:**
  - **NO** displaying cached balances or orderbook state after a WebSocket sequence gap without a high-contrast `STALE / DEGRADED` lock banner.
  - **NO** collapsing `PendingCancel`, `PartiallyFilled`, or `Rejected` orders into generic `"Active/Inactive"` badges.

## Phase 03: Exchange API, WebSocket, Rate-Limit & Signing Middleware
- **Consensus Standards:**
  - **Deterministic `ClOrdID` Idempotency:** Stamp every outbound order with a deterministic client order ID (`ClOrdID` derived from `strategy_id + signal_id + symbol + side`). On any HTTP 5xx or timeout, **query order status by `ClOrdID` first**—never blindly re-POST.
  - **Weighted Token-Bucket Traffic Shaping & Priority Shedding:** Track exchange rate-limit headers dynamically; above 80% bucket utilization, shed non-critical reads and reserve quota exclusively for order cancellations and risk-reducing trades.
  - **WebSocket Sequence Continuity & Jittered Backoff:** Verify `seq_id == prev_seq_id + 1` on every L2 book update; on any gap, immediately invalidate the local book, halt quoting, and pull a fresh REST snapshot. Use jittered exponential backoff on reconnect.
  - **Least-Privilege Signing Isolation:** Isolate HMAC/Ed25519 signing keys in a dedicated adapter with **withdrawal permissions disabled**; default to `TRADING_ENV=paper` unless both `--mode live` and `CONFIRM_LIVE_TRADING=YES` are set.
- **Hard Bans:**
  - **NO** blind retry loops on order placement timeouts (causes double fills and runaway leverage).
  - **NO** executing live exchange `curl`/CLI mutations directly from agent chat/terminal sessions.
  - **NO** continuing to evaluate signals against a local orderbook after a WebSocket sequence gap.

## Phase 04: Fixed-Point Accounting, Event Kernel & Pre-Trade Risk Backend
- **Consensus Standards:**
  - **Fixed-Point / `Decimal` Arithmetic Only:** Represent all prices, quantities, balances, fees, and PnL using integer fixed-point minor units (satoshis/ticks) or `Decimal` initialized from strings (`Decimal('0.00000001')`), quantized strictly to exchange `tickSize` and `stepSize` filters (`ROUND_DOWN`).
  - **Unified Event-Driven Kernel (NautilusTrader Pattern):** Run identical strategy and OMS state-machine code across historical backtest, paper trading, and live execution by feeding chronological market/timer/execution events through a single deterministic bus.
  - **Synchronous Pre-Trade Risk Gate:** Every order intent must pass a synchronous, non-bypassable risk gate checking: max order notional, max position/leverage, fat-finger price collar (% deviation from mid/BBO), self-trade prevention, and daily drawdown cap.
- **Hard Bans:**
  - **NO** IEEE-754 binary floating-point (`float` / JS `number`) for prices, order sizes, fee calculations, or ledger balances.
  - **NO** same-bar execution without an explicit `.shift(1)` / latency delay between signal generation on bar $T$ and fill on $T+1$.
  - **NO** separate research vs. live strategy codebases without automated parity tests.

## Phase 05: Strategy Positioning, Paper-Soak & Compliance GTM
- **Consensus Standards:**
  - **Mandatory 3-Stage Promotion Gate:** Every strategy must graduate through: (1) Out-of-Sample Purged Backtest -> (2) Live-Feed Paper Soak (measuring real L2 queue fills and latency) -> (3) Micro-Capital Canary before scaling allocation.
  - **Immutable TCA & Audit Trail:** Log every signal, pre-trade risk check, `ClOrdID` payload, and exchange fill to compute implementation shortfall (live vs. backtest slippage) and audit reports.
- **Hard Bans:**
  - **NO** promoting a strategy from offline backtest straight to full live capital without a live-feed paper soak.
  - **NO** marketing backtest equity curves as live returns or omitting max drawdown, capacity limits, and regulatory disclaimers.

## Phase 06: Kill-Switch, Cancel-on-Disconnect & Live Reconciliation Ops
- **Consensus Standards:**
  - **Exchange-Native Cancel-on-Disconnect (COD) + Out-of-Band Watchdog:** Enable exchange-level session COD (dead-man's switch) and run an independent watchdog process that cancels all open orders and flattens/halts if daily drawdown (`> X%`), consecutive API errors (`>= 3`), or spread/slippage bounds trip.
  - **Continuous Exchange-as-Truth Reconciliation:** Reconcile local `PENDING`/`FILLED` ledger state against exchange REST/drop-copy open orders, positions, and balances on startup, reconnect, and periodic intervals—treating the **exchange ledger as the source of truth**.
- **Hard Bans:**
  - **NO** relying solely on in-process `SIGINT`/`SIGTERM` hooks to cancel resting orders (fails on `SIGKILL`, OOM, or network partition).
  - **NO** auto-resuming live trading after a circuit-breaker trip without operator verification of position parity.
