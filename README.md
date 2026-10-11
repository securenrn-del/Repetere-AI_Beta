```markdown
# Repetere AI (v0.5.1-beta)

**Author:** Nathaniel Richardson Jr.  
**Repository:** [https://github.com/securenrn-del/repetereai](https://github.com/securenrn-del/repetereai)  
**Binary Distribution:** Standalone 1-Click Setup (`RepetereAI-Setup-v0.5.1-beta.exe`) via [GitHub Releases](https://github.com/securenrn-del/repetereai/releases)[cite: 2, 6]

> ⚠️ **BETA NOTICE:** This is an active preview workstation engineered strictly for local execution on NVIDIA CUDA hardware. Local generation requires dedicated processing time—especially for neural audio decoding and weight streaming. Image diffusion is currently an interface layout preview (backend rendering lands in v0.6.0)[cite: 2]. If you encounter hardware-specific edge cases, please submit an issue on GitHub.

**Repetere AI** is a native Windows C++ multimodal desktop workstation engineered to restore computing sovereignty[cite: 6]. Built directly on low-level Win32, Dear ImGui, GLFW, and OpenGL 3 runtimes, it eliminates cloud subscriptions, telemetry, tracking, and webview wrapper memory bloatware[cite: 6]. It delivers private, uncensored intelligence directly on consumer NVIDIA GeForce RTX hardware[cite: 6].

---

## ⚡ System Requirements

| Component | Minimum Specification | Recommended Specification |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 / 11 (64-bit) | Windows 11 (64-bit) |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM) | NVIDIA RTX 40/50-Series (12 GB+ VRAM)[cite: 6] |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+) | Latest NVIDIA Studio Drivers |
| **System Memory** | 16 GB Physical RAM[cite: 6] | 32 GB Physical RAM (Required for Hybrid Mode) |
| **Target Storage** | 20 GB free space on SSD | 50 GB+ free space on NVMe SSD |

---

## 🚀 Quick Start: Installation & First Launch

1. Download **`RepetereAI-Setup-v0.5.1-beta.exe`** from [GitHub Releases](https://github.com/securenrn-del/repetereai/releases)[cite: 2, 6].
2. Run the installer[cite: 5]. It installs cleanly into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrator privileges[cite: 5].
3. Launch **Repetere AI** from your Desktop shortcut or the Start Menu[cite: 1, 5].
4. Click anywhere on the startup splash screen to enter[cite: 2, 5].
5. The **Hardware Configuration Diagnostic** modal will profile your GPU VRAM and system memory[cite: 1, 6]. Click **Confirm Hardware** to enter the main workstation[cite: 4].

---

## 📦 How to Download & Manage AI Models

AI models are the local weights that power each workspace. They must be present on disk before generation can proceed[cite: 2, 5].

### In-App Downloader (Recommended):
1. In the top menu bar, click **Settings ➔ Repetere Models**[cite: 2, 4].
2. The catalog overlay lists verified models tuned for your hardware[cite: 1, 4]:
   * **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B*)[cite: 1]
   * **General Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 1, 2]
   * **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 1, 2]
   * **Audio / Music Studio (Both Required):**
     * *YuE2 3B Music & Vocal Engine* (`yue2-3b-q4_0.gguf`, ~2.48 GB)[cite: 1, 4]
     * *YuE2 Neural Audio VAE Decoder* (`yue2-vae-f16.gguf`, ~265 MB)[cite: 1, 4]
3. Click **[ Download ]**[cite: 1, 4]. The in-app manager streams chunks via CPR with real-time transfer speeds and validates the 4-byte GGUF magic header (`0x46554747`)[cite: 6, 8, 10].
4. When complete, the badge turns green (**Installed**). Click **[ Return to Workspace ]**[cite: 4, 8, 18].

### Manual Weight Placement (Advanced Users):
You can place `.gguf` weight files directly into your local installation directory:
```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

*(Ensure filenames match the catalog schema exactly so internal CLI arguments resolve cleanly).*

---

## 🧭 Navigating the Workspaces

Repetere AI partitions workflows across five isolated environments:

### 1. CODING

* **Engine Target:** Qwen 2.5 Coder 7B / 14B / 32B Instruct (`Q4_K_M`)


