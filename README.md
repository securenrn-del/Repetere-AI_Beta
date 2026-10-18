# ⚡ Repetere AI (beta-0.6b) ⚡

By Nathaniel Richardson Jr.

---

### Compute Sovereignty Restored

**Repetere AI** is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware.

Named after the Latin verb *repetere* ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows.

---

> [!IMPORTANT]
> **Zero Cloud Telemetry:** All inference requests, prompts, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host hardware.
> 
> 

---

## ⚡ System Requirements

| Component | Minimum Specification | Recommended Specification

 |
| --- | --- | --- |
| **Operating System** | Windows 10 (64-bit)

 | Windows 11 (64-bit)

 |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM)

 | NVIDIA RTX 40/50-Series (12 GB+ VRAM)

 |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+)

 | Latest NVIDIA Studio Drivers

 |
| **System Memory** | 16 GB Physical RAM

 | 32 GB Physical RAM (Required for Hybrid Mode)

 |
| **Target Storage** | 20 GB free space on SSD

 | 50 GB+ free space on NVMe SSD

 |

---

## 📋 Comprehensive Changelog & Today's Updates

### Version 0.6b-beta — Modular Decoupling, Full FLUX Architecture & Multi-Encoder Integrity

Version 0.6b-beta represents a major milestone in codebase decoupling and multimodal completion. Workspace presentation logic has been completely separated out of `FREEAI.cpp` into dedicated translation units (`ImageStudioUI.cpp`, `MusicStudioUI.cpp`, `ChatUI.cpp`), the FLUX diffusion pipeline is fully wired with multi-encoder detection, and critical runtime path resolutions have been hardened.

```diff
+ Added modular UI translation unit decoupling: isolated ImageStudioUI and MusicStudioUI out of FREEAI.cpp
+ Added complete FLUX diffusion multi-component catalog: clip_l.gguf, t5xxl_q4_k.gguf, and ae.gguf alongside flux1-schnell-Q4_0.gguf
+ Added support for both .gguf and .safetensors encoder formats (clip_l, ae, t5xxl_q4_k)
+ Added persistent red UI warning badges and action cards for missing companion weights in Image and Audio studios
+ Added CPR follow-redirect flags (cpr::Redirect{10L, true, true, ...}) for seamless Hugging Face LFS asset downloads
+ Added normalized single-root pathing (<repo_root>/output/music) to prevent nested /freeai/freeai directory duplication
! Fixed "Open Output Folder" in Music Studio to ensure directory creation and direct explorer launching
! Fixed splash screen startup failure by adding multi-level relative path resolution (./, ../, ../../)
! Fixed History transcript modal closing mechanics (Escape, close box [X], and Return buttons restored)
! Fixed Settings menu to restore Hardware Diagnostics Profile and About Repetere AI dialog with GitHub repository linking

```

---

### What Was Fixed Today

