# Repetere AI (v0.5-beta)

**Author:** Nathaniel Richardson Jr.

**Distribution:** Standalone 1-Click Setup (`RepetereAI-Setup-v0.5-beta.exe`) via [GitHub Releases](https://www.google.com/search?q=https://github.com/securenrn-del/repetereai/releases)[cite: 5, 6, 7]

Repetere AI is a native Windows C++ multimodal desktop workstation engineered to restore computing sovereignty. Built directly on low-level Win32, Dear ImGui, GLFW, and OpenGL 3 runtimes, it eliminates cloud subscriptions, telemetry, and webview wrapper memory overhead. It delivers private, uncensored intelligence directly on consumer NVIDIA GeForce RTX hardware.

---

## ⚡ Key Architectural Highlights

* **Native Win32 / Dear ImGui Frontend:** Zero Electron or webview dependencies. Rendered in hardware-accelerated OpenGL 3 with a custom slate dark theme.


* **Auto-Maximizing 1600p+ HiDPI Optimization:** Configured with scaled 28pt Segoe UI typography and a 1.15× global UI layout scaling factor (`ImGuiStyle::ScaleAllSizes`) for clear rendering on modern QHD/4K displays.
* **Embedded Sidecar Lifecycle Supervision:** Self-contained runtime process supervisor (`ProcessManager.h`) that automatically spawns, monitors, and flushes local server engines (`llama-server.exe` on port `8080`) without requiring third-party server frontends[cite: 1, 4, 6].
* **Hardware-Aware Diagnostic Profiling:** Built-in DirectX Graphics Infrastructure (DXGI) and Windows memory polling at startup[cite: 1, 6]. Automatically measures dedicated GPU VRAM and physical system RAM to configure compute tiers[cite: 1, 4].
* **Dynamic VRAM Hot-Swapping:** Automatically flushes GPU memory when switching modalities (e.g., exiting text LLMs to free memory for neural audio or diffusion models) to prevent Out-Of-Memory (OOM) crashes[cite: 1, 4, 6].
* **Integrated Model Repository & Downloader:** Full-screen in-app manager (`Settings -> Repetere Models`) supporting chunked CPR downloads directly from Hugging Face with 4-byte GGUF magic header (`0x46554747`) integrity verification.


* **Thin 1-Click Installer Deployment:** Packaged via Inno Setup into a modern setup executable that scaffolds user directory structures and configures isolated sidecars without requiring elevated administrator access[cite: 5, 7].

---

## 🖥️ System Requirements

| Component | Minimum Specification | Recommended Specification |
| --- | --- | --- |
| **Operating System** | Windows 10 / 11 (64-bit) | Windows 11 (64-bit) |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM) | NVIDIA RTX 40/50-Series (12 GB+ VRAM)

 |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+) | Latest NVIDIA Studio Drivers |
| **System Memory** | 16 GB Physical RAM

 | 32 GB Physical RAM (Required for Hybrid Mode) |
| **Target Storage** | 20 GB free space on NVMe SSD | 50 GB+ free space on NVMe SSD |

---

## 🚀 5-Workspace Multimodal Suite

Repetere AI partitions workflows into five isolated, state-preserved production environments:

### 1. CODING Workspace

* **Engine Target:** Qwen 2.5 Coder 7B / 14B / 32B Instruct (`Q4_K_M`)


