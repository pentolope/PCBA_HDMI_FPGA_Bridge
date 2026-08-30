# PCBA_HDMI_FPGA_Bridge — HDMI-to-FPGA Video Bridge

**Benchmark ID:** 27  
**Difficulty:** 5/5  
**Brief detail:** 3/5  
**Category:** high-speed-video  
**Likely layer count:** 6  
**Primary stressors:** TMDS differential pairs, FPGA escape, clocking, connector pin ordering

## Design brief

Design a board that receives unencrypted HDMI video through an HDMI connector and delivers decoded pixel data or a parallel/video stream to an FPGA on the same board. Use a suitable HDMI receiver device; do not implement HDCP-protected content handling. Include EDID storage, configuration control, clocks, FPGA configuration memory, and a USB/debug interface. Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
