# Dataset

Heavy equipment transaction data for the BSCS2008P selling-price prediction challenge.

| File | Rows | Notes |
|---|---|---|
| `train.csv` | 138,701 | Includes `TargetValue` |
| `test.csv` | 15,000 | Same features, no target |
| `metadata.csv` | 50 | Column descriptions |
| `sample_submission.csv` | 15,000 | `TransactionID`, `TargetValue` |

## Column reference

| Column | Description |
|---|---|
| TransactionID | Unique id for each accounting record |
| TargetValue | Transaction amount in USD (prediction target) |
| AssetID | Internal id for the machine |
| ProductConfigID | Code for the technical build of the unit |
| DataOriginCode | Software or platform the record came from |
| VendorPartnerID | External vendor or partner id |
| TransactionDate | Date the record was finalized |
| RegionCode | Geographic area or jurisdiction |
| ManufactureYear | Year the machine was produced |
| OperationalHoursMeter | Lifetime operating hours |
| UtilizationTier | Low / Medium / High usage |
| Spec_FullDescriptor | Full technical descriptor string |
| Spec_BaseClass | Broad equipment class |
| Spec_SubClass | Finer class within the base class |
| Spec_ReleaseSeries | Production series or version |
| Spec_VariantModifier | Revision or custom variant |
| FunctionalClassification | Operational role of the asset |
| AssetScaleFactor | Size or capacity relative to a standard unit |
| InventoryGroupCategory | Top-level inventory group |
| InventoryGroupDescription | Text description of that group |
| CabinType | Operator cabin / enclosure |
| DrivetrainType | Power-transfer system |
| Forks | Lifting attachment (legacy field) |
| col1 | Drive-system configuration |
| col3 | Stabilization subsystem |
| col4 | Extension-arm layout or reach |
| col5 | Engine air intake / aspiration |
| col6 | Primary extension module |
| col7 | Width of the working component |
| col8 | Protective housing or shielding |
| col9 | Rated power (hp / kW) |
| col10 | Hydraulic / fluid power system |
| col11 | Load-bearing / shock-absorption interface |
| col12 | Piercing / penetrating attachments |
| col13 | Finishing / smoothing attachments |
| col14 | Actuator control logic and hardware |
| col15 | Wheel or tire measurements |
| col16 | Coupling / joining mechanism |
| col18 | Ground traction system |
| col19 | Fluid flow rate |
| col20 | Tread or surface pattern |
| col21 | Ground-contact width |
| col22 | Operational-arm reach |
| col23 | Material-holding interface |
| col24 | Control-system configuration |
| col25 | Traction-component profile |
| col27 | Attached work-tool category |
| col28 | Steering-input configuration |
| col29 | Differential type |
| col30 | Operator steering interface |

`col2`, `col17`, and `col26` are not present in the files.

## Notes for modeling

- Drop identifier columns before fitting: `TransactionID`, `AssetID`, `ProductConfigID`.
- Several `col*` fields are more than 90% missing.
- `ManufactureYear` includes invalid values (for example 1001) that should be treated as missing.
- `Spec_FullDescriptor` has very high cardinality; the simpler spec columns are usually more useful.
