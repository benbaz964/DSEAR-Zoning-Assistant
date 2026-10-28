# DSEAR Zoning Calculator

An Excel workbook for hazardous area classification under DSEAR. It sizes zones for flammable gases, vapours and dusts. Everything runs in plain Excel formulas, with no macros or add-ins.

Gas and vapour zoning follows IEC 60079-10-1: release rate, hypothetical volume Vz, degree of ventilation, zone with availability, then EPL, gas group and T-class. Dust zoning follows IEC 60079-10-2.

## Sheets

| Sheet | Purpose |
| --- | --- |
| Quick Zone | Pick a substance, an activity and an amount, and get the Zone 0, 1 and 2 extents with a plan view. |
| Read Me | Method, equations and limitations. |
| Gas-Vapour | One row per source of release, up to 50 rows. |
| Dust | One row per dust source, up to 40 rows. |
| Substances | Gas and vapour property library. Add rows to extend the dropdowns. |
| Dusts | Dust property library. |
| Tables | Constants, k factors, the zone matrix, the T-class table and the Quick Zone activities. |
| Quick Zone Calc | The workings behind Quick Zone, source by source. |

Yellow cells are inputs. Grey cells come from the libraries. Green cells are results.

## Quick Zone: why some activities have three zones

Each source of release has one grade. A continuous grade gives Zone 0, a primary grade gives Zone 1 and a secondary grade gives Zone 2. One activity can involve several sources at once, so Quick Zone sizes each source separately and nests the zones.

| Activity | Zone 0 | Zone 1 | Zone 2 |
| --- | --- | --- | --- |
| Closed containers / sealed system | Vapour space inside the containers | None: no release in normal operation | Leak or spill of the full amount |
| Decanting / filling / sampling | Vapour space inside the receiving container | Vapour pushed out of the container mouth while filling | Spill of the full amount |
| Open vessel / continuous emission | Evaporation from the open liquid surface | Vapour pushed out while charging the vessel | Spill or overflow of the full amount |

A zone drops out when:

- ventilation dilutes its source to negligible extent;
- a liquid is handled more than the flash point margin below its flash point;
- the substance is a gas, because a gas system holds no air, so there is no Zone 0 inside.

Where ventilation availability is fair or poor, IEC Table D.1 adds an outer zone sized with the failed-ventilation rate. Each zone sits at least 0.5 m beyond the zone inside it. Where Vz exceeds the room volume, the zone becomes the whole room.

The result panel shows each zone's extent, its equipment protection level and the source that sets it. A plan view draws the zones to scale.

## Quick Zone release rates

- **Spill (secondary).** Pool evaporation over amount ÷ spill depth, capped by any bund area.
- **Filling a container (primary).** Filling rate × saturated vapour density, plus evaporation from the container mouth.
- **Open liquid surface (continuous).** Pool evaporation over the vessel's liquid surface.
- **Charging an open vessel (primary).** Filling rate × saturated vapour density, plus evaporation from the surface.
- **Gases.** Every source uses the leak through the hole area at the stated pressure.

Filling rate, mouth area and vessel surface are screening assumptions on the Quick Zone sheet. Change them to match the task.

## Gas and vapour method

1. **Release rate.** Choked or subsonic gas release, liquid jet, or pool evaporation. Vapour pressure comes from an override cell, then Antoine, then Trouton.
2. **Minimum ventilation flow.** Uses k = 0.25 for continuous and primary grades, and 0.5 for secondary.
3. **Hypothetical volume Vz.** Indoors uses the air change rate. Outdoors uses 0.03 s⁻¹.
4. **Degree of ventilation.** High if Vz is under 0.1 m³. Otherwise medium or low, depending on room volume.
5. **Persistence time.** Calculated from the ventilation rate and LEL.
6. **Zone.** Set from grade of release, degree of ventilation and availability. EPL follows from the zone, and T-class from the auto-ignition temperature.

## Dust method

Releases give Zone 20 for continuous, 21 for primary and 22 for secondary. Layers give Zone 21 for poor housekeeping, 22 for fair and none for good. The more onerous result governs.

Maximum surface temperature is the lower of ⅔ of the cloud MIT and the 5 mm layer MIT minus 75 K.

## Substance data

Library values are indicative, from standard references. White spirit is a mixture: its vapour pressure uses n-nonane Antoine constants as a surrogate, and its boiling point is the start of the range. Check flash point, LFL, AIT and gas group against the SDS or IEC 60079-20-1 before relying on a result.

## Limitations

- Vz measures ventilation effectiveness. It is not the zone extent. Distances are indicative only, so set final extents by judgement.
- The pool equation is not valid for liquids at or above their boiling point. Flashing releases need two-phase treatment.
- Hole sizes should follow IEC 60079-10-1 Table B.1 for the item and grade of release.
- This workbook supports a competent-person DSEAR assessment. It does not replace one.
