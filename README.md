```markdown
# ⚡ Repetere AI (beta-0.6b) ⚡

By Nathaniel Richardson Jr.

---

### Compute Sovereignty Restored

**Repetere AI** is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware[cite: 1, 11].

Named after the Latin verb *repetere* ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows[cite: 1, 11].

---

> [!IMPORTANT]
> **Zero Cloud Telemetry:** All inference requests, prompts, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host hardware[cite: 1].

---

## ⚡ System Requirements

| Component | Minimum Specification | Recommended Specification[cite: 1] |
| --- | --- | --- |
| **Operating System** | Windows 10 (64-bit)[cite: 1] | Windows 11 (64-bit)[cite: 1] |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM)[cite: 1] | NVIDIA RTX 40/50-Series (12 GB+ VRAM)[cite: 1] |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+)[cite: 1] | Latest NVIDIA Studio Drivers[cite: 1] |
| **System Memory** | 16 GB Physical RAM[cite: 1] | 32 GB Physical RAM (Required for Hybrid Mode)[cite: 1] |
| **Target Storage** | 20 GB free space on SSD[cite: 1] | 50 GB+ free space on NVMe SSD[cite: 1] |

---

## 🚀 Quick Start: Installation & First Launch

1. Go to the [Releases](https://github.com/securenrn-del/Repetere-AI_Beta/releases) page and download **`RepetereAI-Setup-v0.5.9-beta.exe`**.
2. Run the installer[cite: 12]. It extracts cleanly into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges[cite: 12].
3. Launch **Repetere AI** from your Desktop shortcut or Start Menu.
4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key[cite: 2, 7].
5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM[cite: 7]. Click **Confirm Hardware** to enter the main workstation[cite: 7].

---

## 📦 How to Download & Manage AI Models

AI models are the local weights that power each workspace. They must be downloaded before you can generate code, text, music, or images[cite: 4, 12].

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**[cite: 12].
2. The overlay will display your detected hardware profile and list verified models[cite: 4, 12]:
   * **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B*)[cite: 4]
   * **Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 4]
   * **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 4]
   * **Audio / Music Studio (Both Required):**
     * *YuE2 3B Full Song & Singing Engine* (`yue2-3b-q4_0.gguf`, ~2.48 GB)[cite: 9]
     * *YuE2 Neural Audio VAE Decoder* (`yue2-vae-f16.gguf`, ~265 MB)[cite: 9, 12]
   * **Images Workspace:** *FLUX.1 Schnell Diffusion* (`flux1-schnell-Q4_0.gguf`)[cite: 4]
3. Click **[ Download ]** next to your desired model[cite: 4, 12]. The in-app manager streams chunks via CPR with real-time transfer telemetry and validates the 4-byte GGUF magic header (`0x46554747`)[cite: 4, 5].
4. When finished, the status badge changes to green (**Installed**)[cite: 4, 18]. Click **[ Return to Workspace ]**.

### Option B: Manual File Placement (Advanced)

Place `.gguf` weight files directly into your local application directory[cite: 2, 12]:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

*(Ensure filenames match the catalog schema exactly so dynamic workspace discovery resolves them cleanly).*

---

## 🧭 Workspace User Guide

```text
 ┌────────────────────────────────────────────────────────────────────────┐
 │                        REPETERE AI WORKSPACES                          │
 ├──────────────┬──────────────┬──────────────┬─────────────┬─────────────┤
 │    CODING    │     CHAT     │   CREATIVE   │ AUDIO (YUE) │   IMAGES    │
 │ (Qwen Coder) │ (Llama 3.1)  │  (Hermes 3)  │  (YuE2 3B)  │   (FLUX)    │
 └──────────────┴──────────────┴──────────────┴─────────────┴─────────────┘

```

### 💻 1. CODING

* **Engine Target:** Qwen 2.5 Coder 7B / 14B / 32B Instruct


* **Syntax Extraction:** Automatically formats code blocks (```) inside horizontal-scrolling containers with snippet-level **Copy** buttons.
* **Full Export:** Click **[ Copy Full Response ]** below any message for rapid clipboard export.

### 💬 2. CHAT

* **Engine Target:** Meta Llama 3.1 8B Instruct


* **Context Preservation:** Multi-turn message serialization persists conversation context across sessions.


