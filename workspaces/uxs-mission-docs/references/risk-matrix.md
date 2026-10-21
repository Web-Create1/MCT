# Risk Matrix

A plain five by five matrix. Score = likelihood x severity.

## Likelihood

| Score | Word | Meaning for one run |
|-------|------|---------------------|
| 1 | Rare | Not expected at all |
| 2 | Unlikely | Could happen, not expected |
| 3 | Possible | Might happen in one run of several |
| 4 | Likely | Expected in most runs |
| 5 | Almost certain | Expected every run |

## Severity

| Score | Word | Meaning |
|-------|------|---------|
| 1 | Negligible | No effect on the objective |
| 2 | Minor | Objective partly met, rerun a segment |
| 3 | Moderate | Objective not met, vehicle recovered normally |
| 4 | Major | Vehicle leaves the geofence or needs an abnormal recovery |
| 5 | Severe | Harm to people or property, or vehicle lost |

## Bands

| Score | Band | Rule |
|-------|------|------|
| 1 to 4 | Low | Accept and note |
| 5 to 9 | Medium | Mitigate, name an owner, PIC accepts the residual |
| 10 to 25 | High | No go until a mitigation brings the residual to 9 or below |

The go threshold is a residual score of 9. In simulation, severity is scored as if the run
were real, so the plan stays honest when it moves to hardware.
