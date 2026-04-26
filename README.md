# S&P 500 Dynamic Strategies - Option Profile and Trading Impact

## Objective
A quantitative study of dynamic portfolio strategies on **fifty years of S&P 500 data**, with closed-form theoretical predictions validated against daily rebalanced simulation. Built around the *Decomposition Theorem*, which expresses any self-financing dynamic strategy as a static option payoff plus a path-dependent gamma term.

## Project Overview & workflow

1. **Data retrieval** : dividend reinvested S&P 500 from `yfinance` and a synthetic USD bank account compounded daily from FRED Fed Funds rates.
2. **Descriptive statistics** : full-sample (1976+) versus post 2010 subsample, with a peak to valley drawdown profile.
3. **Black&Scholes proxy testing** : three independent tests of whether geometric Brownian motion is an adequate generative model for the S&P, the bracket identity $V_X \approx V_Y$, the linearity of $V_Y(t)$ in $t$, and the drift identity $E[X-Y] = \tfrac{1}{2}\sigma^2 dt$.
4. **Constant mix strategy** :  derivation of the SDE on the discounted scale, closed form solution, decomposition into Option Profile + Trading Impact, and validation for $l = 3$ (leveraged long), $l = -1$ (perpetual short), and $l = 1$ (buy-and-hold sanity check).
5. **Doubling strategy ("when in trouble, double")** : state dependent exposure rule, SDE solution, identification of the concave option profile, simulation with a leverage cap, and parameter sensitivity sweep.

## Key results

- **Recovered annualised volatility ~16%** from an OLS regression on the bracket process, matching the long run S&P figure.
- **Closed-form prediction matches daily simulation to within fractions of a percent** over fifty years and several orders of magnitude in wealth, a striking empirical confirmation of the Decomposition Theorem.
- **B&S verdict**: workable as a first order proxy, but volatility clustering in the variance residuals and decisively negative monthly skew rule it out as a generative model of risk.
- **Constant mix at $l = 3$** is wiped out by realised variance during 2008 the formal version of the volatility decay that ruins synthetic leveraged ETFs (TQQQ, UPRO).
- **Doubling strategy** never reaches its target on the historical S&P path under realistic leverage caps, illustrating the practical impossibility of guaranteed wealth recovery once the gambler's wealth is bounded.
- **The sign of trading impact is governed entirely by the convexity of the option profile**: concave profiles harvest gamma, convex profiles pay it. This explains why $0 < l < 1$ constant mix and the doubling rule benefit from volatility while $l > 1$, $l < 0$, and unhedged leveraged ETFs bleed through it.

## Takeaway

A strategy's path-dependent behaviour is fully encoded in the curvature of its terminal payoff. Any backtest that ignores this curvature will systematically misprice tail risk.

## Theoretical reference

Built on the Decomposition Theorem from N. Gaussel's *Advanced Topics in Financial Modelling* lecture notes (Université Paris 1 / Yukali, February 2024): any self financing strategy of the form $dV_t = f(S_t)\, dS_t$ admits the path by path decomposition

$$
V_t - V_0 = \underbrace{F(S_t) - F(S_0)}_{\text{Option profile}} - \underbrace{\tfrac{1}{2}\int_0^t f'(S_s)\, S_s^2\, \sigma_s^2 \, ds}_{\text{Trading impact}}
$$

where $F$ is any antiderivative of the holding function $f$.

## Authors

- Anjali Panarakottil Vijayan
- Aminata Barry

Submitted as the final project for *Advanced Topics in Financial Modelling*, taught by Nicolas Gaussel, April 2026.
