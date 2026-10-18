```markdown
# ⚡ Repetere AI (beta-0.6b.4) ⚡

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

| Component | Minimum Specification | Recommended Specification |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit)[cite: 1] | Windows 11 (64-bit)[cite: 1] |
| **GPU Acceleration** | NVIDIA RTX 30-Series (8 GB VRAM)[cite: 1] | NVIDIA RTX 40/50-Series (12 GB+ VRAM)[cite: 1] |
| **Display Drivers** | NVIDIA Game Ready / Studio 528+ (CUDA 12+)[cite: 1] | Latest NVIDIA Studio Drivers[cite: 1] |
| **System Memory** | 16 GB Physical RAM[cite: 1] | 32 GB Physical RAM (Required for Hybrid Mode)[cite: 1] |
| **Target Storage** | 20 GB free space on SSD[cite: 1] | 50 GB+ free space on NVMe SSD[cite: 1] |

---

## 📋 Comprehensive Changelog & Version History

### Version 0.6b.4-beta — Modular Decoupling, Full FLUX Architecture & Multi-Encoder Integrity

Version 0.6b.4-beta delivers complete modular separation of core workspaces out of `FREEAI.cpp`, deploys the full FLUX diffusion multi-encoder pipeline, hardens runtime path resolution, and integrates persistent companion weight validation across audio and visual studios[cite: 1, 2, 8].

```diff
+ Added modular UI translation unit decoupling: isolated ImageStudioUI and MusicStudioUI out of FREEAI.cpp
+ Added complete FLUX diffusion multi-component catalog: clip_l.gguf, t5xxl_q4_k.gguf, and ae.gguf alongside flux1-schnell-Q4_0.gguf
+ Added dual format support for encoders: accepts both .gguf and .safetensors variants (clip_l, ae, t5xxl_q4_k)
+ Added persistent red UI warning badges and action cards for missing companion weights in Image and Audio studios
+ Added CPR follow-redirect flags (cpr::Redirect{10L, true, true, ...}) for seamless Hugging Face LFS asset downloads
+ Added normalized single-root pathing (<repo_root>/output/music) to eliminate nested /freeai/freeai directory duplication
+ Added automated VRAM unloading on tab exit via ImageStudioUI::UnloadFromMemory
! Fixed "Open Output Folder" in Music Studio to ensure directory creation and direct explorer shell launching
! Fixed splash screen startup failure by adding multi-level relative path resolution (./, ../, ../../)
! Fixed History transcript modal closing mechanics (Escape, title bar [X], and Return buttons restored)
! Fixed Settings menu to restore Hardware Diagnostics Profile and About Repetere AI dialog with repository link

