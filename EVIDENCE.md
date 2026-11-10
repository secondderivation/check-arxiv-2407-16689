# Documentary evidence and traceability

The bounded review reproduced algebra and selected parameter summaries, while documenting unresolved EXP fidelity and LOG tail checks.

EXP supernova fidelity and full-plik precision remain unmet; causes are unresolved, and further computation is parked.

This is a retrospective documentary record of existing work. No scientific script was executed to prepare it. Saved outputs are evidence of the named historical calculations, not fresh reproduction. Original protocols are linked separately; this document is not preregistration.

## Claim-by-claim evidence

### C1 — C1 in fixed reviewed version

All five w(a) forms: w(1)=w0, -dw/da(1)=wa, closed-form rho_DE, JBP and BA redshift forms, JBP mirror z'=1/z (A and B independently)

Retained outcome: held:reproduced. Adequacy: pass.

- [evidence/saved/c1_algebra.out](evidence/saved/c1_algebra.out)

### C2 — C2 in fixed reviewed version

CPL in all three data combinations within 0.2 sigma, widths 0.86-1.07 (fidelity gate)

Retained outcome: held:reproduced. Adequacy: pass.

- [evidence/saved/compare.json](evidence/saved/compare.json)
- [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json)

### C3 — C3 in fixed reviewed version

Historical importance-sampling evidence passed JBP PD/PDPP but left EXP PD, JBP DESY5 and LOG/BA below the sampling gate. The 26 October follow-up has fresh lite sampling/sign passes, while EXP SN w0 fidelity, full EXP DESY5 precision and LOG rare-tail criteria remain unmet; causes remain unresolved.

Retained outcome: unresolved. Adequacy: inconclusive.

- [evidence/saved/compare.json](evidence/saved/compare.json)
- [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json)
- [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md)
- [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md)
- [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json)

### C4 — C4 in fixed reviewed version

Historically all 15 saved 68% intervals had the reported signs, with 8/15 below the sampling gate. The 26 October follow-up combines fresh lite sampling/sign passes with historical CPL/JBP evidence; this does not retroactively repair old samples or establish universal posterior confirmation. No contrary sign detection is established.

Retained outcome: unresolved. Adequacy: inconclusive.

- [evidence/saved/is_CPL.json](evidence/saved/is_CPL.json)
- [evidence/saved/is_JBP.json](evidence/saved/is_JBP.json)
- [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json)
- [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md)
- [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md)
- [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json)

### C5 — C5 in fixed reviewed version

Saved PD and DESY5 contour estimates agree with the stated scope, but low-ESS targets do not establish precise contour levels. The withdrawn PantheonPlus scope objection remains withdrawn.

Retained outcome: unresolved. Adequacy: inconclusive.

- [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json)

### C6 — C6 in fixed reviewed version

Printed BA-first ordering is arithmetically correct. Saved candidate fits and limited further optimisation do not certify a stable global ranking; likelihood differences and best-fit method remain open (N1,N8).

Retained outcome: unresolved. Adequacy: inconclusive.

- [evidence/saved/ranking_audit.json](evidence/saved/ranking_audit.json)

### C7 — C7 in fixed reviewed version

LOG Planck+DESI wa sign typo (+1.33 vs -1.33) remains. The ratio 1.68/2.38 and tail 2.40 at ESS 144 are historical; the later LOG sign estimate is compatible with the quoted inequality but its rare-tail criterion remains unmet. Retain l.502 JBP, factor-of-5 and factor-of-2 wording notes (N4 S0+S1, N5 S0).

Retained outcome: held:discrepancy. Adequacy: pass.

- [evidence/saved/c7_text.out](evidence/saved/c7_text.out)
- [evidence/saved/c7b_tail_sigma.out](evidence/saved/c7b_tail_sigma.out)
- [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md)
- [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md)
- [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json)

### C8 — C8 in fixed reviewed version

