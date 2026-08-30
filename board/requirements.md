# Requirements — HDMI-to-FPGA Video Bridge

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `cf110f86f22791d1a2cbdd29bd7de158ec322715566b12028ad7f972bd3b3996`.

## Fixed by the brief

### REQ-01 — The board shall receive unencrypted HDMI video through an HDMI connector.

Brief text:

> receives unencrypted HDMI video through an HDMI connector

### REQ-02 — The board shall deliver decoded pixel data or a parallel/video stream to an FPGA located on the same board.

Brief text:

> delivers decoded pixel data or a parallel/video stream to an FPGA on the same board

### REQ-03 — The design shall use an HDMI receiver device suitable for the task (the brief names no specific part).

Brief text:

> Use a suitable HDMI receiver device

### REQ-04 — The design shall not implement HDCP-protected content handling.

Brief text:

> do not implement HDCP-protected content handling

### REQ-05 — The board shall include EDID storage.

Brief text:

> Include EDID storage, configuration control

### REQ-06 — The board shall include configuration control.

Brief text:

> Include EDID storage, configuration control, clocks

### REQ-07 — The board shall include clocks.

Brief text:

> Include EDID storage, configuration control, clocks

### REQ-08 — The board shall include FPGA configuration memory.

Brief text:

> Include EDID storage, configuration control, clocks, FPGA configuration memory

### REQ-09 — The board shall include a USB/debug interface.

Brief text:

> Include EDID storage, configuration control, clocks, FPGA configuration memory, and a USB/debug interface.

### REQ-10 — TMDS routing shall be treated as a critical design area.

Brief text:

> Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

### REQ-11 — ESD shall be treated as a critical design area (the brief states the concern, not the mitigation).

Brief text:

> Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

### REQ-12 — Reference planes shall be treated as a critical design area.

Brief text:

> Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

### REQ-13 — Receiver power integrity shall be treated as a critical design area.

Brief text:

> Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

### REQ-14 — FPGA escape shall be treated as a critical design area.

Brief text:

> Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

### REQ-15 — Stated brief requirements are authoritative and shall not be relaxed or reinterpreted by the design agent.

Brief text:

> Treat stated requirements as authoritative

### REQ-16 — Where the brief is silent, the design agent shall make and document reasonable engineering decisions rather than invent hidden user requirements.

Brief text:

> where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements

### REQ-17 — This repository should remain a consumer of the shared PCBA_AutoDesignAndTest toolkit rather than accumulating board-specific logic in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Which HDMI receiver device to use — vendor, part, package, and the input/output feature set it must cover.

The brief asks only for "a suitable HDMI receiver device" and names no part, vendor or family.

*Decision:* **not yet made.**

### OPEN-02 — Which form the receiver-to-FPGA video interface takes, and its width, signalling standard, sample rate and synchronisation scheme.

The brief offers a choice — "decoded pixel data or a parallel/video stream" — and fixes neither option nor any bus width, voltage or timing.

*Decision:* **not yet made.**

### OPEN-03 — FPGA selection: family, logic capacity, package, ball/pin count, I/O bank count and bank voltages.

The brief requires an FPGA on the same board but says nothing about which one or how large it must be.

*Decision:* **not yet made.**

### OPEN-04 — HDMI connector variant (type, mounting style, orientation, retention/shield strategy) and its placement relative to the board edge.

The brief says "an HDMI connector" without naming a type, part number, footprint or mechanical arrangement.

*Decision:* **not yet made.**

### OPEN-05 — How EDID storage is implemented — a dedicated non-volatile device versus emulation by another on-board device — plus its DDC addressing, write-protection and update path.

The brief lists EDID storage as required but specifies no device, capacity, bus, address or write policy.

*Decision:* **not yet made.**

### OPEN-06 — What performs configuration control (an on-board controller, the FPGA itself, or an external host over the debug interface) and over which control bus it reaches the receiver and other configurable devices.

The brief names "configuration control" as a required block without saying what implements it or what it controls.

*Decision:* **not yet made.**

### OPEN-07 — Clocking architecture: how many clock sources, which are crystals/oscillators versus recovered or synthesised clocks, frequencies, jitter budget, and the distribution/PLL topology.

The brief requires "clocks" and lists clocking as a stressor, but fixes no frequency, source type, count or jitter requirement.

*Decision:* **not yet made.**

### OPEN-08 — FPGA configuration memory device type and the configuration mode used, including whether the memory is also writable from the USB/debug interface.

The brief requires FPGA configuration memory but names no device, interface or configuration mode.

*Decision:* **not yet made.**

### OPEN-09 — What the USB/debug interface consists of: connector, USB role and speed, whether a bridge device is used, and whether it also carries FPGA programming/JTAG and console traffic.

The brief requires "a USB/debug interface" as a single phrase and does not decompose it into functions, devices or connectors.

*Decision:* **not yet made.**

