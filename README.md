# ⚡ Repetere AI (beta-0.5.9) ⚡



By Nathaniel Richardson Jr.

---

### Compute Sovereignty Restored

**Repetere AI** is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware.

Named after the Latin verb *repetere* ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows.

---

> [!IMPORTANT]
> **Zero Cloud Telemetry:** All inference requests, prompts, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host hardware.

---

## ⚡ System Requirements

| Component | Minimum Specification | Recommended Specification |
| --- | --- | --- |
| **Operating System** | Windows 10 (64-bit) | Windows 11 (64-bit) |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM) | NVIDIA RTX 40/50-Series (12 GB+ VRAM) |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+) | Latest NVIDIA Studio Drivers |
| **System Memory** | 16 GB Physical RAM | 32 GB Physical RAM (Required for Hybrid Mode) |
| **Target Storage** | 20 GB free space on SSD | 50 GB+ free space on NVMe SSD |

---

## 🚀 Quick Start: Installation & First Launch

1. Go to the [Releases](https://www.google.com/search?q=https://github.com/securenrn-del/Repetere-AI_Beta/releases) page and download **`RepetereAI-Setup-v0.5.9-beta.exe`**.
2. Run the installer[cite: 12]. It extracts cleanly into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges[cite: 12].
3. Launch **Repetere AI** from your Desktop shortcut or Start Menu.
4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key[cite: 2, 7, 28].
5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM[cite: 7, 28]. Click **Confirm Hardware** to enter the main workstation[cite: 7, 20].

---

## 📦 How to Download & Manage AI Models

AI models are the local weights that power each workspace. They must be downloaded before you can generate code, text, music, or images[cite: 4, 12].

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**[cite: 12].
2. The overlay will display your detected hardware profile and list verified models[cite: 4, 12]:
* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B*)[cite: 4, 26]
* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 4, 26]
* **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 4, 26]
* **Audio / Music Studio (Both Required):**
* *YuE2 3B Full Song & Singing Engine* (`yue2-3b-q4_0.gguf`, ~2.48 GB)[cite: 9, 26]
* *YuE2 Neural Audio VAE Decoder* (`yue2-vae-f16.gguf`, ~265 MB)[cite: 9, 12, 26]


* **Images Workspace:** *FLUX.1 Schnell Diffusion* (`flux1-schnell-Q4_0.gguf`)[cite: 4, 26]


3. Click **[ Download ]** next to your desired model[cite: 4, 12]. The in-app manager streams chunks via CPR with real-time transfer telemetry and validates the 4-byte GGUF magic header (`0x46554747`)[cite: 4, 5, 26].
4. When finished, the status badge changes to green (**Installed**)[cite: 4, 18, 24]. Click **[ Return to Workspace ]**.

### Option B: Manual File Placement (Advanced)

Place `.gguf` weight files directly into your local application directory[cite: 2, 12]:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

*(Ensure filenames match the catalog schema exactly so the engine resolves them cleanly).*

---

## 🧭 Workspace User Guide

```text
 ┌────────────────────────────────────────────────────────────────────────┐
 │                      REPETERE AI WORKSPACES                            │
 ├──────────────┬──────────────┬──────────────┬─────────────┬─────────────┤
 │    CODING    │     CHAT     │   CREATIVE   │ AUDIO (YUE) │   IMAGES    │
 │ (Qwen Coder) │ (Llama 3.1)  │  (Hermes 3)  │  (YuE2 3B)  │   (FLUX)    │
 └──────────────┴──────────────┴──────────────┴─────────────┴─────────────┘

```

### 💻 1. CODING