* **Markdown Syntax Extraction:** Automatically identifies triple-backtick language blocks (`````) and presents code in horizontal-scrolling containers with snippet-level **Copy** buttons.


* **Quick-Copy Response:** One-click **[ Copy Full Response ]** action directly beneath assistant outputs for rapid clipboard export.
* **Context Preservation:** Multi-turn message serialization persists conversation history across iterative debugging sessions[cite: 15, 17].

### 2. CHAT Workspace

* **Engine Target:** Meta Llama 3.1 8B Instruct (`Q4_K_M`)


* **General Intelligence:** Configured for deep reasoning, long-context document analysis, and natural conversational assistance.


* **Context Reset & Archiving:** Red **Clear Chat** button archives the session to disk while resetting active VRAM context[cite: 6, 7].

### 3. CREATIVE WRITING Workspace

* **Engine Target:** Hermes 3 Llama 3.1 8B / Narrative checkpoints


* **Uncensored Narrative Drafting:** Tailored for complex world-building, scene progression, scriptwriting, and dialogue without cloud filtering.



### 4. AUDIO (MUSIC) Production Studio

* **Engine Target:** YuE2 Neural Audio Synthesis Engine (`yue2-3b-q4_0.gguf` + `yue2-vae-f16.gguf`)
* **Full-Vocal Song Generation:** Supports custom style tags (e.g., `60s Jazz`, `Alternative Rock`) combined with multi-section structured lyrics (`[Verse]`, `[Chorus]`, `[Bridge]`).
* **Input Sanitization:** Automatic filtering converts quotes and flattens newlines to prevent `cmd.exe` terminal argument truncation.
* **Dynamic Output Serialization:** Generated tracks are automatically formatted and tagged as `[StyleTag]_[Lyric1]_[Lyric2]_[Timestamp].wav` in `output/music/`.
* **Integrated Transport Controls:** Single-click playback via native Win32 system shell dispatching straight to default media players.

### 5. IMAGES (DIFFUSION) Studio

* **Engine Target:** FLUX.1 Schnell (`Q4_K_M`) / Stable Diffusion CPP (`sd.exe`)


* **Granular Generation Controls:** Positive and negative prompt inputs, inference steps (1–50), and CFG scale adjustments.


* **Reference Image Conditioning:** Native Windows file picker (`OpenNativeFileDialog`) allowing base image loading for image-to-image workflows.

---

## ⚙️ Hardware Compute Modes

The top-right header contains an engine mode toggle:

* **GPU Mode:** Locks model execution entirely within dedicated GPU VRAM for the highest possible token throughput and lowest latency.


* **HYBRID Mode:** Activates an interactive trade-off confirmation dialog. Spans layers across host RAM and GPU VRAM. This allows GPUs with 8 GB–12 GB of VRAM to execute larger 14B–32B parameter models without Out-Of-Memory termination.



---

## 📁 Installation & Model Setup

### 1. Install via Setup Executable

1. Download **`RepetereAI-Setup-v0.5-beta.exe`** from the [GitHub Releases](https://www.google.com/search?q=https://github.com/securenrn-del/repetereai/releases) page[cite: 5, 6].
2. Run the installer[cite: 5]. It installs into `%LOCALAPPDATA%\Programs\Repetere AI` without requiring administrator access[cite: 5].
3. Check **Launch Repetere AI** to start[cite: 5].

### 2. Model Weight Management

Model weights reside in the local application directory:

```text
Repetere AI/
├── FREEAI.exe                 # Main desktop orchestrator
├── bin/                       # Inference engines & CUDA runtime DLLs
│   ├── llama-server.exe
│   └── audio/
│       └── audiocpp_cli.exe
├── models/                    # GGUF Model weights directory
└── output/
    ├── music/                 # Generated WAV audio files
    └── images/                # Generated diffusion artwork

```

#### In-App Downloader:

Navigate to **Settings ➔ Repetere Models**. The repository table displays your hardware profile and provides one-click downloads for verified text models directly into `models/`.

#### Audio Studio Files (YuE2):

To enable song and vocal synthesis in the **AUDIO** workspace, ensure the following files exist in `models/`:

* `models/yue2-3b-q4_0.gguf` (Primary 3B synthesis weights, ~2.48 GB)
* `models/yue2-vae-f16.gguf` (Neural audio VAE decoder, ~265 MB)

---

## 🔒 Conversation History & Safety Overlays

* **Local JSON Persistence:** Conversations automatically serialize to `chat_history.json` upon context clear or application shutdown[cite: 6, 7].
* **Transcript Viewer:** Accessible via **History ➔ Open History Transcripts** to inspect past sessions by timestamp[cite: 6, 7].
* **Context Restoration:** Single-click **[ Load Conversation into Active Tab ]** reloads archived sessions directly into active memory.
* **History Wipe Guard:** The **Clear All Saved Transcripts** action triggers a confirmation modal requiring explicit verification before permanently removing stored logs.

---

## 📜 License & Acknowledgments

Engineered by **Nathaniel Richardson Jr.** as part of the Repetere AI compute initiative[cite: 5, 6]. Distributed under the MIT License. Special thanks to the open-source contributors behind `llama.cpp`, Dear ImGui, GLFW, and YuE2.

---


3. Navigate to **Releases** on GitHub, draft the `v0.5-beta` pre-release, paste the release summary, attach `ReleaseSetup\RepetereAI-Setup-v0.5-beta.exe`, and publish[cite: 5, 6].
