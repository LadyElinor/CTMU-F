# What the Computation Validates
## A finite mathematical construction inspired by CTMU

Research manuscript, 19 September 2026.

The editable Word manuscript and Markdown source report a verified finite stochastic construction, not empirical validation of CTMU. The model has eight configurations and 512 supported six-transition histories. An exact bounded-state forward Markov representation reproduces its exponentially weighted path law.

## Contents

- `CTMU_Inspired_Computation_Paper.docx`: editable manuscript, including Office Math equations, four result/status tables, proofs, references, and research disclosure.
- `CTMU_Inspired_Computation_Paper.md`: full manuscript source with conventional numbered references.
- `reproduction/ctmu_f_02_audit/`: supplied retrospective audit, preserved original model, tests, archived results, and archived execution log.
- `reproduction/current_run/`: manuscript rerun, 26 passing tests, and supplementary calculation results.
- `reproduction/supplement.py`: initial/conditional KL decomposition, analytic entropy, limiting maximizer probabilities, and the horizon-extension identity.
- `provenance/CTMU_F_02_Retrospective_Audit.zip`: the original supplied archive, unchanged.
- `sources.json`: source identification, editions consulted, and scope of use.
- `SHA256SUMS.json`: content hashes for all other files in this package.

## Reproduce calculations

Python 3.10 or later, standard library only. The manuscript run used Python 3.13.5. From this package's `reproduction` directory:

```sh
cd ctmu_f_02_audit
python audit.py --output ../current_run/audit_results.json
python -m unittest -v test_audit.py
cd ..
python supplement.py
```

No physical observations, fitted physical parameters, or human participants are involved. This is a retrospective reproducibility check of AI-assisted project artifacts, not an independent external replication, preregistration, peer review, or proof-assistant verification. The ordinary mathematical proofs and numerical tests support different types of claims and are reported separately.

The final DOCX was checked for well-formed XML and rendered for visual inspection of all 13 pages. Its equations remain editable. No full Office conformance certification or native Microsoft Word execution is claimed. Rendering can differ slightly by software version and installed fonts.
