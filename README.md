# HDMI-to-FPGA Video Bridge

A board that takes unencrypted HDMI video in on an HDMI connector and hands decoded pixel/parallel video to an on-board FPGA.

This repository holds the scaffold for an HDMI-to-FPGA video bridge: an HDMI connector feeds a suitable HDMI receiver device, and the recovered video is delivered as decoded pixel data or a parallel/video stream to an FPGA on the same board. The brief pins down the signal chain and a required feature set — EDID storage, configuration control, clocks, FPGA configuration memory, and a USB/debug interface — and explicitly excludes HDCP-protected content handling. It also names the areas that must be treated as critical: TMDS routing, ESD, reference planes, receiver power integrity, and FPGA escape.

At brief detail 3/5, everything below that outline is open. No receiver part, FPGA family, connector variant, clock source, power architecture, stackup, impedance target, board outline, or pixel-clock/resolution target is fixed; those are decisions for the design agent to make and document, not requirements to be assumed.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 17 requirements and deliberately leaves
20 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Video input | Unencrypted HDMI video received through an HDMI connector | brief |
| Video sink | An FPGA on the same board, fed decoded pixel data or a parallel/video stream | brief |
| HDMI receiver | A suitable HDMI receiver device — no specific part, vendor or family named by the brief | brief |
| Content protection scope | HDCP-protected content handling is explicitly out of scope | brief |
| EDID storage and configuration control | Both required on the board; implementation not specified | brief |
| Clocks | Required; number, source, frequency and distribution not specified | brief |
| FPGA configuration memory | Required; device type and configuration mode not specified | brief |
| USB/debug interface | Required; role, speed, connector and relationship to FPGA programming not specified | brief |
| Areas to treat as critical | TMDS routing, ESD, reference planes, receiver power integrity, FPGA escape | brief |
| Likely layer count | 6 | metadata |
| Benchmark class | Category high-speed-video; difficulty 5/5; brief detail 3/5 | metadata |
| Primary stressors | TMDS differential pairs, FPGA escape, clocking, connector pin ordering | metadata |
| Board outline, size, mounting and connector placement | Not fixed by the brief — design agent's choice, to be documented | open |
| Power architecture, rail set, sequencing and input supply | Not fixed by the brief — follows from the parts chosen; design agent's choice | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 27 of 32 |
| Category | high-speed-video |
| Difficulty | 5 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 6 |
| Primary stressors | TMDS differential pairs, FPGA escape, clocking, connector pin ordering |

This is a difficulty-5 high-speed-video board with a mid-detail (3/5) brief: it fixes the block diagram and the critical-treatment list, then leaves every component and constraint open. The stressors it exercises are TMDS differential-pair routing, FPGA escape, clocking, and connector pin ordering — all of which fail quietly on paper and only show up in fabrication or bring-up. It tests whether an agent can build a defensible high-speed stackup, pinout and escape strategy from cited device and fab data instead of asserting plausible-sounding numbers.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_HDMI_FPGA_Bridge.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `cf110f86f22791d1a2cbdd29bd7de158ec322715566b12028ad7f972bd3b3996`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