```

---

#### Detailed Fixes & Performance Enhancements

* **Splash Screen Auto-Discovery:** Resolved relative path-traversal failures in `ProcessManager::ResolvePath` when executing directly inside Visual Studio's `$(ProjectDir)`[cite: 1, 14]. Multi-directory fallbacks (`./`, `../`, `../../`) ensure `splashscreen.jpg` is always located and bound to an OpenGL texture with correct aspect-ratio scaling[cite: 1, 4, 5].
* **Settings & Diagnostics Access:** Restored access to **Settings ➔ Hardware Diagnostics Profile** and the centered **About Repetere AI** modal[cite: 1, 2, 5], linking directly to [https://github.com/securenrn-del/Repetere-AI_Beta](https://www.google.com/search?q=https://github.com/securenrn-del/Repetere-AI_Beta) via `ShellExecuteA`[cite: 1, 2, 5, 14].
* **History Modal Exit Routing:** Fixed input trapping in `HistoryUI` so pressing **Escape**, clicking the title bar close box `[X]`, or clicking **[ Return to Workspace ]** immediately and reliably closes the overlay[cite: 1, 2, 6].
* **Music Studio Output Directory Normalization:** Corrected relative path concatenation that created double-nested `/freeai/freeai/output/music` folders. Paths now resolve strictly to `<repo_root>/output/music`.


* **"Open Output Folder" Execution:** Wired `std::filesystem::create_directories(outDir)` prior to calling `ShellExecuteA(NULL, "open", ...)`, ensuring the Windows Explorer shell opens the music output folder without failing.



---

#### Features & Architectural Additions

* **Full Image Studio Architecture (`ImageStudioUI.h/.cpp`):**
* Decoupled the image generation canvas into its own dedicated compilation unit[cite: 1, 2, 12].
* Added `ImageStudioUI::OnTabEnter` to automatically index `./output/images/` and `ImageStudioUI::UnloadFromMemory` to flush active OpenGL textures and buffers from VRAM when switching tabs[cite: 1, 2, 14].
* Multi-component encoder verification: Image Studio inspects `./models/` for companion dependencies required by FLUX[cite: 1, 2], supporting both `.gguf` and `.safetensors` variants (`clip_l`, `ae`, and `t5xxl_q4_k`) with a missing-file notice card[cite: 1, 2].


* **Synchronized In-App Downloader Catalog (`ModelDownloader.h/.cpp`):**
* Expanded `GetCatalog()` to include all required components for FLUX diffusion and YuE2 audio synthesis[cite: 1, 4].
* Added pre-configured catalog download targets for `flux1-schnell-Q4_0.gguf`, `clip_l.gguf`, `t5xxl_q4_k.gguf`, and `ae.gguf`[cite: 1, 4].
* Included `cpr::Redirect{10L, true, true, cpr::PostRedirectFlags::POST_ALL}` to follow Hugging Face CDN and LFS redirection loops without corrupting `.part` downloads[cite: 1, 4].
* Enforced 4-byte GGUF magic binary header verification (`0x46554747` / `GGUF`) in `ValidateGGUFHeader()` before finalizing downloaded models[cite: 1, 4, 13].


* **Modular Codebase Separation:**
* Cleaned monolithic blocks out of `FREEAI.cpp`, isolating `MusicStudioUI` and `ImageStudioUI` into dedicated translation units while keeping `Types.h` structurally decoupled[cite: 1, 2, 12].



---

## 🚀 Quick Start: Installation & First Launch

1. Go to the [Releases](https://github.com/securenrn-del/Repetere-AI_Beta/releases) page and download **`RepetereAI-Setup-v0.6b.4-beta.exe`**.
2. Run the installer[cite: 1, 12]. It extracts into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges[cite: 1, 12].
3. Launch **Repetere AI** from your Desktop shortcut or Start Menu.
4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key[cite: 1, 2, 7].
5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM[cite: 1, 7]. Click **Confirm Hardware** to enter the main workstation[cite: 1, 7].

---

## 📦 How to Download & Manage AI Models

AI models are the local weights that power each workspace. They must be present on disk before generation can proceed[cite: 1, 4, 12].

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**[cite: 1, 12].
2. The overlay displays your detected hardware profile, active engine bindings, and verified catalog[cite: 1, 4, 12]:
* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B / 32B Hybrid*)[cite: 1, 4, 6]
* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 1, 4]
* **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 1, 4]
* **Audio / Music Studio (Required Files):**
* *YuE2 3B Full Song & Singing Engine* (`yue2-3b-q4_0.gguf`, ~2.48 GB)[cite: 1, 9]
* *YuE2 Neural Audio VAE Decoder* (`yue2-vae-f16.gguf`, ~265 MB)[cite: 1, 9, 12]


* **Images Workspace (FLUX Schnell & Companion Encoders):**
* *FLUX.1 Schnell Diffusion* (`flux1-schnell-Q4_0.gguf`)[cite: 1, 4]
* *CLIP-L Text Encoder* (`clip_l.gguf` or `.safetensors`)[cite: 1, 2]
* *T5-XXL Text Encoder* (`t5xxl_q4_k.gguf` or `.safetensors`)[cite: 1, 2]
* *VAE Decoder* (`ae.gguf` or `.safetensors`)[cite: 1, 2]




3. Click **[ Download ]** next to your desired model[cite: 1, 4, 12]. The in-app manager streams chunks via CPR with real-time transfer telemetry and validates the 4-byte GGUF magic header (`0x46554747`)[cite: 1, 4, 5].
4. When finished, the status badge changes to green (**Installed**)[cite: 1, 4]. Click **[ Return to Workspace ]**.

### Option B: Manual File Placement (Advanced)

Place `.gguf` or `.safetensors` weight files directly into your local application directory[cite: 1, 2, 12]:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

---

## 🧭 Navigating the Workspaces

Repetere AI organizes workflows across five dedicated environments[cite: 1, 5]:

### 1. CODING (Split-View IDE)

* **Engine Target:** Qwen 2.5 Coder checkpoints (7B, 14B, and 32B Hybrid)[cite: 1, 6].
* **Features:** Triple-backtick markdown extraction with formatted, horizontal-scrolling code containers, dedicated snippet copy actions, and a single-click `[ Copy Full Response ]` button[cite: 1, 6].

### 2. CHAT (Conversational Assistant)

* **Engine Target:** Meta Llama 3.1 8B Instruct[cite: 1, 6].
* **Features:** General reasoning, document summarization, multi-turn message history, and a red `Clear Chat` action protected by context wipe confirmation guards[cite: 1, 6, 8].

### 3. CREATIVE WRITING (Narrative Studio)

* **Engine Target:** Hermes 3 Llama 3.1 8B[cite: 1, 6].
* **Features:** Uncensored long-form story drafting, scriptwriting, timeline planning, and world-building without cloud filtering[cite: 1, 6].

### 4. AUDIO (MUSIC) Production Studio

* **Engine Target:** YuE2 Neural Audio Synthesis Engine (`yue2-3b-q4_0.gguf` / `yue2-3b-q8_0.gguf` + `yue2-vae-f16.gguf`)[cite: 1, 6, 10].
* **Features:**
* 8,192-byte multiline lyrics and stem input buffer (`lyricsBuffer`) supporting structural tags (`[Verse]`, `[Chorus]`, `[Bridge]`)[cite: 1, 6, 10].
* Configurable duration slider supporting up to 360 seconds (6 minutes) of continuous generation[cite: 1, 2, 12].
* Subshell argument sanitization converting double quotes and flattening line breaks to prevent Win32 command truncation[cite: 1, 6, 10].
* Dynamic track serialization saving renders as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` in `output/music/`[cite: 1, 6, 10].
* Integrated Win32 transport playback controls (`PlaySoundA` / `ShellExecuteA`) and direct folder access[cite: 1, 6, 10].



### 5. IMAGES (Diffusion Studio)

* **Engine Target:** FLUX.1 Schnell (`flux1-schnell-Q4_0.gguf`) paired with companion text encoders and VAE decoder[cite: 1, 2, 4].
* **Features:**
* Dual positive and negative prompt inputs, inference steps (1–50), and CFG scale adjustments[cite: 1, 6, 9].
* Standard resolution presets (`512x512`, `768x768`, `1024x1024`, `1280x720`) and native reference image importing for image-to-image conditioning[cite: 1, 6, 9].
* Automated VRAM cleanup via `ImageStudioUI::UnloadFromMemory` to flush textures and buffers upon tab exit[cite: 1, 2, 14].



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

## 📜 License & Acknowledgments

Engineered by **Nathaniel Richardson Jr.** as part of the Repetere AI compute initiative[cite: 1, 5, 6]. Distributed under the MIT License[cite: 1, 6]. Special thanks to the open-source communities powering llama.cpp, Dear ImGui, GLFW, and YuE2[cite: 1, 6].

```

```