* **Resetting Context:** Click the red **[ Clear Chat ]** button to archive the active transcript to disk and clear GPU memory.



### 🖋️ 3. CREATIVE WRITING

* **Engine Target:** Hermes 3 Llama 3.1 8B


* **Narrative Drafting:** Uncensored prose generation, scene pacing, and world-building without cloud filtering.



### 🎵 4. AUDIO (MUSIC) Production Studio

* **Engine Target:** YuE2 Neural Audio Synthesis Engine (`yue2-3b-q4_0.gguf` + `yue2-vae-f16.gguf`)


* **Arrangement Controls:**
* **Musical Style & Acoustic Tags:** Enter instruments, tempo, and genre descriptors (e.g., *Alternative Rock, driving drums, distorted drop-D guitar, 105 bpm*).
* **Lyrics Buffer:** Type or paste verses, choruses, and tags (supports up to 8,192 bytes):


```text
[Verse]
Walking down this empty road
[Chorus]
Echoes fade into the night

```


* **Duration:** Set track length via the slider (expandable up to 360 seconds).


* **Generation & Playback:** Click **[ Generate Full Song (With Vocals) ]**. The track renders as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` into `output/music/` and can be played via the integrated Win32 transport monitor.



### 🎨 5. IMAGES (DIFFUSION) Studio

* **Engine Target:** FLUX.1 Schnell (`flux1-schnell-Q4_0.gguf`) / `sd.exe`

* **Controls:** Positive and negative prompt inputs, inference steps (1–50), CFG scale adjustment, and resolution presets.
* **Image-to-Image:** Click **[ Upload Base Image File... ]** to attach reference imagery.
* **Render:** Click **[ Render Image ]** to output renders directly to the canvas viewport and `output/images/`.

---

## ⚙️ Hardware Compute Modes: GPU vs. HYBRID

Located in the top-right header:

* **GPU Mode:** Locks model execution entirely within dedicated GPU VRAM for maximum token throughput and minimum latency.


* **HYBRID Mode:** Prompts an interactive confirmation dialog and spans layers across host RAM and GPU VRAM. This enables 8 GB–12 GB GPUs to run larger 14B–32B parameter models without Out-Of-Memory errors.



---

## 📜 Conversation History & Safety Overlays

* **Local JSON Persistence:** Conversations automatically serialize to `chat_history.json` upon context clear or shutdown.


* **Transcript Viewer:** Navigate to **History ➔ Open History Transcripts** to inspect past sessions by timestamp.


* **Context Restoration:** Single-click **[ Load Conversation into Active Tab ]** to restore past dialogues directly into memory.


* **Wipe Guard:** The **[ Clear All Saved Transcripts ]** action triggers a confirmation modal requiring explicit verification before permanently removing stored logs.



---

## 📋 Comprehensive Changelog

### Version 0.5.9-beta — Modular Workspace Decoupling, Headless Process Supervision & Hardware Gating

```diff
+ Added full translation-unit modular decoupling (HistoryUI, ModelManagerUI, MusicStudioUI, ImageStudioUI)
+ Added dynamic filesystem model discovery (ScanLocalModels) across all workspace screens
+ Added missing-model intercept card directing users to Settings -> Repetere Models on empty tabs
+ Added multi-directory fallback resolution for splashscreen.jpg assets
+ Added explicit fixed-column layout formatting in ModelManagerUI to resolve 28pt HiDPI clipping
+ Added Win32 Job Object containment (JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE) for leak-free child lifecycles
+ Added discrete GPU adapter validation (DXGI polling rejecting APU/iGPU configurations)
+ Added 8,192-byte multiline lyrics and stem input rack with Win32 transport playback
+ Added FLUX.1 Schnell image studio pipeline with auto-unloading VRAM guards
+ Added CPR background chunk streaming with 4-byte GGUF magic header validation (0x46554747)
+ Added one-click copy targets: [Copy Snippet] and [Copy Full Response]
! Fixed subshell cmd.exe argument truncations via quote stripping and newline flattening
! Fixed cold-boot loopback connection drops by polling http://127.0.0.1:8080/health
! Fixed History Overlay escape, close box, and return button dismiss bugs
! Fixed About Us popup modal positioning, repository hyperlink dispatch, and freeze states
! Fixed Image Studio encoder verification to check .safetensors alongside .gguf companions