* **Splash Screen Auto-Discovery:** Resolved path-traversal failures in `ProcessManager::ResolvePath` when launching directly from Visual Studio's `$(ProjectDir)`[cite: 14]. Multi-directory fallbacks (`./`, `../`, `../../`) guarantee `splashscreen.jpg` is always loaded into an OpenGL texture with proper aspect-ratio scaling[cite: 4, 5].
* **Settings & Diagnostic Access:** Restored **Settings ➔ Hardware Diagnostics Profile** and the centered **About Repetere AI** modal[cite: 2, 5], linking directly to [https://github.com/securenrn-del/Repetere-AI_Beta](https://www.google.com/search?q=https://github.com/securenrn-del/Repetere-AI_Beta) via `ShellExecuteA`[cite: 2, 5, 14].
* **History Modal Exit Routing:** Fixed event trapping in `HistoryUI` so pressing **Escape**, clicking the title bar `[X]`, or clicking **[ Return to Workspace ]** immediately and reliably closes the overlay[cite: 2, 6].
* **Music Studio Output Directory Normalization:** Corrected relative path concatenation that created double-nested `/freeai/freeai/output/music` folders. Paths now resolve strictly to `<repo_root>/output/music`.


* **"Open Output Folder" Execution:** Wired `std::filesystem::create_directories(outDir)` prior to calling `ShellExecuteA(NULL, "open", ...)`, ensuring the Windows Explorer shell opens the music output folder without failing.



---

### What Was Added Today

* **Full Image Studio Architecture (`ImageStudioUI.h/.cpp`):**
* Fully decoupled the image generation canvas into its own dedicated module[cite: 2, 12].
* Added `ImageStudioUI::OnTabEnter` to automatically index `./output/images/` and `ImageStudioUI::UnloadFromMemory` to flush active OpenGL textures and buffers from VRAM when leaving the tab[cite: 2, 14].
* Multi-component encoder verification: Image Studio inspects `./models/` for companion dependencies required by FLUX[cite: 2], supporting both `.gguf` and `.safetensors` variants (`clip_l`, `ae`, and `t5xxl_q4_k`) with a missing-file notice card[cite: 2].


* **Synchronized Catalog in In-App Downloader (`ModelDownloader.h/.cpp`):**
* Expanded `GetCatalog()` to include all required components for FLUX diffusion and YuE2 audio synthesis.
* Added pre-configured catalog download targets for `flux1-schnell-Q4_0.gguf`, `clip_l.gguf`, `t5xxl_q4_k.gguf`, and `ae.gguf`.
* Included `cpr::Redirect{10L, true, true, cpr::PostRedirectFlags::POST_ALL}` to follow Hugging Face CDN and LFS redirection loops without corrupting `.part` downloads.
* Enforced 4-byte GGUF magic binary header verification (`0x46554747` / `GGUF`) in `ValidateGGUFHeader()` before finalizing downloaded models[cite: 1, 4, 13].


* **Modular Codebase Reorganization:**
* Cleaned monolithic blocks out of `FREEAI.cpp`, isolating `MusicStudioUI` and `ImageStudioUI` into dedicated translation units while keeping `Types.h` structurally decoupled[cite: 2, 12].



---

## 🚀 Quick Start: Installation & First Launch

1. Go to the [Releases](https://github.com/securenrn-del/Repetere-AI_Beta/releases) page and download **`RepetereAI-Setup-v0.6b-beta.exe`**.


2. Run the installer. It extracts into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges.


3. Launch **Repetere AI** from your Desktop shortcut or Start Menu.
4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key[cite: 2, 7].
5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM[cite: 7]. Click **Confirm Hardware** to enter the main workstation[cite: 7].

---

## 📦 How to Download & Manage AI Models

AI models are the local weights that power each workspace. They must be downloaded before you can generate code, text, music, or images[cite: 4, 12].

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**.


2. The overlay displays your detected hardware profile, active engine bindings, and verified catalog[cite: 4, 12]:
* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B / 32B Hybrid*)[cite: 4, 6]
* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 4]
* **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 4]
* **Audio / Music Studio (Required Files):**
* *YuE2 3B Full Song & Singing Engine* (`yue2-3b-q4_0.gguf`, ~2.48 GB)[cite: 9]
* *YuE2 Neural Audio VAE Decoder* (`yue2-vae-f16.gguf`, ~265 MB)[cite: 9, 12]


* **Images Workspace (FLUX Schnell & Companion Encoders):**
* *FLUX.1 Schnell Diffusion* (`flux1-schnell-Q4_0.gguf`)[cite: 4]
* *CLIP-L Text Encoder* (`clip_l.gguf` or `.safetensors`)[cite: 2]
* *T5-XXL Text Encoder* (`t5xxl_q4_k.gguf` or `.safetensors`)[cite: 2]
* *VAE Decoder* (`ae.gguf` or `.safetensors`)[cite: 2]