Historical EXP SN pivots miss tolerance; earlier low-ESS targets remain exploratory and JBP second-crossing intervals are conditional on z<=6. Later accepted lite samples do not supply the uncomputed updated contours, pivots or crossing distributions. Printed-label/pivot slips remain S0 (N6); EXP fidelity and its cause remain unresolved (N3).

Retained outcome: unresolved. Adequacy: inconclusive.

- [evidence/saved/c8_pivot.out](evidence/saved/c8_pivot.out)
- [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json)
- [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md)
- [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md)
- [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json)

### C9 — C9 in fixed reviewed version

Crossing prescription is undocumented. Solver zero weights demonstrate exclusions in our implementation only. LOG early-DE statement is checked on the selected positive-weight subset, not the excluded region or whole prior.

Retained outcome: held:discrepancy. Adequacy: pass.

- [evidence/saved/c9_assumptions.out](evidence/saved/c9_assumptions.out)

## Why the attempt stopped

- [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md)
- [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md)
- [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json)

Failed sampling/precision or efficiency gates remain failed. Successful earlier controls do not establish a missing posterior. Cause, budget exhaustion and environmental failure remain distinct. No absent author material or unverified inference is labelled a paper error.

## Provenance and scope

The historical Claude first pass, Codex independent review and subsequent critique remain separately attributed. This public evidence edition was assembled by informed Codex P1. Numerical records are copied without recalculation; local host paths are omitted where present. The private source trace records exact originals. No correspondence or private case events are included. See [provenance](EVIDENCE-PROVENANCE.json).

Third-party paper text/data are linked by the fixed arXiv version; this report redistributes generated review outputs only. No licence for third-party data is inferred.

For C4 and C5, [compare.json](evidence/saved/compare.json) contains the exact saved sign/contour comparison records; [sampling_audit.json](evidence/saved/sampling_audit.json) supplies the separate adequacy gate. The failed gates constrain what those comparisons establish.

## Historical unavailable diagnostics

The following retained historical fields contain nonfinite values and are unavailable diagnostics, not finite validated estimates or zero. The original JSON remains unchanged. This is a disclosure of old evidence, not a fresh calculation failure.

- [evidence/saved/is_CPL.json](evidence/saved/is_CPL.json): `/targets/PD/mc_err_mean/H0`, `/targets/PD/mc_err_mean/omegam`, `/targets/PD/mc_err_mean/sigma8`, `/targets/PD/mc_err_mean/rdrag`, `/targets/PD/mc_err_mean/S8`, `/targets/PDPP/mc_err_mean/H0`, `/targets/PDPP/mc_err_mean/omegam`, `/targets/PDPP/mc_err_mean/sigma8`, `/targets/PDPP/mc_err_mean/rdrag`, `/targets/PDPP/mc_err_mean/S8`, `/targets/PDD5/mc_err_mean/H0`, `/targets/PDD5/mc_err_mean/omegam`, `/targets/PDD5/mc_err_mean/sigma8`, `/targets/PDD5/mc_err_mean/rdrag`, `/targets/PDD5/mc_err_mean/S8`.
- [evidence/saved/is_JBP.json](evidence/saved/is_JBP.json): `/targets/PD/mc_err_mean/H0`, `/targets/PD/mc_err_mean/omegam`, `/targets/PD/mc_err_mean/sigma8`, `/targets/PD/mc_err_mean/rdrag`, `/targets/PD/mc_err_mean/S8`, `/targets/PDPP/mc_err_mean/H0`, `/targets/PDPP/mc_err_mean/omegam`, `/targets/PDPP/mc_err_mean/sigma8`, `/targets/PDPP/mc_err_mean/rdrag`, `/targets/PDPP/mc_err_mean/S8`, `/targets/PDD5/mc_err_mean/H0`, `/targets/PDD5/mc_err_mean/omegam`, `/targets/PDD5/mc_err_mean/sigma8`, `/targets/PDD5/mc_err_mean/rdrag`, `/targets/PDD5/mc_err_mean/S8`.
