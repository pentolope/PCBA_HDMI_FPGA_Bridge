# Architecture — HDMI-to-FPGA Video Bridge

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- TMDS differential pairs
- FPGA escape
- clocking
- connector pin ordering

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## HDMI input port and cable interface

- Which HDMI connector type and mounting style is used, and what is the exact pin-to-signal mapping taken from its datasheet rather than from memory?
- How is TMDS pair polarity and pair ordering verified end to end, from connector pin numbers through the receiver's pin names?
- How are the connector shield and shell terminated to the board — directly, capacitively, resistively, or through a deliberate split — and where does cable-borne current return?
- How is the cable-side supply pin treated — sourced, sensed, isolated, or ignored — and what does that imply for HPD?
- Which HDMI pins (CEC, utility, ARC) are populated, and which are deliberately left unconnected?
- What mechanical retention and board-edge clearance does the connector require, and does it fit the chosen outline?

## TMDS routing and differential-pair integrity

- What differential impedance target is chosen for the TMDS pairs, and which stackup and trace geometry from the fabricator's data produces it?
- What intra-pair skew and inter-pair length-matching budget applies at the chosen maximum pixel clock, and where does that budget come from?
- How many layer transitions do the TMDS pairs take, and what return-path via strategy accompanies each one?
- What keep-out and spacing rules separate TMDS pairs from each other and from adjacent signals?
- Where does any ESD protection sit in the pair, and what is its capacitance loading relative to the TMDS budget?
- Are the pairs routed on a layer that is referenced to a continuous plane for their entire length, and how is that verified?

## HDMI receiver device selection and configuration

- Which receiver device is chosen, and what selection criteria (input rate range, output formats, package, availability) justify it over alternatives?
- What output format does it produce, and does that satisfy the brief's 'decoded pixel data or a parallel/video stream' requirement without extra glue?
- How is the receiver configured at power-up, and by what device over what control bus?
- What does the device require for reset, power-up ordering and strap/boot pins?
- Given HDCP is out of scope, which receiver features are deliberately unused, and does that affect its required support circuitry?

## Receiver power integrity

- What rails does the receiver require, at what voltages, tolerances and currents, per its datasheet?
- What decoupling network does the vendor specify or recommend, and how is it placed relative to each supply pin?
- Are any receiver rails required to be isolated, filtered or separately regulated from digital rails, and how is that implemented?
- What supply sequencing or ramp constraints does the receiver impose, and how does the power architecture guarantee them?
- How is plane or copper-pour area allocated so that the receiver's supply pins see low impedance at the frequencies of interest?

## Receiver-to-FPGA video interface

- What is the physical form of the video bus: bus width, signalling standard, voltage level and clocking scheme?
- What setup/hold and skew budget applies across the bus at the target pixel clock, and how is routing constrained to meet it?
- Are level translation or series termination needed between the receiver's output level and the FPGA bank voltage?
- How are the sync, data-enable and clock signals grouped and matched relative to the data lines?
- What happens on the bus during receiver reset or loss of input, and does the FPGA need to tolerate that?

## Clocking architecture

- What clock sources exist on the board, and what does each one serve?
- Is the receiver's recovered pixel clock the FPGA's video clock, or is a separate reference used, and what re-timing does that imply?
- What jitter and frequency-stability requirement does each consumer impose, and which datasheet states it?
- How are clock nets routed, referenced and terminated relative to the TMDS and video-bus rules?
- Where can clocks be probed during bring-up without disturbing them?

## FPGA selection, banking and escape

- Which FPGA and package is chosen, and what drove the choice — I/O count, logic capacity, package escapability, or something else?
- How are signals assigned to banks so that bank voltages match the video bus, configuration, clock and debug requirements?
- What escape strategy does the package require: how many routing layers, what via type, what trace/space, and does the fabricator support it?
- Which pins are fixed by the device (configuration, clock-capable, dedicated) and therefore constrain the pinout before any preference applies?
- How is the FPGA's power delivery arranged, including core, I/O and auxiliary rails and their decoupling?
- How is the pin assignment cross-checked against the vendor pin file rather than asserted?

## FPGA configuration and configuration memory

- Which configuration mode is used, and what mode pins, pull resistors and timing does the FPGA's configuration guide require?
- Which configuration memory device is chosen, and is it explicitly supported by the FPGA's configuration flow?
- Can the configuration memory be programmed in-system, and via which path?
- How does the configuration sequence interact with power sequencing and with the receiver's own reset?
- What indicates configuration success or failure to someone standing at the board?

## EDID, DDC and configuration control

- Where does EDID physically live, and what device or emulation serves it on the DDC bus?
- Is level translation or isolation needed on the DDC bus between the HDMI cable domain and board logic, and what pull-up values apply on each side?
- How is EDID content written or updated in the field, and is it write-protected in normal operation?
- What controls HPD assertion, and how is it sequenced against EDID being valid and the receiver being ready?
- Which device is the configuration-control master, what bus does it use, and what is the address map of everything on that bus?
- What is the defined behaviour if the source polls DDC before the board is fully powered or configured?

## USB and debug interface

- What is the USB role, speed and connector, and what device implements it?
- Does the debug path also carry FPGA programming, and if so how does it coexist with the configuration memory path?
- What differential impedance and routing rules does the chosen USB speed require, and from which specification?
- Does the interface supply or draw board power, and how does that interact with the power architecture?
- What ESD and overcurrent protection does the USB port get, and how is that decided separately from the HDMI port?

## Power architecture and sequencing

- How is the board powered, over what input connector and voltage range?
- What is the complete rail list, and for each rail what is the current budget derived from device datasheets rather than estimated?
- What sequencing order is required by the FPGA, receiver and memory together, and what enforces it?
- What regulator topology is chosen per rail, and what does that imply for switching noise near the TMDS and clock sections?
- How is rail health observable during bring-up?

## Stackup, reference planes and manufacturability

- What is the final stackup — layer order, materials, thicknesses, copper weights — and which fabricator's stackup table is it drawn from?
- Which layers reference the TMDS pairs, the video bus and the clocks, and are those planes continuous under every one of those nets?
- How are plane splits, if any, placed so that no critical net crosses one?
- What minimum trace/space and via geometry does the FPGA escape need, and does the chosen fabricator's capability page allow it at this layer count?
- What controlled-impedance callouts appear in the fabrication notes, and do they match the impedance targets used during routing?
- What test points, fiducials and assembly-process constraints does the board need for the chosen parts and sides?

## Answers still owed

All of them. See [status.md](status.md).
