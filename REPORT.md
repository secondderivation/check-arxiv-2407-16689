# Robust Preference for Dynamical Dark Energy in DESI BAO and SN Measurements

[2407.16689v2](https://arxiv.org/abs/2407.16689v2) · Review 0.1.0-rc2

**Attempt documented.** The bounded review reproduced algebra and selected parameter summaries, while documenting unresolved EXP fidelity and LOG tail checks.

**Limit:** EXP supernova fidelity and full-plik precision remain unmet; causes are unresolved, and further computation is parked.

## Checked scope

- The bounded review reproduced algebra and selected parameter summaries, while documenting unresolved EXP fidelity and LOG tail checks.

Not checked: EXP supernova fidelity and full-plik precision remain unmet; causes are unresolved, and further computation is parked.

## Review record

| Claim | Method | Outcome / adequacy | Evidence |
|---|---|---|---|
| C1: C1 in fixed reviewed version — All five w(a) forms: w(1)=w0, -dw/da(1)=wa, closed-form rho\_DE, JBP and BA redshift forms, JBP mirror z'=1/z (A and B independently) | source\_check | held:reproduced / pass | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/c1_algebra.out](evidence/saved/c1_algebra.out) |
| C2: C2 in fixed reviewed version — CPL in all three data combinations within 0.2 sigma, widths 0.86-1.07 (fidelity gate) | source\_check | held:reproduced / pass | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/compare.json](evidence/saved/compare.json), [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json) |
| C3: C3 in fixed reviewed version — Historical importance-sampling evidence passed JBP PD/PDPP but left EXP PD, JBP DESY5 and LOG/BA below the sampling gate. The 26 October follow-up has fresh lite sampling/sign passes, while EXP SN w0 fidelity, full EXP DESY5 precision and LOG rare-tail criteria remain unmet; causes remain unresolved. | source\_check | unresolved / inconclusive | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/compare.json](evidence/saved/compare.json), [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json), [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md), [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md), [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json) |
| C4: C4 in fixed reviewed version — Historically all 15 saved 68% intervals had the reported signs, with 8/15 below the sampling gate. The 26 October follow-up combines fresh lite sampling/sign passes with historical CPL/JBP evidence; this does not retroactively repair old samples or establish universal posterior confirmation. No contrary sign detection is established. | source\_check | unresolved / inconclusive | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/is_CPL.json](evidence/saved/is_CPL.json), [evidence/saved/is_JBP.json](evidence/saved/is_JBP.json), [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json), [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md), [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md), [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json), [evidence/saved/compare.json](evidence/saved/compare.json) |
| C5: C5 in fixed reviewed version — Saved PD and DESY5 contour estimates agree with the stated scope, but low-ESS targets do not establish precise contour levels. The withdrawn PantheonPlus scope objection remains withdrawn. | source\_check | unresolved / inconclusive | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json), [evidence/saved/compare.json](evidence/saved/compare.json) |
| C6: C6 in fixed reviewed version — Printed BA-first ordering is arithmetically correct. Saved candidate fits and limited further optimisation do not certify a stable global ranking; likelihood differences and best-fit method remain open (N1,N8). | source\_check | unresolved / inconclusive | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/ranking_audit.json](evidence/saved/ranking_audit.json) |
| C7: C7 in fixed reviewed version — LOG Planck+DESI wa sign typo (+1.33 vs -1.33) remains. The ratio 1.68/2.38 and tail 2.40 at ESS 144 are historical; the later LOG sign estimate is compatible with the quoted inequality but its rare-tail criterion remains unmet. Retain l.502 JBP, factor-of-5 and factor-of-2 wording notes (N4 S0+S1, N5 S0). | source\_check | held:discrepancy / pass | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/c7_text.out](evidence/saved/c7_text.out), [evidence/saved/c7b_tail_sigma.out](evidence/saved/c7b_tail_sigma.out), [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md), [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md), [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json) |
| C8: C8 in fixed reviewed version — Historical EXP SN pivots miss tolerance; earlier low-ESS targets remain exploratory and JBP second-crossing intervals are conditional on z\<=6. Later accepted lite samples do not supply the uncomputed updated contours, pivots or crossing distributions. Printed-label/pivot slips remain S0 (N6); EXP fidelity and its cause remain unresolved (N3). | source\_check | unresolved / inconclusive | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/c8_pivot.out](evidence/saved/c8_pivot.out), [evidence/saved/sampling_audit.json](evidence/saved/sampling_audit.json), [evidence/followup/ASSESSMENT.md](evidence/followup/ASSESSMENT.md), [evidence/followup/NUMBERS.md](evidence/followup/NUMBERS.md), [evidence/followup/raw-audit.json](evidence/followup/raw-audit.json) |
| C9: C9 in fixed reviewed version — Crossing prescription is undocumented. Solver zero weights demonstrate exclusions in our implementation only. LOG early-DE statement is checked on the selected positive-weight subset, not the excluded region or whole prior. | source\_check | held:discrepancy / pass | [EVIDENCE.md](EVIDENCE.md), [evidence/saved/c9_assumptions.out](evidence/saved/c9_assumptions.out) |

[Protocol and provenance](PROTOCOL.md). This review record is retrospective.

## Bounded attempt

Historical algebra and transcription checks

Historical selected parameter-summary comparisons

Later lite sampling and full-plik EXP DESY5 continuation, with separate acceptance limits

Saved-diagnostic follow-up audit reported; no raw chain inspected now

Information boundary: Frozen local evidence through 3 November 2026, as checked for assembly on 10 November; no current external search.

Stop reasons: numerical_adequacy (established); budget (established); ambiguous_prescription (established); cause_unresolved (unknown)

Not started: None recorded.

Availability: unknown. 

Reopening condition: Concrete new settings/chains/code, identified implementation/support problem, or owner-approved discriminating matched control/tail check; committed plan/ACK and finite budget required.

Tools: Historical analysis tools documented in saved evidence. Human involvement: Owner parked further computation; documentary preparation does not restart it..

Effort (unknown): model minutes unknown, compute hours unknown, human minutes unknown.

## Review provenance

Prepared with AI assistance. Historical Claude first pass and Codex independent review/critique remain distinct; this assembly reads saved evidence and is neither blind B nor new P2. No scientific code was run in this assembly.

Tools: Claude (historical A); Codex (historical B/C and current informed assembly). Human involvement: Owner selected the preparation scope and approved the predecessor release published on 10 November 2026; the owner approved publication of this editorial revision on 11 November 2026.
