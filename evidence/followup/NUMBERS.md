# Recomputed saved-evidence summary

Arithmetic/source audit only; no new posterior.

| Target | Sampling | Signs at 68% | Fidelity misses (four selected parameters) |
|---|---|---|---|
| EXP_PDPP | True (fresh MCMC) | True | w0 |
| EXP_PDD5 | True (fresh MCMC) | True | w0 |
| LOG_PD | True (fresh MCMC) | True | none |
| LOG_PDPP | True (fresh MCMC) | True | none |
| LOG_PDD5 | True (fresh MCMC) | True | none |
| EXP_PD | True (fresh MCMC) | True | none |
| JBP_PDD5 | True (fresh MCMC) | True | none |
| BA_PD | True (fresh MCMC) | True | none |
| BA_PDPP | True (fresh MCMC) | True | none |
| BA_PDD5 | True (fresh MCMC) | True | none |
| CPL_PD | True (historical importance sampling) | True | historical; not re-audited here |
| CPL_PDPP | True (historical importance sampling) | True | historical; not re-audited here |
| CPL_PDD5 | True (historical importance sampling) | True | historical; not re-audited here |
| JBP_PD | True (historical importance sampling) | True | historical; not re-audited here |
| JBP_PDPP | True (historical importance sampling) | True | historical; not re-audited here |

| EXP data | w0 | MCSE | Offset / paper half-width | Width ratio |
|---|---:|---:|---:|---:|
| EXP_PDPP | -0.844779 | 0.001419 | 0.694 | 1.285 |
| EXP_PDD5 | -0.753931 | 0.002088 | 1.043 | 1.274 |

Full EXP DESY5: sampling True; precision False; combined False. w0=-0.754259, MCSE=0.002044; required <=0.002 (miss 2.21%).
Full minus lite=-0.000327; quadrature MCSE=0.002922; approximate two-MCSE interval=[-0.006172, 0.005517]. Full minus paper=0.049741.
Full w0 chain means range [-0.758004, -0.750526]; second-minus-first half=-0.002553.
LOG PD: P(wa<0)=0.99484019, MCSE=0.00073637, effective rare-tail=48.845944 < 50; unresolved. One-sided Gaussian equivalent=2.564932, transformed two-MCSE endpoints=[2.4765712881552133, 2.6794594601999746]. This is not a model-comparison significance.
