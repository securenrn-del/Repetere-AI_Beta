⚡ Repetere AI (beta-0.5.9) ⚡

By Nathaniel Richardson

Compute Sovereignty Restored
Repetere AI is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware.

Named after the Latin verb repetere ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows.

[!IMPORTANT]
Zero Cloud Telemetry: All inference requests, prompts, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host hardware.

📋 Comprehensive Changelog
Version 0.5.9-beta — Modular Workspace Decoupling, Headless Process Supervision & Hardware Gating
Version 0.5.9-beta refactors Repetere AI into isolated UI translation units while maintaining build stability. It introduces headless process supervision via native Win32 Job Objects, hardware-aware adapter gating (restricting model targets to eligible discrete NVIDIA accelerators while warning APU-only machines), silent model switching, and stabilizes the multimodal pipeline across all five state-isolated production environments.

Diff
+ Added Win32 Job Object containment (JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE) for leak-free child lifecycles
+ Added discrete GPU adapter validation (DXGI polling rejecting APU/iGPU configurations)
+ Added 8,192-byte multiline lyrics and stem input rack with Win32 transport playback
+ Added FLUX.1 Schnell image studio pipeline with auto-unloading VRAM guards
+ Added CPR background chunk streaming with 4-byte GGUF magic header validation (0x46554747)
+ Added one-click copy targets: [Copy Snippet] and [Copy Full Response]
! Fixed subshell cmd.exe argument truncations via quote stripping and newline flattening
! Fixed cold-boot loopback connection drops by polling http://127.0.0.1:8080/health
1. Embedded Sidecar Architecture & Process Supervisor (ProcessManager.h)
Win32 Job Object Containment Inference sidecars (llama-server.exe, audiocpp_cli.exe, sd.exe) are tethered to an internal Windows Job Object configured with JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE, ensuring background sidecars terminate when closing or reloading the client.

Headless Background Execution Enforced CREATE_NO_WINDOW and SW_HIDE startup flags, eliminating flashing command-line consoles during model transitions.

