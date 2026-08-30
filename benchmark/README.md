# Benchmark entry — board 27 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_HDMI_FPGA_Bridge` |
| Board id | `hdmi_fpga_bridge` |
| Category | high-speed-video |
| Difficulty | 5 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 6 |
| Primary stressors | TMDS differential pairs, FPGA escape, clocking, connector pin ordering |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

This is a difficulty-5 high-speed-video board with a mid-detail (3/5) brief: it fixes the block diagram and the critical-treatment list, then leaves every component and constraint open. The stressors it exercises are TMDS differential-pair routing, FPGA escape, clocking, and connector pin ordering — all of which fail quietly on paper and only show up in fabrication or bring-up. It tests whether an agent can build a defensible high-speed stackup, pinout and escape strategy from cited device and fab data instead of asserting plausible-sounding numbers.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
