# Historical protocol — public text edition

Original SHA-256: `c01a1475039ee73d592c64c7f6421f64799546bb95cddcedcf10e56222d0ef0e`. Local path prefixes and links to undistributed private records are replaced with descriptive text; scientific criteria are preserved. This is historical provenance, not a newly approved execution plan.

# PROTOCOL: arXiv:2407.16689v2 (Giarè, Najafi, Pan, Di Valentino, Firouzjaee, "Robust Preference for Dynamical Dark Energy in DESI BAO and SN Measurements", JCAP 10 (2024) 035)

Committed 2026-10-13 before any computation on the paper's data (G2). Changes go in a dated addendum at the end, also before the run they affect. Anything not planned here is labelled `post_hoc` in the report.

Inputs: `paper.json` (V0 freeze and hashes), `claims/C1–C9-r1.json`, `conventions.json`, `paper_values.json` (printed numbers, parsed from the TeX by `checks/v1_transcribe.py`), `datasets.json` and `data/fetch_data.py` (pinned files and hashes).

Roles: this session is **A** (Claude). Everything it produces is **V2 only** (G19). V4 needs a blind **B** run by Codex in a new conversation with only its packet open (G23): the paper, the data links, the claims and the tolerance table of §3, nothing else. A's expectations are in `A-EXPECTATIONS.md`, committed with this file and sealed from B until B freezes its results. V5 needs a critic **C**, also a new Codex conversation.

Status of what A has seen before this commit: the paper's TeX (all of it; not the figures), the arXiv abstract page. A built the pipeline (`checks/models.py`, `checks/likelihood.py`) and timed it: one CAMB run at the paper's CPL Planck+DESI mean parameters to check that a tabulated w(a) gives the same result as CAMB's native w0–wa (it printed H0 = 64.57 for both; this is a code check at one point, not a posterior), and the full likelihood at three hand-chosen points (χ² printed, compared with nothing). No posterior, fit or best fit has been computed. A knows the DESI DR1 w0–wa results from training, not from the DESI paper; they are not used.

## 1. Implementation (fixed now)

**Code.** CAMB 2.0.4 (pip) in PPF mode; CPL through CAMB's native w0–wa, the other four forms as a 2,000-point spline table in a ∈ [1e-9, 1] (`checks/models.py`, written from the printed equations; no author code is used or known to be public, G13). The table is installed before the cosmology is set, so θ_MC → H0 uses the model's w(a) (control C0.1). Likelihoods through Cobaya 3.6.2 as an evaluator only (`checks/likelihood.py`): `planck_2018_highl_plik.TTTEEE_lite_native`, `planck_2018_lowl.TT`, `planck_2018_lowl.EE`, `act_dr6_lenslike.ACTDR6LensLike` (v1.2, variant `actplanck_baseline`, lmax 4000), `bao.desi_2024_bao_all`, `sn.pantheonplus`, `sn.desy5`. One massive neutrino of 0.06 eV, N_eff = 3.046, halofit mead2016 for lensing, `lens_potential_accuracy` 1. Every component is evaluated at every point and stored, so one CAMB call serves all three data combinations (PD = Planck+DESI, PDPP = +PantheonPlus, PDD5 = +DESY5).

**Priors.** As conventions.json (Table 1 of the paper; A_planck Gaussian 1 ± 0.0025). CAMB failures get zero likelihood and are counted (C9).