```

#### 1. Modular Translation Units Decoupling & UI Architecture

* **Split Source Structure:** Deconstructed the monolithic rendering loop from `FREEAI.cpp` into dedicated compilation units: `HistoryUI.h/.cpp`, `ModelManagerUI.h/.cpp`, `MusicStudioUI.h/.cpp`, and `ImageStudioUI.h/.cpp`.


* **Dynamic Model Discovery:** Integrated `ScanLocalModels()` and `FindModelForWorkspace()` into each workspace screen, scanning the `models/` root and subdirectories to bind installed `.gguf` weights dynamically without hardcoded filenames.
* **Missing Weight Intercepts:** Integrated `RenderMissingModelNotice` banners across every workspace screen with direct one-click routing to the Model Downloader when weights are unpopulated.
* **HiDPI Table Layouts:** Corrected column padding and fixed width constraints in `ModelManagerUI.cpp` to prevent text truncation, button clipping, and path wrapping at 28pt Segoe UI scaling.
* **Persistent Modal Navigation:** Fully restored modal close lifecycles for the History viewer, About Repetere AI dialog, and DXGI Hardware Diagnostics overlay, ensuring Escape key, header close, and return-to-workspace actions dismiss cleanly without thread hangs.

#### 2. Embedded Sidecar Architecture & Process Supervisor (`ProcessManager.h`)

* **Win32 Job Object Containment:** Inference sidecars (`llama-server.exe`, `audiocpp_cli.exe`, `sd.exe`) are tethered to an internal Windows Job Object configured with `JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE`, ensuring background sidecars terminate when closing or reloading the client.


* **Headless Background Execution:** Enforced `CREATE_NO_WINDOW` and `SW_HIDE` startup flags, eliminating flashing command-line consoles during model transitions.


* **Active Loopback Health Polling:** Background threads query the local loopback (`[http://127.0.0.1:8080/health](http://127.0.0.1:8080/health)`) using asynchronous CPR ping requests prior to routing prompts, preventing dropped connections during cold starts.


* **Path Resolution:** Implemented relative path binding that locates runtime sidecars across Visual Studio build outputs, root directories, and `bin/` without hardcoded machine paths.


* **Orphaned Process Sweeper:** Integrated `CreateToolhelp32Snapshot` sweeps using `th32ProcessID` to terminate any lingering sidecar binaries on workspace transitions or application shutdown.

#### 3. Hardware-Aware Telemetry & Adapter Gating (`HardwareScanner.h`)

* **DirectX Graphics Infrastructure (DXGI) Polling:** Deep adapter enumeration inspecting dedicated video memory, shared memory, and PCI vendor IDs (`0x10DE` for NVIDIA, `0x1002` for AMD, `0x8086` for Intel).


* **Discrete 4 GB VRAM Gate:** Filters dedicated GPUs with $\ge$ 4,000 MB VRAM, classifying setups into *ENTRY_4GB*, *BASELINE_8GB*, or *PRO_12GB+* tiers.


* **APU & iGPU Segregation:** System scanning identifies integrated chipsets (e.g., AMD Vega/Radeon, Intel Iris/UHD) and dynamically flags systems lacking a discrete GPU with an `INCOMPATIBLE_APU` diagnostic status.


* **Model Target Binding:** Engine recommendations and automatic download targets are strictly coupled to verified discrete NVIDIA accelerators pending alternative runtime backends.
* **Layer Offloading Optimization:** Automatically configures offload layers (`-ngl 99` for dedicated GPU mode; `-ngl 16` to `-ngl 24` for HYBRID memory bridging) to fit target parameters safely.

#### 4. Full 5-Workspace Multimodal Suite (`FREEAI.cpp`, `Types.h`)

* 💻 **`CODING` (Split-View IDE):**
* Configured for software engineering tasks powered by Qwen 2.5 Coder checkpoints (7B, 14B, and 32B Hybrid).


* Custom markdown parser identifies triple-backtick language blocks (```), formatting code in horizontal-scrolling containers with snippet-level copy actions and a single-click `[ Copy Full Response ]` button.


* 💬 **`CHAT` (General Assistant):**
* Conversational scratchpad powered by Meta Llama 3.1 8B Instruct.


* Features multi-turn message serialization, session auto-archiving to disk, and a distinct red `Clear Chat` action protected by context wipe confirmation guards.




* 🖋️ **`CREATIVE WRITING` (Narrative Studio):**
* Long-form narrative story drafting, timeline planning, and world-building powered by Hermes 3 Llama 3.1 8B.


* Retains prose presentation with dedicated transcript logging.




* 🎵 **`AUDIO (MUSIC)` (YuE2 Neural Production Studio):**
* Full vocal and instrumental song generation rack powered by YuE2 3B weights (`yue2-3b-q4_0.gguf` / `yue2-3b-q8_0.gguf`) paired with `yue2-vae-f16.gguf`.


* 8,192-byte multiline lyrics and stem input buffer (`lyricsBuffer`) supporting structured arrangements (`[Verse]`, `[Chorus]`, `[Bridge]`) with configurable generation durations up to 360 seconds.


* Subshell argument sanitization converting double quotes and flattening line breaks to prevent Win32 `cmd.exe` argument chopping.


* Automatic track serialization saving renders as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` in `output/music/`, with asynchronous Win32 transport playback (`PlaySoundA` / `ShellExecuteA`).




* 🎨 **`IMAGES` (Diffusion Studio):**
* Text-to-image and image-to-image workspace utilizing FLUX.1 Schnell (`flux1-schnell-Q4_0.gguf`) and `sd.exe` sidecar integration.


* Verification checks identify companion safetensors (`clip_l.safetensors`, `ae.safetensors`, `t5xxl_q4_k.safetensors`) alongside `.gguf` weights.
* Granular generation controls: dual positive and negative prompt inputs, inference steps (1–50), CFG scale adjustment, resolution presets (`512x512` to `1280x720`), and native reference image importing.
* GPU memory management automatically flushes dormant diffusion workers via `StopDiffusion()` upon tab exit.





#### 5. Integrated Model Downloader & Manager (`ModelDownloader.h/.cpp`)

* ⚡ **Asynchronous CPR Chunking:** Non-blocking background downloads with real-time transfer metrics running on dedicated worker threads to preserve UI framerates.


* 🔄 **HTTP 302/307 Redirect Resilience:** Fully configured follow-redirect flags (`cpr::Redirect{10L, true, true, cpr::PostRedirectFlags::POST_ALL}`) ensuring successful retrieval from Hugging Face CDN and LFS endpoints.
* 🛡️ **Binary Header Validation:** Pre-deployment validation verifying the 4-byte GGUF magic binary header (`0x46554747` / `GGUF`) on incoming `.part` files prior to final deployment in `models/`.


* 📦 **Curated Model Registry:** Direct download entries for verified weights, including Qwen 2.5 Coder (7B, 14B, 32B), Meta Llama 3.1 8B, Hermes 3 8B, YuE2 Audio (weights + VAE), and FLUX.1 Schnell.


* 🎛️ **In-App Management Overlay (`Settings -> Repetere Models`):** Full-screen overlay displaying hardware diagnostics, disk model status, and dynamic `[Set Active]` model hot-swapping controls.



#### 6. Local JSON History Persistence (`HistoryManager.h/.cpp`)

* 💾 **Direct Serialization:** Conversation history serializes safely to `chat_history.json` on application shutdown or context reset without external third-party JSON parser overhead.


* 🔣 **Character Escaping:** Hand-crafted escaping routines sanitize quotes, tabs, and newlines to preserve syntax blocks across reloads.


* 📖 **Transcript Viewer:** Accessible via `History -> Open History Transcripts` featuring explicit foreground z-index prioritization (`ImGui::SetNextWindowFocus()`) and one-click context re-injection (`[ Load Conversation into Active Tab ]`).


* 🛑 **Accidental Wipe Protection:** Red confirmation modals intercept transcript deletion requests to prevent data loss.



---

## 🛠️ System Overview & Active Architecture

| Architectural Layer | Implementation Details |
| --- | --- |
| **UI & Viewport Engine** | [Dear ImGui](https://github.com/ocornut/imgui) + [GLFW](https://www.glfw.org/) + OpenGL 3 (GLSL `#version 130`) rendering in an auto-maximizing 1600p+ desktop viewport with 1.15× scaling and 28pt Segoe UI typography.

 |
| **Styling & Assets** | Custom slate dark theme palette, custom application taskbar/window icons via `stb_image`, and a full-viewport startup splash screen (`splashscreen.jpg`) with dismiss on click or keypress.

 |
| **Hardware Diagnostics** | Direct DirectX Graphics Infrastructure (DXGI) and Windows memory scanner querying dedicated VRAM and host RAM on startup to profile the machine and assign optimal model quantization targets.

 |
| **Asynchronous Pipeline** | Detached background worker threads (`std::thread`) decouple inference requests from the UI loop to prevent frame stalling, synchronized safely via `std::mutex`.

 |
| **Process Lifecycles** | Native Win32 child process supervisor managing `llama-server.exe`, `audiocpp_cli.exe`, and `sd.exe` over loopback port `8080` with Job Object lifecycle containment.

 |
| **Model Distribution** | Native CPR-based chunk streaming engine with resume support, live transfer telemetry, and automated 4-byte GGUF magic header validation (`0x46554747`).

 |

---

## 📂 Modular Codebase Layout

```text
RepetereAI/
├── 📁 bin/                         # Native inference sidecars (llama-server.exe, sd.exe, CUDA DLLs)
│   └── 📁 audio/                   # Neural audio sidecar (audiocpp_cli.exe, isolated runtime DLLs)
├── 📁 models/                      # Target directory for downloaded .gguf weights and VAEs
│   └── 📁 sidecars/                # YuE2 JSON configs & Qwen BPE tokenizer (yue2-qwen.tiktoken)
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
│   ├── 📄 HistoryUI.h/.cpp         # Modular transcript viewer, session restoration, and deletion modals
│   ├── 📄 ModelManagerUI.h/.cpp    # Hardware telemetry split-view, GGUF catalog downloads, and hot-swap table
│   ├── 📄 MusicStudioUI.h/.cpp     # Neural audio generation workspace, lyrics rack, and Win32 playback transport
│   ├── 📄 ImageStudioUI.h/.cpp     # FLUX.1 diffusion workspace, reference image loader, and canvas viewport
│   └── 📄 FREEAI.cpp               # Entry point, GLFW/OpenGL loop, splash screen, top menu bar, and workspace routing
├── 📄 .gitignore                   # Excludes .vs/, x64/, Debug/, Release/, *.zip, and local build binaries
├── 📄 chat_history.json            # Local serialized conversation transcript database
├── 📄 FREEAI.slnx                  # XML-based Visual Studio Solution
└── 🖼️ splashscreen.jpg             # Startup graphic and window icon asset

```

---

## 🗺️ Development Roadmap

* [x] Native Dear ImGui + GLFW + OpenGL3 window and custom dark styling.


* [x] Asynchronous CPR inference threading with mutex synchronization.


* [x] Markdown code block extraction with clipboard copy actions.
* [x] GPU vs. HYBRID memory mode toggle and warning dialogs.


* [x] Local JSON conversation history viewer and management.


* [x] Startup DXGI VRAM and system memory scanner modal.


* [x] Integrated in-app GGUF model downloader with header validation.


* [x] Full 5-workspace multimodal suite (**Coding**, **Chat**, **Creative Writing**, **Audio Music**, **Images**).


* [x] Dynamic sidecar process lifecycle management and VRAM hot-swapping on port 8080.


* [x] Standalone 1-Click Setup executable packaging via Inno Setup.


* [x] Modular workspace translation units decoupling (`ChatUI`, `HistoryUI`, `ModelManagerUI`, `MusicStudioUI`, `ImageStudioUI`).
* [ ] Native Vulkan / DirectML backend compute toggles for non-NVIDIA GPUs.
* [ ] Peer-to-Peer Mesh (Repetere Grid): Time-banking barter economy to pool idle GPU cycles across nodes without cryptocurrency.
* [ ] Encrypted Remote Mobile Client: WebRTC/STUN hole-punching and QR pairing to control the home desktop server from an Android companion app.

---

## 📜 License & Acknowledgments

Engineered by Nathaniel Richardson Jr. as part of the Repetere AI compute initiative. Distributed under the MIT License. Special thanks to the open-source contributors behind `llama.cpp`, `Dear ImGui`, `GLFW`, and `YuE2`.

```

```
