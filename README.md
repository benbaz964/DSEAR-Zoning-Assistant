# DSEAR Zoning Calculator

An Excel workbook for hazardous area classification under DSEAR. It sizes zones for flammable gases, vapours and dusts.

Gas and vapour zoning follows IEC 60079-10-1: release rate, hypothetical volume Vz, degree of ventilation, zone with availability, then EPL, gas group and T-class. Dust zoning follows IEC 60079-10-2.

## Sheets

| Sheet | Purpose |
| --- | --- |
| Quick Zone | Pick a substance, enter the amount and activity, and get the zoning. |
| Read Me | Method, equations and limitations. |
| Gas-Vapour | One row per source of release, up to 50 rows. |
| Dust | One row per dust source, up to 40 rows. |
| Substances | Gas and vapour property library. Add rows to extend the dropdowns. |
| Dusts | Dust property library. |
| Tables | Constants, k factors, the zone matrix and the T-class table used by every formula. |

Yellow cells are inputs. Grey cells come from the libraries. Green cells are results.

## Gas and vapour method

1. **Release rate.** Choked or subsonic gas release, liquid jet, or pool evaporation. Vapour pressure comes from an override cell, then Antoine, then Trouton.
2. **Minimum ventilation flow.** Uses k = 0.25 for continuous and primary grades, and 0.5 for secondary.
3. **Hypothetical volume Vz.** Indoors uses the air change rate. Outdoors uses 0.03 s⁻¹.
4. **Degree of ventilation.** High if Vz is under 0.1 m³. Otherwise Medium or Low, depending on room volume.
5. **Persistence time.** Calculated from the ventilation rate and LEL.
6. **Zone.** Set from grade of release, degree of ventilation and availability. EPL follows from the zone, and T-class from the autoignition temperature.

## Dust method

Releases give Zone 20 for continuous, 21 for primary and 22 for secondary. Layers give Zone 21 for poor housekeeping, 22 for fair and none for good. The more onerous result governs.

Maximum surface temperature is the lower of ⅔ of the cloud MIT and the 5 mm layer MIT minus 75 K.

## Limitations

- Vz measures ventilation effectiveness. It is not the zone extent. The hemisphere radius is indicative only, so set final extents by judgement.
- Substance data are indicative values from standard references. Check LFL, AIT, flash point and gas group against the SDS or IEC 60079-20-1 before relying on a result.
- The pool equation is not valid for liquids at or above their boiling point. Flashing releases need two-phase treatment.
- Hole sizes should follow IEC 60079-10-1 Table B.1 for the item and grade of release.
- This workbook supports a competent-person DSEAR assessment. It does not replace one.