**Sampler: importance sampling with a surrogate-built proposal.** One full evaluation costs about 1.1 s on four threads (2.6 s on one thread, four workers in parallel); a Metropolis run to R−1 < 0.01 per model and dataset would take days, so posteriors are computed by importance sampling:
1. *CMB centre.* LCDM best fit to the Planck likelihoods alone (CMB and lensing, no BAO or SN), Py-BOBYQA from a fixed start (ω_b 0.0224, ω_c 0.120, 100θ_MC 1.0409, τ 0.054, n_s 0.965, ln10¹⁰A_s 3.044, A_planck 1), ≤ 400 evaluations. Used only as the centre of the surrogate's Gaussian CMB.
2. *Surrogate posterior per model and target (proposal only).* −2 ln L_s = Δᵀ C⁻¹ Δ + χ²_BAO + χ²_SN, where Δ is the six CMB parameters minus the step-1 centre, C the (omegabh2, omegach2, theta, tau, logA, ns) block of `base_plikHM_TTTEEE_lowl_lowE_lensing.covmat` (planck_supp_data_and_covmats), and χ²_BAO, χ²_SN are Cobaya's own DESI and SN likelihood classes fed with our background (`checks/background.py`: closed-form ρ_DE, radiation and one massive neutrino; θ_MC → H0 by root finding with the CosmoMC θ formula, r_drag from a fitting formula, both calibrated by a constant ratio against CAMB at 20 points per model). Sampled with emcee (seeded), 40 walkers × 4,000 steps, first 1,000 discarded.
3. *Proposal for target t.* q_t = 0.85 K_t + 0.15 T_t: K_t is a Gaussian-kernel mixture on 2,000 thinned surrogate samples with kernel covariance 0.7² Σ_s (Σ_s the surrogate covariance); T_t a multivariate Student-t (ν = 4) with the surrogate mean and covariance 2² Σ_s. A_planck is drawn from its prior. Draws outside the prior box are rejected and redrawn (the truncation constant cancels in self-normalised weights).
4. *Round 1.* 1,000 draws per target, 3,000 per model, for CPL, EXP, JBP, LOG, BA. Weights for target t: w = L_t π / q_mix with the balance heuristic q_mix = Σ_t N_t q_t / N over all draws of that model, so every draw serves all three targets.
5. *Gate (replaces R̂ for this sampler, G27):* Kish ESS ≥ 400 per target and largest normalised weight ≤ 0.03. A target that misses gets round 2: 1,000 draws from a kernel mixture on 1,000 points resampled from its weighted draws (kernel 0.7² × weighted covariance) plus the same 15 % Student-t, all rounds pooled with the balance heuristic. At most three rounds; a target still below the gate is `inconclusive on the gate`, with bootstrap Monte Carlo errors, and its outcome is stated only where the Monte Carlo error is below a fifth of the tolerance it is compared with.
6. Seeds: numpy PCG64, seed 16689 + 100·round + model index (CPL 0 … BA 4); emcee seed 26689 + model index. All draws, likelihood components and weights are saved (`checks/out/is/*.npz`, kept outside Git, SHA-256 in `checks/IS.sha256`). Monte Carlo errors on means and limits by bootstrap over draws (200 resamples).

**Best fits (C6).** For each model and LCDM and each target: Py-BOBYQA on −2 ln(posterior) (likelihoods plus the A_planck prior) in parameters scaled by their surrogate standard deviations, from the two highest-posterior draws of that target (LCDM: from the step-1 centre and from the CPL best fit with w0 = −1, wa = 0), ≤ 400 evaluations each, then one restart from the best (rhobeg 0.1 in scaled units, ≤ 200 evaluations). The lowest value is the best fit; the spread between starts and the restart drop are the minimiser precision. χ² reported without the A_planck prior term (conventions.json), the prior term listed.

**Statistics.** As conventions.json: posterior means, GetDist two-tail 68 % limits, one-tail 95 % upper limit for JBP w_a (Planck+DESI); w0 and wa prior ranges declared to GetDist.

## 2. Controls (run first)

