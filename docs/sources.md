# Sources — HDMI-to-FPGA Video Bridge

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| HDMI receiver device datasheet | Supplies the input rate range, TMDS termination and biasing requirements, output bus format and timing, rail voltages/currents, reset and strap behaviour, and configuration register map — none of which may be assumed. |
| HDMI receiver vendor hardware-design / layout application note | The brief names receiver power integrity and reference planes as critical; the vendor's layout guidance is the citable basis for decoupling placement, plane treatment and TMDS entry rules. |
| HDMI connector datasheet and mechanical drawing | Connector pin ordering is a named stressor; pin numbering, pair assignment, shield/shell terminations and the footprint must come from the part's own drawing, not from recollection. |
| HDMI / TMDS and DDC-EDID interface specifications (and the EDID data-structure standard) | Defines pair assignment, differential impedance expectations, HPD and DDC behaviour, and EDID structure — the interoperability rules the board must satisfy at the connector. |
| FPGA family datasheet plus package pinout and pin-assignment files | FPGA escape is a named stressor; bank organisation, bank voltage rules, dedicated/clock-capable pins, ball pitch and package geometry are needed before any pinout or escape claim can be made. |
| FPGA configuration user guide | Fixes which configuration modes exist, which memory devices are supported, what mode-pin and pull-resistor circuitry is required, and how configuration timing relates to power-up. |
| Configuration memory device datasheet | Establishes interface, voltage, capacity and programming behaviour, and whether the device is compatible with the FPGA's chosen configuration mode. |
| Clock source (oscillator/crystal) and clock-distribution device datasheets | Clocking is a named stressor; frequency stability, jitter, load and start-up specs must be cited to show the receiver's and FPGA's clock requirements are met. |
| ESD/TVS protection device datasheets | The brief lists ESD as critical; the protection choice must be justified against clamping performance and, crucially, the line capacitance the TMDS pairs can tolerate. |
| Power regulator and power-sequencing device datasheets | Rail voltages, current capability, transient response, sequencing and enable behaviour must be sourced from the devices actually chosen, since the brief fixes no power architecture. |
| PCB fabricator capability and stackup/impedance documentation for the chosen layer count | Minimum trace/space, via technology, available stackups and controlled-impedance geometry determine whether the escape and the TMDS impedance targets are actually manufacturable. |
| Shared PCBA_AutoDesignAndTest toolkit documentation | The brief asks that this repo stay a consumer of the shared toolkit, so its interfaces and expected repository structure govern how the design is produced and stored. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
