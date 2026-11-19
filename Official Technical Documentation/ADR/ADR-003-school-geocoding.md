# ADR-003: Filling school coordinates by geocoding
Status: Accepted
Date: 2026-10-23
Context: Distance (FR 7.4) needs `school.location`, but the dataset has no coordinates, only a postal code. Four postal codes in the dataset have lost their leading zero (e.g. `88256`).
Options:
- Geocode on sync via the OneMap Search API: stays current as schools move or merge; needs an external call.
- One-off seed file of coordinates: simpler, but goes stale.
Decision: The sync geocodes `postal_code` with OneMap, after left-padding it to six digits. Chosen by the user.
Consequences: `school.location` stays nullable. Geocoding runs only when `location` is NULL or `postal_code` changed. A failed lookup leaves `location` NULL and does not fail the sync; such schools are excluded from distance ranking. Endpoint, auth and limits go in INT-01; DATA-01 v0.2 records the rule.
