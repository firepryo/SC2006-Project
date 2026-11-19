# ADR-006: CCA category "Others"
Status: Accepted
Date: 2026-10-23
Context: The likely CCA source, data.gov.sg dataset `d_9aba12b5527843afb0b2e8e4ed6ac6bd`, groups CCAs by `cca_generic_name` into PHYSICAL SPORTS, VISUAL AND PERFORMING ARTS, UNIFORMED GROUPS, CLUBS AND SOCIETIES and OTHERS. The `cca_category` enum had only the first four.
Options:
- Add `Others` to `cca_category`: every CCA row in the dataset can be stored.
- Keep four values: the CCA sync skips OTHERS rows, so those CCAs never appear in search or comparison.
Decision: Add `Others` to `cca_category`. Chosen by the user.
Consequences: DATA-01 v1.0 enum and DDL include `Others`. INT-01 maps OTHERS to `Others`.