* **Engine Target:** Qwen 2.5 Coder 7B / 14B / 32B Instruct[cite: 4, 26]
* **Syntax Extraction:** Automatically formats code blocks (```) inside horizontal-scrolling containers with snippet-level **Copy** buttons.
* **Full Export:** Click **[ Copy Full Response ]** below any message for rapid clipboard export.

### 💬 2. CHAT

* **Engine Target:** Meta Llama 3.1 8B Instruct[cite: 4, 26]
* **Context Preservation:** Multi-turn message serialization persists conversation context across sessions[cite: 1, 31].
* **Resetting Context:** Click the red **[ Clear Chat ]** button to archive the active transcript to disk and clear GPU memory[cite: 1, 10].

### 🖋️ 3. CREATIVE WRITING

* **Engine Target:** Hermes 3 Llama 3.1 8B[cite: 3, 4, 26]
* **Narrative Drafting:** Uncensored prose generation, scene pacing, and world-building without cloud filtering[cite: 3].

### 🎵 4. AUDIO (MUSIC) Production Studio

* **Engine Target:** YuE2 Neural Audio Synthesis Engine (`yue2-3b-q4_0.gguf` + `yue2-vae-f16.gguf`)[cite: 9, 26]
* **Arrangement Controls:**
* **Musical Style & Acoustic Tags:** Enter instruments, tempo, and genre descriptors (e.g., *Alternative Rock, driving drums, distorted drop-D guitar, 105 bpm*).
* **Lyrics Buffer:** Type or paste verses, choruses, and tags (supports up to 8,192 bytes)[cite: 13, 20, 31]:
```text
[Verse]
Walking down this empty road
[Chorus]
Echoes fade into the night

```


* **Duration:** Set track length via the slider (expandable up to 300+ seconds)[cite: 13, 32].


* **Generation & Playback:** Click **[ Generate Full Song (With Vocals) ]**[cite: 9, 17]. The track renders as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` into `output/music/` and can be played via the integrated Win32 transport monitor[cite: 13, 17, 32].

### 🎨 5. IMAGES (DIFFUSION) Studio

* **Engine Target:** FLUX.1 Schnell (`flux1-schnell-Q4_0.gguf`) / `sd.exe`[cite: 4, 22, 26]
* **Controls:** Positive and negative prompt inputs, inference steps (1–50), CFG scale adjustment, and resolution presets[cite: 22].
* **Image-to-Image:** Click **[ Upload Base Image File... ]** to attach reference imagery[cite: 22].
* **Render:** Click **[ Render Image ]** to output renders directly to the canvas viewport and `output/images/`[cite: 22, 30].

---

## ⚙️ Hardware Compute Modes: GPU vs. HYBRID

Located in the top-right header[cite: 7, 20]:

* **GPU Mode:** Locks model execution entirely within dedicated GPU VRAM for maximum token throughput and minimum latency[cite: 4, 26].
* **HYBRID Mode:** Prompts an interactive confirmation dialog and spans layers across host RAM and GPU VRAM[cite: 4, 26]. This enables 8 GB–12 GB GPUs to run larger 14B–32B parameter models without Out-Of-Memory errors[cite: 4, 26].

---

## 📜 Conversation History & Safety Overlays

* **Local JSON Persistence:** Conversations automatically serialize to `chat_history.json` upon context clear or shutdown[cite: 1, 10, 15].
* **Transcript Viewer:** Navigate to **History ➔ Open History Transcripts** to inspect past sessions by timestamp[cite: 10].
* **Context Restoration:** Single-click **[ Load Conversation into Active Tab ]** to restore past dialogues directly into memory[cite: 7, 10, 32].
* **Wipe Guard:** The **[ Clear All Saved Transcripts ]** action triggers a confirmation modal requiring explicit verification before permanently removing stored logs[cite: 7, 10, 13].

---

## 📋 Comprehensive Changelog

### Version 0.5.9-beta — Modular Workspace Decoupling, Headless Process Supervision & Hardware Gating

```diff
+ Added Win32 Job Object containment (JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE) for leak-free child lifecycles
+ Added discrete GPU adapter validation (DXGI polling rejecting APU/iGPU configurations)
+ Added 8,192-byte multiline lyrics and stem input rack with Win32 transport playback
+ Added FLUX.1 Schnell image studio pipeline with auto-unloading VRAM guards
+ Added CPR background chunk streaming with 4-byte GGUF magic header validation (0x46554747)
+ Added one-click copy targets: [Copy Snippet] and [Copy Full Response]
! Fixed subshell cmd.exe argument truncations via quote stripping and newline flattening
! Fixed cold-boot loopback connection drops by polling [http://127.0.0.1:8080/health](http://127.0.0.1:8080/health)

```

#### 1. Embedded Sidecar Architecture & Process Supervisor (`ProcessManager.h`)

* Win32 Job Object Containment Inference sidecars (`llama-server.exe`, `audiocpp_cli.exe`, `sd.exe`) are tethered to an internal Windows Job Object configured with `JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE`, ensuring background sidecars terminate when closing or reloading the client[cite: 12].
* Headless Background Execution Enforced `CREATE_NO_WINDOW` and `SW_HIDE` startup flags, eliminating flashing command-line consoles during model transitions[cite: 16].
* Active Loopback Health Polling Background threads query the local loopback (`http://127.0.0.1:8080/health`) using asynchronous CPR ping requests prior to routing prompts, preventing dropped connections during cold starts[cite: 8].
* Path Resolution Implemented relative path binding that locates runtime sidecars across Visual Studio build outputs, root directories, and `bin/` without hardcoded machine paths[cite: 2, 4, 17].
* Orphaned Process Sweeper Integrated `CreateToolhelp32Snapshot` sweeps using `th32ProcessID` to terminate any lingering sidecar binaries on workspace transitions or application shutdown.

#### 2. Hardware-Aware Telemetry & Adapter Gating (`HardwareScanner.h`)

* DirectX Graphics Infrastructure (DXGI) Polling Deep adapter enumeration inspecting dedicated video memory, shared memory, and PCI vendor IDs (`0x10DE` for NVIDIA, `0x1002` for AMD, `0x8086` for Intel)[cite: 4].
* Discrete 4 GB VRAM Gate Filters dedicated GPUs with $\ge$ 4,000 MB VRAM, classifying setups into *ENTRY_4GB*, *BASELINE_8GB*, or *PRO_12GB+* tiers[cite: 4].
* APU & iGPU Segregation System scanning identifies integrated chipsets (e.g., AMD Vega/Radeon, Intel Iris/UHD) and dynamically flags systems lacking a discrete GPU with an `INCOMPATIBLE_APU` diagnostic status[cite: 13, 20].
* Model Target Binding Engine recommendations and automatic download targets are strictly coupled to verified discrete NVIDIA accelerators pending alternative runtime backends[cite: 20].
* Layer Offloading Optimization Automatically configures offload layers (`-ngl 99` for dedicated GPU mode; `-ngl 16` to `-ngl 24` for HYBRID memory bridging) to fit target parameters safely.

#### 3. Full 5-Workspace Multimodal Suite (`FREEAI.cpp`, `Types.h`)

* 💻 **`CODING` (Split-View IDE):**
* Configured for software engineering tasks powered by Qwen 2.5 Coder checkpoints (7B, 14B, and 32B Hybrid)[cite: 4, 26].
* Custom markdown parser identifies triple-backtick language blocks (```), formatting code in horizontal-scrolling containers with snippet-level copy actions and a single-click `[ Copy Full Response ]` button.


* 💬 **`CHAT` (General Assistant):**
* Conversational scratchpad powered by Meta Llama 3.1 8B Instruct[cite: 4, 26].
* Features multi-turn message serialization, session auto-archiving to disk, and a distinct red `Clear Chat` action protected by context wipe confirmation guards[cite: 1, 10].


* 🖋️ **`CREATIVE WRITING` (Narrative Studio):**
* Long-form narrative story drafting, timeline planning, and world-building powered by Hermes 3 Llama 3.1 8B[cite: 3, 4, 26].
* Retains prose presentation with dedicated transcript logging[cite: 1].


* 🎵 **`AUDIO (MUSIC)` (YuE2 Neural Production Studio):**
* Full vocal and instrumental song generation rack powered by YuE2 3B weights (`yue2-3b-q4_0.gguf` / `yue2-3b-q8_0.gguf`) paired with `yue2-vae-f16.gguf`[cite: 9, 26, 31].
* 8,192-byte multiline lyrics and stem input buffer (`lyricsBuffer`) supporting structured arrangements (`[Verse]`, `[Chorus]`, `[Bridge]`) with configurable generation durations up to 300+ seconds[cite: 13, 20, 31].
* Subshell argument sanitization converting double quotes and flattening line breaks to prevent Win32 `cmd.exe` argument chopping[cite: 7].
* Automatic track serialization saving renders as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` in `output/music/`, with asynchronous Win32 transport playback (`PlaySoundA` / `ShellExecuteA`)[cite: 13, 17, 32].


* 🎨 **`IMAGES` (Diffusion Studio):**
* Text-to-image and image-to-image workspace utilizing FLUX.1 Schnell (`flux1-schnell-Q4_0.gguf`) and `sd.exe` sidecar integration[cite: 4, 22, 26].
* Granular generation controls: dual positive and negative prompt inputs, inference steps (1–50), CFG scale adjustment, resolution presets (`512x512` to `1280x720`), and native reference image importing[cite: 22].
* GPU memory management automatically flushes dormant diffusion workers via `StopDiffusion()` upon tab exit[cite: 19].



#### 4. Integrated Model Downloader & Manager (`ModelDownloader.h/.cpp`)

* ⚡ **Asynchronous CPR Chunking:** Non-blocking background downloads with real-time transfer metrics running on dedicated worker threads to preserve UI framerates[cite: 4, 18, 24].
* 🔄 **HTTP 302/307 Redirect Resilience:** Fully configured follow-redirect flags (`cpr::Redirect{10L, true, true, cpr::PostRedirectFlags::POST_ALL}`) ensuring successful retrieval from Hugging Face CDN and LFS endpoints[cite: 24, 27].
* 🛡️ **Binary Header Validation:** Pre-deployment validation verifying the 4-byte GGUF magic binary header (`0x46554747` / `GGUF`) on incoming `.part` files prior to final deployment in `models/`[cite: 4, 5, 26].
* 📦 **Curated Model Registry:** Direct download entries for verified weights, including Qwen 2.5 Coder (7B, 14B, 32B), Meta Llama 3.1 8B, Hermes 3 8B, YuE2 Audio (weights + VAE), and FLUX.1 Schnell[cite: 4, 26].
* 🎛️ **In-App Management Overlay (`Settings -> Repetere Models`):** Full-screen overlay displaying hardware diagnostics, disk model status, and dynamic `[Set Active]` model hot-swapping controls[cite: 4, 16].

#### 5. Local JSON History Persistence (`HistoryManager.h/.cpp`)

* 💾 **Direct Serialization:** Conversation history serializes safely to `chat_history.json` on application shutdown or context reset without external third-party JSON parser overhead[cite: 1, 10, 15].
* 🔣 **Character Escaping:** Hand-crafted escaping routines sanitize quotes, tabs, and newlines to preserve syntax blocks across reloads[cite: 1].
* 📖 **Transcript Viewer:** Accessible via `History -> Open History Transcripts` featuring explicit foreground z-index prioritization (`ImGui::SetNextWindowFocus()`) and one-click context re-injection (`[ Load Conversation into Active Tab ]`)[cite: 10, 31, 32].
* 🛑 **Accidental Wipe Protection:** Red confirmation modals intercept transcript deletion requests to prevent data loss[cite: 7, 10, 13].

---

## 🛠️ System Overview & Active Architecture

| Architectural Layer | Implementation Details |
| --- | --- |
| **UI & Viewport Engine** | [Dear ImGui](https://github.com/ocornut/imgui) + [GLFW](https://www.glfw.org/) + OpenGL 3 (GLSL `#version 130`) rendering in an auto-maximizing 1600p+ desktop viewport with 1.15× scaling and 28pt Segoe UI typography[cite: 7, 13, 20]. |
| **Styling & Assets** | Custom slate dark theme palette, custom application taskbar/window icons via `stb_image`, and a full-viewport startup splash screen (`splashscreen.jpg`) with dismiss on click or keypress[cite: 7, 14, 20]. |
| **Hardware Diagnostics** | Direct DirectX Graphics Infrastructure (DXGI) and Windows memory scanner querying dedicated VRAM and host RAM on startup to profile the machine and assign optimal model quantization targets[cite: 4, 7, 20]. |
| **Asynchronous Pipeline** | Detached background worker threads (`std::thread`) decouple inference requests from the UI loop to prevent frame stalling, synchronized safely via `std::mutex`[cite: 4, 18, 24]. |
| **Process Lifecycles** | Native Win32 child process supervisor managing `llama-server.exe`, `audiocpp_cli.exe`, and `sd.exe` over loopback port `8080` with Job Object lifecycle containment[cite: 12]. |
| **Model Distribution** | Native CPR-based chunk streaming engine with resume support, live transfer telemetry, and automated 4-byte GGUF magic header validation (`0x46554747`)[cite: 4, 5, 26]. |

---

## 📂 Modular Codebase Layout

```text
RepetereAI/
├── 📁 bin/                         # Native inference sidecars (llama-server.exe, sd.exe, CUDA DLLs)
│   └── 📁 audio/                   # Neural audio sidecar (audiocpp_cli.exe, isolated runtime DLLs)
├── 📁 models/                      # Target directory for downloaded .gguf weights and VAEs
├── 📁 output/                      # Generated multimodal artifacts
│   ├── 📁 images/                  # Output directory for diffusion renders
│   └── 📁 music/                   # Output directory for synthesized WAV tracks
├── 📁 freeai/
│   ├── 📄 Types.h                  # Core structures: ChatSessionState, ImageStudioState, MusicStudioState, HardwareProfile
│   ├── 📄 HardwareScanner.h        # DXGI & Win32 memory querying engine, VRAM tier routing, APU gating
│   ├── 📄 ProcessManager.h         # Win32 child process supervisor (Job Objects, headless flags, health checks)
│   ├── 📄 ModelDownloader.h/.cpp   # Asynchronous CPR chunked model downloader with GGUF header validation
│   ├── 📄 InferenceClient.h/.cpp   # Detached asynchronous CPR REST worker pipeline for chat completions
│   ├── 📄 HistoryManager.h/.cpp    # JSON escaping, serialization, and chat_history.json disk persistence
│   ├── 📄 Theme.h/.cpp             # OpenGL texture loading (stb_image), window icons, dark slate palette
│   ├── 📄 ChatUI.h/.cpp            # Code block syntax extractor, clipboard copy actions, and chat workspace layout
│   └── 📄 FREEAI.cpp               # Entry point, GLFW/OpenGL loop, splash screen, top menu bar, and workspace tabs
├── 📄 .gitignore                   # Excludes .vs/, x64/, Debug/, Release/, *.zip, and local build binaries
├── 📄 chat_history.json            # Local serialized conversation transcript database
├── 📄 FREEAI.slnx                  # XML-based Visual Studio Solution
└── 🖼️ splashscreen.jpg             # Startup graphic and window icon asset

```

---

## 🗺️ Development Roadmap

* [x] Native Dear ImGui + GLFW + OpenGL3 window and custom dark styling[cite: 7, 20].
* [x] Asynchronous CPR inference threading with mutex synchronization[cite: 4, 18, 24].
* [x] Markdown code block extraction with clipboard copy actions.
* [x] GPU vs. HYBRID memory mode toggle and warning dialogs[cite: 7, 20].
* [x] Local JSON conversation history viewer and management[cite: 1, 10, 15].
* [x] Startup DXGI VRAM and system memory scanner modal[cite: 4, 7, 20].
* [x] Integrated in-app GGUF model downloader with header validation[cite: 4, 5, 26].
* [x] Full 5-workspace multimodal suite (**Coding**, **Chat**, **Creative Writing**, **Audio Music**, **Images**)[cite: 7, 10, 20].
* [x] Dynamic sidecar process lifecycle management and VRAM hot-swapping on port 8080[cite: 4, 7, 16].
* [x] Standalone 1-Click Setup executable packaging via Inno Setup[cite: 12].
* [ ] Modular workspace translation units decoupling (`CodingUI`, `MusicStudioUI`, `ImageStudioUI`, `ModelManagerUI`).
* [ ] Native Vulkan / DirectML backend compute toggles for non-NVIDIA GPUs.
* [ ] Peer-to-Peer Mesh (Repetere Grid): Time-banking barter economy to pool idle GPU cycles across nodes without cryptocurrency.
* [ ] Encrypted Remote Mobile Client: WebRTC/STUN hole-punching and QR pairing to control the home desktop server from an Android companion app.

---

## 📜 License & Acknowledgments

Engineered by Nathaniel Richardson Jr. as part of the Repetere AI compute initiative. Distributed under the MIT License. Special thanks to the open-source contributors behind `llama.cpp`, `Dear ImGui`, `GLFW`, and `YuE2`.
