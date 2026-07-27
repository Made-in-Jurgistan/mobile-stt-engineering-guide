<div align="center">

# <img src="https://api.iconify.design/lucide:mic.svg?color=%230047ab" width="28" height="28" alt="" /> Mobile Speech-to-Text Engineering Guide

### The Definitive 2026 Production Guide for Mobile STT Systems

**33 Sections · Android · iOS · Edge · Cloud · Kotlin · Python · C++ · ONNX**

[![Version](https://img.shields.io/badge/version-2026.2.0-0047ab?style=flat-square)](https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/)
[![License](https://img.shields.io/badge/license-CC%20BY--SA%204.0-0047ab?style=flat-square)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Accessibility](https://img.shields.io/badge/WCAG-2.2%20AA-0047ab?style=flat-square)](https://www.w3.org/TR/WCAG22/)
[![Print Ready](https://img.shields.io/badge/print-A4%20ready-0047ab?style=flat-square)](https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/)

</div>

---

> **The complete signal-to-transcript pipeline** — from microphone capture to LLM-formatted output.
> Covers `whisper.cpp`, Moonshine v2, Silero VAD v6, ONNX Runtime, and the full production stack
> for building production-grade speech-to-text on mobile, edge, and cloud.

---

## <img src="https://api.iconify.design/lucide:book-open.svg?color=%230047ab" width="20" height="20" alt="" /> Table of Contents

| # | Section | Group | Focus |
|---|---------|-------|-------|
| 01 | About This Guide | Orientation | Prerequisites, audience, how to read |
| 02 | Pipeline Architecture | Orientation | End-to-end signal-to-text flow |
| 03 | Core Concepts & Terminology | Orientation | DSP fundamentals, sample rates, mel spectrograms |
| 04 | Audio Capture | Signal Layer | `AudioRecord`, `AVAudioEngine`, PortAudio, 16 kHz mono PCM |
| 05 | Pre-Processing & Noise | Signal Layer | RNNoise, WebRTC APM, Krisp SDK |
| 06 | Voice Activity Detection | Signal Layer | Silero VAD v6, Moonshine VAD, WebRTC VAD |
| 07 | Streaming & Chunking | Signal Layer | LiveKit, WebSocket, gRPC, ring buffers |
| 08 | Feature Extraction | Signal Layer | Log-mel spectrograms, `torchaudio`, `librosa`, `whisper.cpp` mel |
| 09 | Acoustic Models Landscape | Model Layer | Whisper, Moonshine, Sherpa-ONNX, Distil-Whisper |
| 10 | Whisper Architecture | Model Layer | Encoder-decoder internals, attention, alignment |
| 11 | Moonshine v1 & v2 | Model Layer | Low-latency on-device architecture, streaming |
| 12 | Streaming Decoders | Model Layer | CTC, RNN-T, transducer decoding strategies |
| 13 | Language Model Integration | Model Layer | External LM fusion, shallow/deep fusion, rescoring |
| 14 | Post-Processing | Output Layer | Punctuation, capitalization, inverse text normalization |
| 15 | LLM Formatting Layer | Output Layer | LLM-powered text refinement, diarization formatting |
| 16 | Android — Full Stack | Platforms | Kotlin IME integration, `AudioRecord` → ONNX → text |
| 17 | iOS Implementation | Platforms | `AVAudioEngine`, Core ML, Swift pipeline |
| 18 | Cloud Architecture | Platforms | Server deployment, GPU inference, autoscaling |
| 19 | Edge & On-Device | Platforms | TFLite, ONNX Runtime Mobile, quantization |
| 20 | whisper.cpp Deep Dive | Deep Dives | C++ internals, GGML tensor format, threading |
| 21 | Moonshine Deep Dive | Deep Dives | Architecture, ONNX export, inference optimization |
| 22 | Sherpa-ONNX Pipeline | Deep Dives | End-to-end ONNX pipeline, VAD + ASR + ITN |
| 23 | Model Benchmarks | Deep Dives | RTF, WER, latency, memory across models & devices |
| 24 | VoiceKeyboard IME Integration | Keyboard Integration | Android IME with voice-to-text, `InputConnection` |
| 25 | Performance & Optimization | Production | Latency budgets, memory profiling, battery impact |
| 26 | Privacy & Security | Production | On-device vs cloud, PII handling, encryption |
| 27 | Troubleshooting | Production | Common failures, diagnostic flowcharts |
| 28 | QA Checklist | Production | Pre-release quality gate, 50+ checkpoints |
| 29 | Open Source Index & Refs | Reference | Curated library of tools, papers, and repos |
| 30 | Advanced Debugging Field Manual | Reference | STT-specific debugging techniques |
| 31 | Backtrack & Self-Correction | Advanced Features | Model self-correction, backtrack heuristics |
| 32 | Personal Dictionary | Advanced Features | Custom vocab, domain adaptation, hotwords |
| 33 | Voice Command Mode | Advanced Features | Intent detection, command grammar, hybrid mode |

---

## <img src="https://api.iconify.design/lucide:key-round.svg?color=%230047ab" width="20" height="20" alt="" /> Key Technologies

| Category | Technologies |
|----------|-------------|
| **Acoustic Models** | Whisper, `whisper.cpp`, Moonshine v1/v2, Distil-Whisper, Sherpa-ONNX |
| **VAD** | Silero VAD v6, Moonshine VAD, WebRTC VAD |
| **Runtimes** | ONNX Runtime, ONNX Runtime Mobile, TFLite, Core ML, `whisper.cpp` (GGML) |
| **Audio** | `AudioRecord` (Android), `AVAudioEngine` (iOS), PortAudio, RNNoise, WebRTC APM |
| **Languages** | Kotlin, Python, C++, Swift |
| **Streaming** | LiveKit, WebSocket, gRPC, ring buffers |
| **LLM Integration** | Post-processing LLM formatting, diarization, ITN |
| **Platforms** | Android (API 30–36), iOS, Cloud (GPU), Edge (ARM) |

---

## <img src="https://api.iconify.design/lucide:sparkles.svg?color=%230047ab" width="20" height="20" alt="" /> Guide Features

- **<img src="https://api.iconify.design/lucide:ruler.svg?color=%230047ab" width="16" height="16" alt="" /> Print-Ready** — A4 duplex margins, page-break controls, print-safe color resets
- **<img src="https://api.iconify.design/lucide:accessibility.svg?color=%230047ab" width="16" height="16" alt="" /> WCAG 2.2 AA** — Keyboard navigation, skip links, `:focus-visible` outlines, reduced-motion support, forced-colors support
- **<img src="https://api.iconify.design/lucide:search.svg?color=%230047ab" width="16" height="16" alt="" /> SEO Optimized** — Open Graph, JSON-LD `TechArticle` structured data, canonical URL
- **<img src="https://api.iconify.design/lucide:palette.svg?color=%230047ab" width="16" height="16" alt="" /> Editorial Design** — Lora (display) · DM Sans (body) · JetBrains Mono (code); warm paper palette with cobalt blue accent (`#0047ab`)
- **<img src="https://api.iconify.design/lucide:smartphone.svg?color=%230047ab" width="16" height="16" alt="" /> Responsive** — CSS-only sidebar navigation, mobile hamburger menu, scroll progress indicator
- **<img src="https://api.iconify.design/lucide:zap.svg?color=%230047ab" width="16" height="16" alt="" /> Performance** — `content-visibility: auto`, `@property` typed custom properties, layered CSS architecture
- **<img src="https://api.iconify.design/lucide:rainbow.svg?color=%230047ab" width="16" height="16" alt="" /> Wide Gamut** — `color-gamut: p3` media query with OKLCH accent colors

---

## <img src="https://api.iconify.design/lucide:rocket.svg?color=%230047ab" width="20" height="20" alt="" /> Getting Started

### Read Online

Visit the hosted guide: **[Made-in-Jurgistan.github.io/mobile-stt-engineering-guide](https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/)**

### Read Locally

```bash
git clone https://github.com/Made-in-Jurgistan/Made-in-Jurgistan.github.io.git
cd Made-in-Jurgistan.github.io/mobile-stt-engineering-guide
open Mobile_STT_Engineering_Guide.html
# or serve locally:
python -m http.server 8000
# navigate to http://localhost:8000
```

### Print to PDF

Open the HTML file in Chrome/Edge → `Ctrl+P` → set paper size to A4 → enable background graphics → print to PDF.

---

## <img src="https://api.iconify.design/lucide:bar-chart-3.svg?color=%230047ab" width="20" height="20" alt="" /> Pipeline Architecture at a Glance

```text
Mic → 16kHz PCM → Pre-Processing → VAD → Chunking → Feature Extraction
                                                      ↓
                            Acoustic Model (Whisper / Moonshine / Sherpa)
                                                      ↓
                            Post-Processing → LLM Formatting → Transcript
```

---

## <img src="https://api.iconify.design/lucide:library.svg?color=%230047ab" width="20" height="20" alt="" /> Related Guides

| Guide | Focus |
|-------|-------|
| **Android Keyboard Design Guide** | Production IME development, API 30–36, Material You 3.0 |
| **Android Keyboard: 3D & Personalization** | 3D rendering, PBR materials, custom themes, game engine bridges |
| **Debugging Field Manual** | Cross-platform debugging, AI-augmented workflows, 30 sections |

---

## <img src="https://api.iconify.design/lucide:file-text.svg?color=%230047ab" width="20" height="20" alt="" /> Metadata

| Field | Value |
|-------|-------|
| **Author** | Made in Jurgistan |
| **Version** | 2026.2.0 |
| **Published** | 2026-07-23 |
| **Updated** | 2026-07-23 |
| **License** | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| **Accessibility** | WCAG 2.2 AA |
| **Canonical URL** | `https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/` |
| **Theme Color** | `#0047ab` (Cobalt Blue) |
| **Fonts** | Lora · DM Sans · JetBrains Mono |

---

## <img src="https://api.iconify.design/lucide:git-pull-request.svg?color=%230047ab" width="20" height="20" alt="" /> Contributing

Report issues or suggest improvements: [github.com/Made-in-Jurgistan/mobile-stt-engineering-guide-2026/issues](https://github.com/Made-in-Jurgistan/mobile-stt-engineering-guide-2026/issues)

---

## <img src="https://api.iconify.design/lucide:scale.svg?color=%230047ab" width="20" height="20" alt="" /> License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — Free to share and adapt with attribution. See [`LICENSE-STT.md`](LICENSE-STT.md) for details.

---

## <img src="https://api.iconify.design/lucide:quote.svg?color=%237c3aed" width="20" height="20" alt="" /> How to Cite

If you reference this guide in academic work, documentation, or project READMEs, please use one of the formats below. Both are consistent with the output generated by GitHub's "Cite this repository" button and the [`cffconvert`](https://github.com/citation-file-format/cffconvert) tool from the repository's `CITATION.cff` file.

### APA (7th Edition)

```text
Made in Jurgistan. (2026). Mobile Speech-to-Text Engineering Guide (Version 2026.2.0) [Computer software]. https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/
```

### BibTeX

```bibtex
@software{Made_in_Jurgistan_Mobile_Speech_2026,
  author = {Made in Jurgistan},
  month = {7},
  title = {{Mobile Speech-to-Text Engineering Guide}},
  url = {https://Made-in-Jurgistan.github.io/mobile-stt-engineering-guide/},
  version = {2026.2.0},
  year = {2026}
}
```

> **Note:** A `CITATION.cff` file at the repository root also enables GitHub's built-in "Cite this repository" button (right sidebar on the repo page), which auto-generates APA and BibTeX citations from the same metadata.

---

<div align="center">

**Made in Jurgistan** — Complete Edition · 2026

</div>