- **C0.1 Tabulated w(a).** CPL as a table vs CPL native, at three points: every χ² component equal within 0.01 and H0 within 1e-4 relative. For EXP, JBP, LOG, BA: CAMB's H(z) and D_M(z) (from the Cobaya provider) against `background.py` at the same H0, z ≤ 3: relative difference < 2e-4 (massive-neutrino treatment differs slightly).
- **C0.2 Surrogate pieces.** Cobaya's DESI and SN χ² with our background vs with CAMB's, at five points per model: |Δχ²| < 0.1. θ_MC → H0 of the surrogate after calibration vs CAMB: |ΔH0| < 0.05 km/s/Mpc.
- **C0.3 CAMB accuracy.** χ² components at one point per model with our settings vs `AccuracyBoost` 1.5, `lAccuracyBoost` 1.5: total |Δχ²| < 0.3 (reported; a larger shift goes in an addendum before the runs).
- **C0.4 Prior-edge behaviour.** Fraction of round-1 draws per model where CAMB fails; reported, feeds C9.

## 3. Checks, tolerances and outcomes

Tolerances are for `held:reproduced`. A miss is first checked against our transcription, plik_lite and the lensing likelihood (G5) before it is called a discrepancy. σ below is the paper's 68 % half-width (mean of + and −).

