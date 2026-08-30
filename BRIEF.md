# PCBA_HDMI_FPGA_Bridge — HDMI-to-FPGA Video Bridge
## Design brief

Design a board that receives unencrypted HDMI video through an HDMI connector and delivers decoded pixel data or a parallel/video stream to an FPGA on the same board. Use a suitable HDMI receiver device; do not implement HDCP-protected content handling. Include EDID storage, configuration control, clocks, FPGA configuration memory, and a USB/debug interface. Treat TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape as critical.