Active Loopback Health Polling Background threads query the local loopback ([http://127.0.0.1:8080/health](http://127.0.0.1:8080/health)) using asynchronous CPR ping requests prior to routing prompts, preventing dropped connections during cold starts.

Path Resolution Implemented relative path binding that locates runtime sidecars across Visual Studio build outputs, root directories, and bin/ without hardcoded machine paths.

Orphaned Process Sweeper Integrated CreateToolhelp32Snapshot sweeps using th32ProcessID to terminate any lingering sidecar binaries on workspace transitions or application shutdown.

2. Hardware-Aware Telemetry & Adapter Gating (HardwareScanner.h)
DirectX Graphics Infrastructure (DXGI) Polling Deep adapter enumeration inspecting dedicated video memory, shared memory, and PCI vendor IDs (0x10DE for NVIDIA, 0x1002 for AMD, 0x8086 for Intel).

Discrete 4 GB VRAM Gate Filters dedicated GPUs with 
≥ 4,000 MB VRAM, classifying setups into ENTRY_4GB, BASELINE_8GB, or PRO_12GB+ tiers.

APU & iGPU Segregation System scanning identifies integrated chipsets (e.g., AMD Vega/Radeon, Intel Iris/UHD) and dynamically flags systems lacking a discrete GPU with an INCOMPATIBLE_APU diagnostic status.

Model Target Binding Engine recommendations and automatic download targets are strictly coupled to verified discrete NVIDIA accelerators pending alternative runtime backends.

Layer Offloading Optimization Automatically configures offload layers (-ngl 99 for dedicated GPU mode; -ngl 16 to -ngl 24 for HYBRID memory bridging) to fit target parameters safely.

3. Full 5-Workspace Multimodal Suite (FREEAI.cpp, Types.h)
Plaintext
 ┌────────────────────────────────────────────────────────────────────────┐
 │                      REPETERE AI WORKSPACES                            │
 ├──────────────┬──────────────┬──────────────┬─────────────┬─────────────┤
 │    CODING    │     CHAT     │   CREATIVE   │ AUDIO (YUE) │   IMAGES    │
 │ (Qwen Coder) │ (Llama 3.1)  │  (Hermes 3)  │  (YuE2 3B)  │   (FLUX)    │
 └──────────────┴──────────────┴──────────────┴─────────────┴─────────────┘
💻 CODING (Split-View IDE):

Configured for software engineering tasks powered by Qwen 2.5 Coder checkpoints (7B, 14B, and 32B Hybrid).

Custom markdown parser identifies triple-backtick language blocks (```), formatting code in horizontal-scrolling containers with snippet-level copy actions and a single-click [ Copy Full Response ] button.

💬 CHAT (General Assistant):

Conversational scratchpad powered by Meta Llama 3.1 8B Instruct.

Features multi-turn message serialization, session auto-archiving to disk, and a distinct red Clear Chat action protected by context wipe confirmation guards.

🖋️ CREATIVE WRITING (Narrative Studio):

Long-form narrative story drafting, timeline planning, and world-building powered by Hermes 3 Llama 3.1 8B.

Retains prose presentation with dedicated transcript logging.

🎵 AUDIO (MUSIC) (YuE2 Neural Production Studio):

Full vocal and instrumental song generation rack powered by YuE2 3B weights (yue2-3b-q4_0.gguf / yue2-3b-q8_0.gguf) paired with yue2-vae-f16.gguf.

8,192-byte multiline lyrics and stem input buffer (lyricsBuffer) supporting structured arrangements ([Verse], [Chorus], [Bridge]) with configurable generation durations up to 300+ seconds.

Subshell argument sanitization converting double quotes and flattening line breaks to prevent Win32 cmd.exe argument chopping.

Automatic track serialization saving renders as [StyleTag]_[Word1]_[Word2]_[Timestamp].wav in output/music/, with asynchronous Win32 transport playback (PlaySoundA / ShellExecuteA).

🎨 IMAGES (Diffusion Studio):

Text-to-image and image-to-image workspace utilizing FLUX.1 Schnell (flux1-schnell-q4_k_m.gguf) and sd.exe sidecar integration.

Granular generation controls: dual positive and negative prompt inputs, inference steps (1–50), CFG scale adjustment, resolution presets (512x512 to 1280x720), and native reference image importing.

GPU memory management automatically flushes dormant diffusion workers via StopDiffusion() upon tab exit.

4. Integrated Model Downloader & Manager (ModelDownloader.h/.cpp)
⚡ Asynchronous CPR Chunking: Non-blocking background downloads with real-time transfer metrics (MB downloaded, total size, percentage progress bar) running on dedicated worker threads to preserve UI framerates.

🔄 HTTP 302/307 Redirect Resilience: Fully configured follow-redirect flags (cpr::Redirect{10L, true, true, cpr::PostRedirectFlags::POST_ALL}) ensuring successful retrieval from Hugging Face CDN and LFS endpoints.

🛡️ Binary Header Validation: Pre-deployment validation verifying the 4-byte GGUF magic binary header (0x46554747 / GGUF) on incoming .part files prior to final deployment in models/.

📦 Curated Model Registry: Direct download entries for verified weights, including Qwen 2.5 Coder (7B, 14B, 32B), Meta Llama 3.1 8B, Hermes 3 8B, YuE2 Audio (weights + VAE), and FLUX.1 Schnell.

🎛️ In-App Management Overlay (Settings -> Repetere Models): Full-screen overlay displaying hardware diagnostics, disk model status, and dynamic [Set Active] model hot-swapping controls.

5. Local JSON History Persistence (HistoryManager.h/.cpp)
💾 Direct Serialization: Conversation history serializes safely to chat_history.json on application shutdown or context reset without external third-party JSON parser overhead.

🔣 Character Escaping: Hand-crafted escaping routines sanitize quotes, tabs, and newlines to preserve syntax blocks across reloads.

📖 Transcript Viewer: Accessible via History -> Open History Transcripts featuring explicit foreground z-index prioritization (ImGui::SetNextWindowFocus()) and one-click context re-injection ([ Load Conversation into Active Tab ]).

🛑 Accidental Wipe Protection: Red confirmation modals intercept transcript deletion requests to prevent data loss.

🛠️ System Overview & Active Architecture
Architectural Layer	Implementation Details
UI & Viewport Engine	Dear ImGui + GLFW + OpenGL 3 (GLSL #version 130) rendering in an auto-maximizing 1600p+ desktop viewport with 1.15× scaling and 28pt Segoe UI typography.
Styling & Assets	Custom slate dark theme palette, custom application taskbar/window icons via stb_image, and a full-viewport startup splash screen (splashscreen.jpg) with dismiss on click or keypress.
Hardware Diagnostics	Direct DirectX Graphics Infrastructure (DXGI) and Windows memory scanner querying dedicated VRAM and host RAM on startup to profile the machine and assign optimal model quantization targets.
Asynchronous Pipeline	Detached background worker threads (std::thread) decouple inference requests from the UI loop to prevent frame stalling, synchronized safely via std::mutex.
Process Lifecycles	Native Win32 child process supervisor managing llama-server.exe, audiocpp_cli.exe, and sd.exe over loopback port 8080 with Job Object lifecycle containment.
Model Distribution	Native CPR-based chunk streaming engine with resume support, live transfer telemetry, and automated 4-byte GGUF magic header validation (0x46554747).
📂 Modular Codebase Layout
Plaintext
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
⚡ Building and Running
System Requirements
Component	Minimum Specification	Recommended Specification[cite: 1]
Operating System	Windows 10 (64-bit)[cite: 1]	Windows 11 (64-bit)[cite: 1]
GPU Acceleration	NVIDIA RTX 30-Series (8 GB VRAM)[cite: 1]	NVIDIA RTX 40/50-Series (12 GB+ VRAM)[cite: 1]
Display Drivers	NVIDIA Game Ready / Studio 528+ (CUDA 12+)[cite: 1]	Latest NVIDIA Studio Drivers[cite: 1]
System Memory	16 GB Physical RAM[cite: 1]	32 GB Physical RAM (Required for Hybrid Mode)[cite: 1]
Target Storage	20 GB free space on SSD[cite: 1]	50 GB+ free space on NVMe SSD[cite: 1]
Build Pipeline
Clone the Repository:

Bash
git clone [https://github.com/securenrn-del/Repetere-AI_Beta.git](https://github.com/securenrn-del/Repetere-AI_Beta.git)
cd Repetere-AI_Beta
Install Dependencies via vcpkg:

Bash
vcpkg install cpr:x64-windows glfw3:x64-windows imgui[glfw-binding,opengl3-binding]:x64-windows
Compile in Visual Studio 2022:

Open FREEAI.slnx.

Set configuration to Release | x64.

Verify link dependencies: dxgi.lib, winmm.lib, ws2_32.lib.

Press Ctrl + Shift + B to compile[cite: 1, 2].

Launch Application:

Press F5 to launch the workstation[cite: 1, 2].
