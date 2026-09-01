# PCBA_HDMI_FPGA_Bridge — HDMI-to-FPGA Video Bridge
## Design brief

Design a board that receives unencrypted HDMI video through an HDMI connector and delivers decoded pixel data or a parallel/video stream to an FPGA on the same board. Use a suitable HDMI receiver device; do not implement HDCP-protected content handling. Include EDID storage, configuration control, clocks, FPGA configuration memory, and a USB/debug interface. Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

## Functional requirements

- No HDCP keys, provisioning or decryption on the board; operation shall not rely on any HDCP block in the receiver.
- Supported pixel clock range, colour depth and colour space shall be stated and within reach of receiver and capturing FPGA I/O.
- Pixel data, pixel clock, sync/data-enable and lock status shall reach FPGA pins able to receive them at that clock.
- Sink-side DDC and Hot Plug Detect shall be implemented, HPD asserting only when a valid EDID is readable, and the source's +5 V shall not be back-fed.

## Power and clocking

- All rails shall be enumerated with worst-case current, tolerance and ripple, and meet every device's sequencing and ramp limits.
- Receiver analog and PLL supplies shall be filtered, separated from switching rails and decoupled per the receiver vendor's guidance, with switching loops kept clear of the TMDS region.
- Clock sources shall meet the accuracy and jitter limits of every device they drive and route point-to-point over continuous reference.

## Signal integrity and routing

- TMDS pairs shall be 100 Ω differential, kept on one layer where practical, continuously referenced to an unbroken plane, and routed short.
- No TMDS pair may cross a plane split, gap or void; layer changes shall be minimised and given adjacent return vias.
- Intra-pair and inter-pair skew shall be budgeted from the maximum pixel clock and verified against routed lengths.
- The receiver-to-FPGA bus shall use FPGA banks matching the receiver's output levels and escape the package while meeting setup and hold at that clock.

## Protection and robustness

- Every exposed HDMI pin shall be ESD-protected to a stated IEC 61000-4-2 level, at the connector, ahead of any semiconductor.
- TMDS protection shall be low-capacitance, identical per pair, and shown to leave eye margin at the maximum data rate.
- Shield and shell grounding shall be deliberate and shall not return shield current across the receiver's reference plane.

## Test, bring-up and debug access

- FPGA configuration memory shall be programmable in system, with a path that still works when its contents are invalid.
- EDID shall be rewritable on an assembled board; FPGA configuration and debug pins, receiver control and reset lines, and the recovered pixel clock shall reach a header or test pads.

## Open choices

- Receiver device: must cover the specified format range, present an output the chosen FPGA can capture, and need no HDCP provisioning.
- FPGA device, configuration scheme and memory type, constrained by capture rate, I/O count and bank voltage.
- What the USB/debug interface must do, where it terminates, and which agent owns receiver configuration.
- Stackup, layer count and connector variant, driven by the TMDS and FPGA escape requirements.