| Claim | Check | Tolerance |
|---|---|---|
| C1 | SymPy (`checks/c1_algebra.py`): w(1) = w0 and −dw/da(1) = wa for all five forms; order at which EXP (and LOG, JBP, BA) departs from CPL around a = 1; a → 0 limits; closed-form ln f(a) against direct integration; JBP and BA from their redshift forms w0 + wa z/(1+z)² and w0 + wa z(1+z)/(1+z²); JBP symmetry w(a) = w(1−a) and the mirror redshift z' = (1+z)/z − 1 | Exact |
| C2 | CPL, three targets | **Fidelity gate**: PDPP and PDD5 means of w0, wa, H0, Ω_m within ± 0.4 σ and their half-widths within ± 30 %. PD column: w0, wa, H0, Ω_m means within ± 0.5 σ, half-widths within ± 40 % (prior-bounded, asymmetric). Other rows reported against ± 0.5 σ, not gating |
| C3 | EXP, JBP, LOG, BA, three targets each | As C2 per column. JBP PD w_a: our one-tail 95 % upper limit within ± 0.3 of 0.648 |
| C4 | For all 15 model–target pairs: 68 % and 95 % intervals of w0 and wa; P(w0 > −1), P(wa < 0) | Held if the 68 % interval of w0 lies above −1 and that of wa below 0 for all 15 (the paper's tables imply 68 %); 95 % reported. "Minimal impact" is assessed on the sign of the preference and reported (not tested) for its size |
| C5 | 2D credible level ℓ of (w0, wa) = (−1, 0) for all 15 pairs | PD: held if ℓ > 0.95 for all five models. SN: held if ℓ > 0.95 for all ten ("well outside": ℓ > 0.99 reported) |
| C6 | Best fits (§1): Δχ² for 15 pairs; ranking within each target | Each Δχ² within ± 1.0 of the printed value (plik_lite and minimiser vs the paper). Ranking: "BA best in all three targets" held if BA's Δχ² is the lowest in each target by more than the combined minimiser precision; `not resolved` where the gap is below it; contradicted where another model is lower by more than it. Same test for "CPL never best" and "JBP smallest except PDD5" |
| C7 | `checks/c7_text.py` on paper_values.json | Exact after half-up rounding to the printed digits: each sigma statement holds if the conventions.json rule gives at least (for "more than") or within ± 0.25 (for "almost", "approximately", "≳") the printed level; ranges and factors recomputed from the tables |
| C8 | From our PDPP and PDD5 posteriors (claim method) | z_p within ± 0.03; w(z_p) mean within ± 0.4 σ and half-width ± 30 %; z_c mean within ± 0.4 σ. JBP second pivot and crossing: checked against the mirror of the printed first ones (rounding intervals) and against our posteriors |
| C9 | (a) printed equations and CAMB modules; (b) CAMB failure fraction per model in all draws; LOG: maximum Ω_DE(z = 1100) over draws with posterior weight, and the posterior mass at wa > 0 for PD; all models: posterior mass with w(a → 0) > 0 per target | (a) recorded as a statement; (b) the footnote holds if Ω_DE(z = 1100) < 1e-3 for all LOG draws carrying weight; early-time w > 0 mass reported |

**Severity, fixed now (G18, 05 §3).** C2/C3 misses with the gate passed: Track R questions first (plik vs plik_lite, lensing, neutrinos, PPF); not a finding unless a conclusion changes. C4: a 68 % interval of w0 including −1 or of wa including 0 in any pair is an S1 scope note; failing in several pairs so that the abstract's "consistently" does not hold is an S2 candidate (full lane, B and C first on C4). C5: a PD ℓ ≤ 0.95 is S1 (conclusions wording; the abstract does not state the 95 % contour). C6: `not resolved` rankings are S1 (G20: the abstract states a ranking the χ² gaps cannot carry); a ranking contradicted by more than 1.0 in χ² in any target is an S2 candidate on the abstract's last sentence (full lane). C7, C8: S0–S1. C9: S0–S1, unless the LOG early-time condition fails for draws that carry more than 5 % of a posterior's weight (then S2 candidate on the LOG results, full lane).

## 4. Data re-tests (only after the C2 fidelity gate passes)

Data traces, not verification; they never change a claim outcome (G17). Best fits only (§1 best-fit recipe, from the paper-data best fits), for the five models and LCDM:
- **M1** Planck + DESI DR2 BAO (`bao.desi_dr2.desi_bao_all`, update role) + PantheonPlus.
- **M2** Planck + DESI DR2 + DES-SN5YR recalibrated (DES-Dovekie, Cobaya `sn.desdovekie`, update role).
Metric: Δχ² against LCDM and the ranking of the five models, with minimiser precision. If compute runs short, M2 first.

## 5. Literature (G21), after the runs

INSPIRE (WebFetch, record API): papers citing 2407.16689 that compare w(a) parameterisations with DESI (DR1 or DR2), errata, comments; the v1 → v2 changes in the tables (v1 PDF). Results to `literature.md` with queries and dates.

## 6. Stop rules

Round cap 2 per claim. Claim cap 10, 9 used. Every number in the report is printed by a script in `checks/` into `checks/out/` (G14). Effort is measured from the session log at the end of each stage (G28). Compute cap for the A pass: 14 h of wall clock from the first importance-sampling run for all sampling and minimisations; what has not finished by then is `not_run`.

## Addendum A1 (2026-10-13, before any importance-sampling run or best fit): controls C0.2 and C0.3

**What the controls showed** (`checks/out/c0_controls.out`). C0.1 passed (tabulated CPL vs native: max |Δχ²| 0.0017; CAMB vs `background.py`: ≤ 2.2e-5). C0.2 failed as written: at five random points per model (CMB parameters near Planck, w0 ∈ [−1.1, −0.4], wa ∈ [−2, 0.3]) the surrogate's DESI/SN χ² differs from CAMB's by up to 0.24 (BA; 0.05–0.14 for the others), against 0.1; the H0 part passed (≤ 0.001 km/s/Mpc). C0.3 exceeded its 0.3 reporting level at four of five random points (CPL 0.51, EXP 0.69, LOG 0.35, BA 1.07; JBP 0.03), almost all in `plik_lite` high-ℓ.

**Follow-up** (`checks/c0_followup.py`, `checks/out/c0_followup.out`), at the paper's printed means per model and column:
- C0.2: the surrogate error grows with the distance from the data (residual × a 1e-5 distance error); at the printed means the error in the χ² that each target actually uses is ≤ 0.022 (PD: BAO), ≤ 0.030 (PDPP: BAO + PantheonPlus) and ≤ 0.036 (PDD5: BAO + DES-SN5YR). The 0.155 maximum is PantheonPlus at Planck+DESI points, where SN data are not in the target.
- C0.3: the accuracy shift at the printed means is −0.43 to +0.06 for the models and −0.40 to +0.13 for LCDM at the same CMB parameters; model minus LCDM is −0.08 to +0.04. The shift is a common offset that cancels in Δχ² to < 0.1.

**Decision.** No change to §1. The surrogate builds the proposal only; weights and best fits use the full CAMB likelihoods, so its error can cost efficiency (caught by the ESS / max-weight gate), not bias. Default CAMB accuracy is kept: the Δχ² error from accuracy (< 0.1) is well inside the C6 tolerance (± 1.0) and the minimiser precision we report. C0.2 is recorded as failed at random points and passed at the printed means; C0.3 as reported. The surrogate's JBP Planck+DESI point used w_a = −0.5 (the table prints only an upper limit).

**Memory.** One Cobaya model with these likelihoods holds about 2 GB; all scripts build at most one model per process (four workers in parallel at most).

## Addendum A2 (2026-10-14 02:30 UTC, after CPL importance sampling, before any other model's result and before any best fit): compute budget

**Why.** A full evaluation costs 3.6 s per worker in the importance-sampling pool (CPL: three rounds of 3,000 draws, 2,700 s each; the gate needed all three rounds). At that rate the five models take about 11 h of the 14 h cap (§6, counted from 2026-10-13 23:36 UTC, the first draw), leaving about 3 h for 18 best fits and 12 re-test fits, which the §1 recipe (≤ 1,000 evaluations each) cannot meet. This addendum changes only the budget; CPL results (C2 gate passed) do not bear on it.

**Changes.**
- Best fits (C6): one start for each DDE model, the highest-posterior draw of the target, ≤ 250 evaluations, then the restart from it (rhobeg 0.1, ≤ 100). LCDM keeps two starts (the CMB centre and the CPL best fit at w0 = −1, wa = 0), ≤ 150 evaluations each, and the restart. Minimiser precision for a one-start fit is the restart drop, with a floor of 0.1 in χ²; the lowest χ² among the importance-sampling draws is reported beside each best fit as an upper bound. The C6 tolerance (± 1.0) and the ranking rule are unchanged.
- Order after importance sampling: best fits for all 18 pairs, then re-test M2, then M1 (§4), until the cap. Anything not finished at 2026-10-14 13:36 UTC is `not_run`.

## Addendum A3 (2026-10-14 05:25 UTC, during EXP round 3; no JBP, LOG or BA result exists yet): order of work under the cap

**Why.** Rounds now take 45–63 min (3.6–4.9 s per evaluation per worker), the container restarted once (≈ 40 min lost), and CPL and EXP each needed three rounds. Three rounds for JBP, LOG and BA plus the best fits would end about 3 h after the cap (2026-10-14 13:36 UTC), leaving C6 (the abstract's ranking) `not_run`. The cap is kept; the order changes so every claim gets an answer.

**Order** (`checks/run_a3.py`): finish EXP round 3; round 1 for JBP, LOG, BA; best fits for all 15 model–target pairs and LCDM (Addendum A2 budget, starts from the draws available then); round 2 for JBP, LOG, BA where the gate is not met; round 3 likewise; then re-tests M2 and M1. A job still running at the cap is stopped and counts as `not_run`.

**Reporting a posterior that misses the gate.** It is reported with its ESS, maximum weight and bootstrap error of the means, and every C3–C5 comparison for it is marked "below gate". A C3 miss below the gate is `inconclusive`, not `not_reproduced`, unless it exceeds the tolerance by more than three bootstrap errors.

*Note to A3 (05:25 UTC).* Swapping drivers closed the output pipe of the running EXP round 3, which then stopped near its end (lost, not used). The driver now writes job output to files (`checks/out/jobs/`), and EXP round 3 is redone after the best fits with the same seeds and proposals.