* **Syntax Presentation:** Automatically extracts triple-backtick language blocks (```) into horizontal-scrolling containers with snippet-level **Copy** buttons.


* **Quick Response Copy:** Single-click **[ Copy Full Response ]** action directly beneath assistant outputs for rapid clipboard export.
* **Context Preservation:** Multi-turn message serialization preserves conversational history across iterative debugging sessions.

### 2. CHAT

* **Engine Target:** Meta Llama 3.1 8B Instruct (`Q4_K_M`)


* **General Intelligence:** Tuned for logical reasoning, document summarization, and interactive assistance.


* **Memory Reset:** The red **Clear Chat** button archives transcripts to disk while resetting active VRAM context.



### 3. CREATIVE WRITING

* **Engine Target:** Hermes 3 Llama 3.1 8B / Narrative checkpoints


* **Uncensored World-Building:** Tailored for complex narrative progression, scene development, scriptwriting, and dialogue without cloud filtering.



### 4. AUDIO (MUSIC) Production Studio

* **Engine Target:** YuE2 Neural Audio Synthesis Engine (`yue2-3b-q4_0.gguf` / `yue2-3b-q8_0.gguf` + `yue2-vae-f16.gguf`)


* **Full-Song Vocal Synthesis:** Generates full vocal and instrumental tracks based on style tags (e.g., Alternative Rock, 110 bpm, driving drums) and structured lyrics (`[Verse]`, `[Chorus]`, `[Bridge]`) with generation durations configurable up to 300 seconds.


* **Expanded Lyrics Buffer:** 8192-byte input memory buffer (`Types.h`) preventing text truncation on long multi-verse compositions.


* **Input Sanitization:** Automatically sanitizes quotes and flattens multi-line breaks to prevent Windows `cmd.exe` subshell argument chopping.


* **Dynamic Model Discovery:** Embedded engine scanner detects any installed YuE2 quantization (prioritizing `q8_0` > `q5_k_m` > `q4_k_m` > `q4_0`) alongside `yue2-vae-f16.gguf` without hardcoded path dependencies.


* **Smart File Serialization:** Tracks are saved as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` in `output/music/`.


* **Master Transport:** Play output tracks immediately via Win32 system shell integration to your default media player.



### 5. IMAGES (DIFFUSION) Studio (Preview)

* **Status:** ⚠️ **Visual Layout Preview (Live Diffusion Engine scheduled for v0.6.0).**

* **Current Features:** Dual positive/negative prompt buffers, step/CFG sliders, resolution presets, and native file dialogs (`OpenNativeFileDialog`) for base reference images.

---

## ⚙️ Hardware Compute Modes

* **GPU Mode (Active Default):** Confines execution strictly to dedicated GPU VRAM for maximum token throughput and minimum latency.


* **HYBRID Mode (Interface Preview):** Top-bar toggle with confirmation dialogs. Spans weights across system RAM and VRAM for running 14B–32B models on lower-tier cards (full dynamic layer allocation unlocks in v0.6.0).



---

## 🔒 Conversation History & Persistence

* **Local JSON Persistence:** Transcripts serialize to `chat_history.json` on context clearing or application shutdown, supporting dynamic model tags across sessions.


* **Transcript Viewer:** Accessible via **History ➔ Open History** with foreground z-index prioritization (`ImGui::SetNextWindowFocus()`).


* **Context Restoration:** Single-click **[ Load Conversation into Active Tab ]** restores archived discussions directly into active working memory.


* **History Wipe Guard:** Deletion actions trigger a modal confirmation dialog to prevent accidental data loss.

---

## 🛠️ What's New & Fixed in v0.5.1-beta

* **Dynamic YuE2 Model Discovery:** The audio engine scanner (`FindBestYueModel`) recursively discovers any installed YuE2 quantization (including `yue2-3b-q4_0.gguf`, `yue2-3b-q8_0.gguf`, etc.) alongside `yue2-vae-f16.gguf` instead of crashing on a hardcoded path.


* **Robust Subshell Argument Sanitization:** Hardened CLI string formatting for `audiocpp_cli.exe`. Quotes (`"`, `'`) and raw newlines are stripped and escaped to eliminate `cmd.exe` subshell truncations and exit code failures.


* **Expanded Lyrics Memory Buffer:** Increased `lyricsBuffer` in `Types.h` to 8192 bytes, allowing complete multi-verse arrangements, tags, and bridges to be processed without buffer overflow.


* **Multi-Turn Context Serialization:** `InferenceClient` serializes prior conversational message turns into request payloads, preserving iterative context memory across turns.


* **Universal Model History Persistence:** Updated `HistoryManager` JSON serialization routines to support dynamic model tags (such as Meta Llama 3.1 and Hermes 3) rather than hardcoded identifiers.


* **Safe Music Generation Guard:** Added UI validation in `RenderMusicStudioWorkspace` that disables synthesis buttons and alerts the user if required YuE2 weights or VAE files are missing.


* **Foreground History Modal Snap:** Corrected z-indexing and window focus flags (`ImGui::SetNextWindowFocus()`) so the transcript overlay consistently opens in the foreground.


* **Linker & Object Collision Fixes:** Resolved duplicate symbol linker errors (`LNK2005`) between `FREEAI.obj` and `Theme.obj` by isolating `stb_image` implementation definitions.


* **High-DPI 1600p+ Viewport Optimization:** Preserved scaled 24pt/28pt Segoe UI font metrics, auto-maximizing window commands, and 1.15× responsive layout styling (`ImGuiStyle::ScaleAllSizes`).


* **Optimized Inno Setup Packaging:** Configured parallelized LZMA2 solid compression (`LZMANumBlockThreads=8`) excluding legacy internal runtime directories to deliver a fast compile and an installer size (~1.29 GB) within release thresholds.



---
TO DO LIST: Upcoming Features
---
### Repetere AI: Workstation Evolution & Architectural Solutions

---

### 1. Multi-Vendor Compute Strategy: Universal GPU & APU Support

* **The Problem:** Compiling strictly for NVIDIA CUDA isolates AMD Radeon, Intel Arc, and integrated APUs/iGPUs, preventing broad hardware accessibility.


* **The Solution:** Implement a dual-backend architecture:
* **Bundled Execution Engines:** Ship pre-compiled binaries in `bin/cuda/llama-server.exe` (peak token performance on NVIDIA) and `bin/vulkan/llama-server.exe` (universal compute across AMD, Intel, and APUs).
* **Automated Vendor Discovery:** Update `HardwareScanner.h` to read DXGI `desc.VendorId`:


* `0x10DE` $\rightarrow$ NVIDIA (Default to CUDA).
* `0x1002` (AMD) / `0x8086` (Intel) $\rightarrow$ Default to Vulkan.


* **User Backend Override:** Add an ImGui toggle under `Settings -> Acceleration` (`[Auto-Detect]`, `[CUDA]`, `[Vulkan]`) that dynamically switches the sidecar path without modifying the core orchestrator loop.
* **Dual-Pipeline Routing (APU / Discrete GPU):** Instead of layer-splitting a single model across slow PCIe buses, run independent sidecars on separate ports:
* **dGPU (Device 0 / CUDA):** Dedicated to heavy text/code LLM generation on port 8080.


* **APU/iGPU (Device 1 / Vulkan):** Dedicated to background tasks, audio synthesis (`audiocpp_cli.exe`), or embeddings on port 8081.







---

### 2. UI Layout Overhaul: The 4-Zone Workstation Shell

* **The Problem:** Flat horizontal tabs with trailing header buttons cause layout clipping, restrict screen real estate, and feel like a prototype rather than an integrated workstation.


* **The Solution:** Refactor the Dear ImGui shell into four distinct structural zones designed for high-resolution displays:


* **Left Activity Rail (~70px):** Vertical icon bar to toggle active workspaces (`CODE`, `CHAT`, `WRIT`, `SONG`, `DIFF`).


* **Top Telemetry Header:** Displays workspace breadcrumbs, active `.gguf` checkpoint, and the `[GPU / HYBRID]` compute switch.


* **Central Viewport:** Modality-specific canvas viewports.


* **Bottom Diagnostic Shelf (~32px):** Real-time monitoring of sidecar process health, dedicated VRAM usage (DXGI), and host RAM load.





---

### 3. CODING: Split-Pane IDE & Agentic Diff Engine

* **The Problem:** Streaming full file rewrites across chat bubbles wastes token bandwidth, generates latency, and risks compilation breaks.
* **The Solution:**
* **Workspace Split:** 35% chat inspector on the left; 65% code canvas using `ImGuiColorTextEdit` on the right.


* **Surgical Diff Engine:** Local Qwen 2.5 Coder is instructed via prompt contracts to output standard `<<<<<<< SEARCH / ======= / >>>>>>> REPLACE` blocks.


* **In-Place Patching:** A C++ parser fuzzy-matches lines in the active editor buffer, replaces code in place, and visually highlights modified lines without rewriting the entire file.
* **System Compiler Toolchain Discovery:** Rather than bundling multi-gigabyte compiler toolchains into the setup package, detect system-installed compilers (`cl.exe`, `g++`, `clang++`, `python.exe`) via `PATH`.


* **Sandboxed Execution Drawer:** Execute code via `CreateProcessW` wrapped inside a Windows Job Object (enforcing execution timeouts and memory limits), streaming `stdout`/`stderr` through anonymous pipes directly into a bottom terminal tray.



---

### 4. AUDIO (MUSIC): Arrangement Rack & Saved Track Deck

* **The Problem:** Music synthesis via `audiocpp_cli.exe` (YuE2) was isolated to flat text boxes without arrangement controls, track history, or easy styling syntax.


* **The Solution:**
* **Arrangement Rack (Upper Deck):** Retains the 8192-byte `lyricsBuffer` with one-click **Vocal Directive Chips** (`[Singer 1 - Screaming]`, `[Clean Belt]`, `[Rap / Clinical Cadence]`, `[Dynamic Drop]`). Clicking a chip appends structural brackets directly into the lyric string without manual formatting.


* **Saved Audio Deck (Lower Deck):** Scans `output/music/` using `<filesystem>` on startup, populating past renders with file size, timestamps, and one-click `[▶ Play]`, `[⏹ Stop]`, and `[Edit in Rack]` actions.


* **Metadata Restoration:** `[Edit in Rack]` parses the track's metadata sidecar file and reloads its exact lyrics, style tags, and BPM back into active memory buffers.


* **Two-Stage Generation:** Natural language prompts are first parsed on port 8080 by the text LLM to construct acoustic tags and verse formatting, then handed off to `audiocpp_cli.exe` with sanitized arguments.





---

### 5. IMAGES: Photoshop-Style Studio with Zero VRAM Leaks

* **The Problem:** Binding large collections of image textures into GPU memory simultaneously leads to rapid VRAM exhaustion and crashes.


* **The Solution:**
* **3-Column Studio Layout:** Left Inspector (Prompts, steps, CFG, aspect ratio), Center Viewport (Interactive canvas), and Right Saved Assets Gallery.


* **Dynamic Texture Virtualization:** Only the single active image displayed on the canvas is bound to GPU VRAM. Loading or generating a new image calls `glDeleteTextures(1, &activeCanvasTexture)` before binding the next texture.


* **Metadata Disk Browser:** The right-hand gallery scans `output/images/` via `<filesystem>`, loading only filename and size metadata into a lightweight table with zero idle VRAM footprint.


* **Interactive 2D Transform Canvas:** ImGui drawlist viewport supporting mouse-wheel zoom (10% to 600%) and right/middle-click panning across an OpenGL quad.



---

### 6. CREATIVE WRITING & CHAT

* **CREATIVE WRITING (Manuscript Studio):**
* **Live Chapter Canvas:** Binds directly to `.txt`/`.md` chapter files via `ImGuiColorTextEdit`.
* **Lore Drawer & Story Bible:** Collapsible reference drawer containing character profiles, timeline constraints, and world rules that are automatically prepended to the system prompt to prevent narrative drift.
* **Targeted Scene Diffs:** Highlight an excerpt or beat, prompt a stylistic revision, and let the diff engine patch that specific passage in memory while keeping the rest of the manuscript intact.


* **CHAT (Conversational Scratchpad):**
* Retains its clean, lightweight conversational interface for quick technical Q&A, math, and system queries without being tied to an active document or audio buffer.





---

### Immediate Implementation Checklist

1. **Scaffold `DiffEngine.h`:** Write the string search-and-replace algorithm to locate and patch source text using `SEARCH/REPLACE` blocks.
2. **Add `ImGuiColorTextEdit`:** Integrate the editor source files into the Visual Studio solution under the UI filter.


3. **Scaffold Split-Pane in `FREEAI.cpp`:** Divide the `CODING` workspace into a 35% chat inspector and a 65% editor buffer.


4. **Expand Audio Studio Deck:** Implement the `<filesystem>` scanner for `output/music/` and add the vocal directive chip buttons in `RenderMusicStudioWorkspace`.

---

## 📜 License & Acknowledgments

Authored by **Nathaniel Richardson Jr.** Distributed under the MIT License. Special thanks to the open-source communities powering [llama.cpp](https://github.com/ggerganov/llama.cpp), [Dear ImGui](https://github.com/ocornut/imgui), [GLFW](https://www.glfw.org/), and [YuE2](https://www.google.com/search?q=https://github.com/audio-cpp).

```

```