### OPEN-10 — Power architecture: input supply source and voltage range, the set of rails, regulator topologies, current budgets, and any sequencing or ramp-rate constraints.

The brief is silent on power; the rail set is a consequence of parts that have not been chosen yet.

*Decision:* **not yet made.**

### OPEN-11 — ESD and port-protection strategy on the HDMI interface, including what is protected, the protection technology, and the capacitance budget it may consume on TMDS pairs.

The brief names ESD as an area to treat as critical — a stressor to address, not a device or topology it selects.

*Decision:* **not yet made.**

### OPEN-12 — Layer stackup: actual layer count and ordering, dielectric materials and thicknesses, copper weights, and which layers serve as reference planes for TMDS and for the FPGA escape.

Metadata gives 6 as a likely layer count only; the brief fixes no stackup, material or plane assignment, while naming reference planes as critical.

*Decision:* **not yet made.**

### OPEN-13 — Impedance targets and matching rules: single-ended and differential impedance values, intra-pair skew and inter-pair length-matching tolerances for TMDS and for the video bus.

The brief requires TMDS routing to be treated as critical but states no impedance, skew or matching number.

*Decision:* **not yet made.**

### OPEN-14 — Board outline, dimensions, mounting-hole pattern, keep-outs and whether the board is standalone or mates with a carrier/host.

The brief states no mechanical envelope, form factor or mounting requirement.

*Decision:* **not yet made.**

### OPEN-15 — Video bandwidth target: maximum supported resolution, refresh rate, colour depth and resulting TMDS bit/pixel-clock rate the board is designed to.

The brief says "HDMI video" without naming any resolution, frame rate, colour depth or clock rate; the target is a decision to be made and justified.

*Decision:* **not yet made.**

### OPEN-16 — Whether HDMI audio is de-embedded and delivered to the FPGA, and whether CEC, ARC/HEAC or the utility pin are supported or left unpopulated.

The brief scopes the board around video and does not state whether the other HDMI-carried functions are in or out of scope.

*Decision:* **not yet made.**

### OPEN-17 — DDC and hot-plug-detect topology: whether the HDMI cable-side supply domain is crossed at all and, if it is, how that crossing is handled — sourced, sensed, isolated, level-shifted or left unconnected — together with how HPD is asserted and what the DDC bus carries on each side.

The brief requires EDID storage but says nothing about the DDC/HPD electrical topology or whether any voltage-domain crossing is needed to serve it.

*Decision:* **not yet made.**

### OPEN-18 — FPGA pin assignment and escape plan: which banks carry the video bus, configuration, clocks and debug, and how fanout/escape is achieved on the chosen stackup.

The brief flags FPGA escape as critical but the FPGA, its package and its pinout are all unchosen, so no escape constraint is yet fixed.

*Decision:* **not yet made.**

### OPEN-19 — Bring-up and test provisions: test points, status indicators, probe access on the video bus, and any connector or header dedicated to validation.

The brief specifies no test, debug-visibility or instrumentation requirement beyond the USB/debug interface itself.

*Decision:* **not yet made.**

### OPEN-20 — Manufacturing constraints: fabricator and capability class, minimum trace/space, via technology (through, blind/buried, via-in-pad), assembly process and sides populated.

The brief names no vendor, process or capability limit; these follow from the stackup and escape decisions, which are themselves open.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json). **That file is the authoritative
   record**, and the only one the benchmark's scripts read: a decision written
   only in prose is invisible to `board_status.py` and to any result that
   counts how many decisions an attempt actually made.
2. Answer it under its `OPEN-nn` heading here as well, with the reasoning and
   the evidence that made the choice. This file is the readable copy; where the
   two disagree, the JSON is what happened.
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Asserting differential-impedance and trace-geometry numbers for the TMDS pairs without citing an actual fabricator stackup — the easiest and most common unsubstantiated claim on this board.
- Silently adopting a maximum resolution, colour depth or pixel-clock rate. The brief states none; the bandwidth target is an open decision that must be chosen and justified, not treated as given.
- Reproducing a receiver IC's reference design and presenting it as an analysed design, without citing the datasheet pages that actually constrain rails, decoupling and TMDS termination.
- Getting HDMI connector pin ordering, pair grouping or polarity wrong from memory. Every pin assignment must be traceable to the connector drawing and the HDMI pin definition; this error is invisible in review and fatal in hardware.
- Claiming an FPGA pinout is escapable on the assumed layer count without an actual fanout study against the package pin file, ball pitch, bank voltage rules and the fabricator's via/trace capability.
- Treating 'ESD' as discharged by dropping in a protection part. The brief lists ESD as a critical area, so the justification must include the device's capacitance budget against the TMDS pairs, not just its existence.
- Inventing rail voltages, currents or sequencing for parts that have not been selected. Power is entirely open here and depends on the receiver and FPGA chosen.
- Treating metadata's 'likely layer count: 6' as a fixed requirement rather than a hint — or conversely ignoring it and never justifying the stackup that is actually used.
