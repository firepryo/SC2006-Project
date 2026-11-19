# ADR-002: Mapping the dataset's main level to school type
Status: Accepted
Date: 2026-10-23
Context: The Data Dictionary defines four school types (Primary, Secondary, Junior College, Mixed Levels). The dataset's `mainlevel_code` has eight values, including MIXED LEVEL (P1-S4), MIXED LEVEL (S1-JC2) and CENTRALISED INSTITUTE (Millennia Institute).
Options:
- Map to the four types and also store the raw value: keeps the Data Dictionary model and the detail for display.
- Map to the four types only: loses detail such as S1-JC2 vs P1-S4.
- Replace the enum with the eight dataset values: diverges from the Data Dictionary.
Decision: Map to the four `school_type` values and store the raw value in `school.main_level`. Chosen by the user. Mapping is in DATA-01 §3.8.
Consequences: DATA-01 v0.2 adds `school.main_level`. A new, unknown `mainlevel_code` makes the sync log that record as failed (status Partial) rather than guess a type.