3. Click **[ Download ]** next to your desired model[cite: 4, 12]. The in-app manager streams chunks via CPR with real-time transfer telemetry and validates the 4-byte GGUF magic header (`0x46554747`)[cite: 4, 5].
4. When finished, the status badge changes to green (**Installed**)[cite: 4, 18]. Click **[ Return to Workspace ]**.

### Option B: Manual File Placement (Advanced)

Place `.gguf` or `.safetensors` weight files directly into your local application directory[cite: 2, 12]:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

---

## 🗂️ Active Modular Codebase Architecture

```text
RepetereAI/
├── bin/                        # Native inference sidecars (llama-server.exe, sd.exe, CUDA DLLs)
│   └── audio/                  # Neural audio sidecar (audiocpp_cli.exe)
├── models/                     # Target directory for downloaded .gguf models & encoders
│   └── sidecars/               # YuE2 configs & tokenizers (yue2-model-config.json, etc.)
├── output/                     # Local artifact renders
│   ├── images/                 # Generated diffusion artwork
│   └── music/                  # Synthesized WAV audio files (<repo_root>/output/music)
├── freeai/
│   ├── Types.h                 # Core data structures (ChatSessionState, ImageStudioState, MusicStudioState)
│   ├── HardwareScanner.h       # DXGI & Windows memory querying engine for VRAM/RAM tier calculation
│   ├── ProcessManager.h        # Win32 child process supervisor (Job Objects, headless flags, path resolution)
│   ├── ModelDownloader.h/.cpp  # Asynchronous CPR chunked model downloader with GGUF header validation
│   ├── InferenceClient.h/.cpp  # Detached asynchronous CPR REST worker pipeline for chat completions
│   ├── HistoryManager.h/.cpp   # JSON escaping, serialization, and chat_history.json disk I/O routines
│   ├── Theme.h/.cpp            # OpenGL texture loading (stb_image), window icon hooks, ImGui dark palette
│   ├── ChatUI.h/.cpp           # Code block syntax extractor, clipboard copy actions, chat workspace layout
│   ├── HistoryUI.h/.cpp        # Saved transcript modal overlay and session loading
│   ├── ModelManagerUI.h/.cpp   # Hardware telemetry split-view and model deletion controls
│   ├── MusicStudioUI.h/.cpp    # YuE2 two-column production rack, lyrics buffer, and playback transport
│   ├── ImageStudioUI.h/.cpp    # FLUX diffusion split prompt layout, texture canvas, and encoder checks
│   └── FREEAI.cpp              # Main orchestrator, GLFW/OpenGL loop, splash screen, top menu bar, tabs
├── .gitignore                  # Excludes build caches (.vs/, x64/, Debug/, Release/, *.zip)
├── chat_history.json           # Local serialized conversation storage
├── FREEAI.slnx                 # XML-based Visual Studio Solution
└── splashscreen.jpg            # Startup graphic and window icon asset

```

---

## 🛠️ Verification Checklist for Next Build

1. **Clean & Build Solution:** Run **Build ➔ Clean Solution**, followed by **Ctrl + Shift + B** in Visual Studio 2022 to confirm zero compilation or linking errors.
2. **Launch & Verify UI Navigation:**
* Confirm the splash screen displays and dismisses on click or keypress.
* Open **Settings ➔ Hardware Diagnostics Profile** and **Settings ➔ About Repetere AI** to ensure modals appear and the GitHub URL activates cleanly.
* Open **History ➔ Open History Transcripts** and confirm **Escape** and the **[ Return to Workspace ]** button properly close the window.


3. **Validate Audio Studio Pathing:**
* Generate a test audio track and verify the console outputs `--out` targeting `<repo_root>/output/music/<track_name>.wav` without redundant nested paths.
* Click **[ Open Output Folder ]** and ensure Windows Explorer launches directly to `output/music/`.


4. **Inspect Image Studio Encoders:**
* Open the **IMAGES** tab and verify whether companion files (`clip_l`, `t5xxl`, `ae`) are detected or trigger the expected download notice cards.
