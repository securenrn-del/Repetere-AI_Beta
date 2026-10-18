# ⚡ Repetere AI (beta-0.6.9) ⚡

By Nathaniel Richardson Jr.

---

### Compute Sovereignty Restored

**Repetere AI** is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware.

Named after the Latin verb *repetere* ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows.

---

> [!IMPORTANT]
> **Zero Cloud Telemetry:** All inference requests, prompts, code modifications, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host hardware.
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

## 📋 Comprehensive Changelog & Version History

### Version 0.6b.4-beta — Interactive IDE Architecture, In-Place Diff Engine & Workspace Stabilization

Version 0.6b.4-beta introduces a live, interactive split-pane IDE development environment directly inside the **CODING** workspace. It incorporates an in-place AST search-and-replace patch engine with whitespace-tolerant block matching, synchronized line numbering, automatic turn archiving to disk, and dynamic model indicator telemetry. Furthermore, this release cements full modular decoupling of media studios, integrates dual-format companion validation across the FLUX pipeline, and hardens runtime path and modal dialog dispatch.

```diff
+ Added interactive Split-Pane IDE workspace in CodingUI: 38% agent prompt/transcript pane, 62% code canvas
+ Added synchronized dual-column line-number gutters aligned with active code buffer
+ Added multi-pattern <<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE in-place AST diff parser
+ Added whitespace- and indentation-tolerant search matching (tab/space normalization and line-ending trims)
+ Added smart markdown code-fence fallback replacing matching functions directly in the editor buffer
+ Added manual [Apply Response to Editor] toolbar action to push raw completions into the live canvas
+ Added automated turn and patch archiving to chat_history.json via SaveSessionToDisk on generation and clear
+ Added green dynamic active model indicator badge in workspace headers and Model Manager ([model] (active))
+ Added modular UI translation unit decoupling: isolated ImageStudioUI and MusicStudioUI out of FREEAI.cpp
+ Added complete FLUX diffusion multi-component catalog: clip_l.gguf, t5xxl_q4_k.gguf, and ae.gguf
+ Added dual format support for encoders: accepts both .gguf and .safetensors variants (clip_l, ae, t5xxl_q4_k)
+ Added persistent red UI warning badges and action cards for missing companion weights in Image Studio
+ Added CPR follow-redirect flags (cpr::Redirect{10L, true, true, ...}) for Hugging Face LFS downloads
+ Added normalized single-root pathing (<repo_root>/output/music) to eliminate nested directory duplication
+ Added automated VRAM unloading on tab exit via ImageStudioUI::UnloadFromMemory
! Fixed coding session history omissions by hooking SaveSessionToDisk into completions, clears, and shutdown
! Fixed editor replacement failures by strictly enforcing system prompt diff formatting over raw markdown
! Fixed About dialog repository navigation to route directly to beta repo via Win32 ShellExecuteA
! Fixed "Open Output Folder" in Music Studio to ensure directory creation prior to shell dispatch
! Fixed splash screen startup failure by adding multi-level relative path resolution (./, ../, ../../)
! Fixed History transcript modal closing mechanics (Escape, title bar [X], and Return buttons restored)
! Fixed Settings menu to restore Hardware Diagnostics Profile access

```

---

### Detailed Fixes & Architectural Additions (Today's Updates)

#### 💻 Interactive Coding IDE & In-Place Diff Engine (`CodingUI.h/.cpp`)

* **Split-Pane Architecture:** Reworked the `CODING` workspace into an integrated split-view engineering studio (38% left agent transcript and prompt queue, 62% right live code canvas).


* **Synchronized Line-Number Gutters:** Implemented real-time dual-column gutter tracking synchronized directly with newline counts in the multiline editor buffer.


* **In-Place Diff Parser (`ApplyDiffBlocks`):**
* Integrated parsing for `<<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE` AST patch blocks.


* Added whitespace and indentation normalization (converting tabs to spaces and trimming carriage returns) to prevent formatting mismatches between local models and disk files from failing string matches.


* Implemented an intelligent markdown code-fence fallback that scans the document for matching function or block signatures and substitutes them in place when diff tags are omitted.


* Added an **Apply Response to Editor** action button allowing users to manually force assistant code directly into the active editor buffer.




* **Multi-Language File Dialogs:** File open and save operations now utilize native Windows dialogs with `OFN_NOCHANGEDIR`, preventing file picker interactions from corrupting the application working directory.


* **Automated Coding Session Archiving:** Wired `#include "HistoryManager.h"` into `CodingUI.cpp`. Completing prompts, receiving patches, clicking **Clear Chat**, and application shutdown triggers `SaveSessionToDisk(state.history, "CODING")`, ensuring development workflows are preserved in `chat_history.json`.



#### ⚡ Host Telemetry & Navigation Hardening (`FREEAI.cpp`)

* **Dynamic Active Model Indicators:** Updated header presentation across all active tabs to display `<model_name> (active)` in green text, synchronizing visual runtime status between the main viewport and the Model Manager table.


* **Beta Repository Linking:** Restored the **About Repetere AI** modal in both `Settings` and `About` menus, executing native `ShellExecuteA` calls targeting the beta repository (`[https://github.com/securenrn-del/Repetere-AI_Beta](https://github.com/securenrn-del/Repetere-AI_Beta)`).


* **Shutdown History Flush:** Application termination cascades now auto-archive all active tabs—including `g_TabCoding`—immediately before stopping inference child processes.



#### 🖼️ FLUX Studio & Decoupled Media Translation Units

* **Modular UI Separation:** Extracted `ImageStudioUI` and `MusicStudioUI` into dedicated compilation units, eliminating header circular dependencies and accelerating build times.


* **Companion Dependency Verification:** Image Studio checks `./models/` for companion dependencies required by FLUX, validating both `.gguf` and `.safetensors` files (`clip_l`, `ae`, `t5xxl_q4_k`).


* **Automated VRAM Garbage Collection:** Navigating away from the image workspace triggers `ImageStudioUI::UnloadFromMemory`, automatically purging bound OpenGL textures and raw frame buffers from video memory.


* **Resilient Model Downloader:** Extended `ModelDownloader` with Hugging Face LFS redirect tracking (`cpr::Redirect{10L, true, ...}`) and automated 4-byte GGUF magic binary header verification (`0x46554747` / `GGUF`).



---

## 🧭 Active Workspaces (Current Implementation)

1. 💻 **CODING (Interactive IDE):** Interactive split-view programming studio powered by Qwen 2.5 Coder checkpoints (7B, 14B, 32B Hybrid). Features line-numbered guttering, in-place AST diff patching (`SEARCH/REPLACE`), whitespace-tolerant snippet matching, manual editor injection, file loading/saving, and turn archiving.


2. 💬 **CHAT (Conversational Assistant):** General instruct reasoning powered by Meta Llama 3.1 8B Instruct with multi-turn context serialization and safety-prompted context clears.


3. 🎵 **AUDIO (MUSIC) Studio:** Full vocal and instrumental song synthesis powered by YuE2 3B weights (`yue2-3b-q4_0.gguf` + `yue2-vae-f16.gguf`). Features an 8,192-byte multiline lyrics buffer, structured tag parsing (`[Verse]`, `[Chorus]`), timeline synthesis up to 6 minutes (360s), CLI argument sanitization, and Win32 transport playback.


4. 🎨 **IMAGES (Diffusion Studio):** Text-to-image and image-to-image canvas powered by FLUX.1 Schnell. Includes dual positive/negative prompt buffers, steps/CFG tuning, resolution presets, and companion encoder detection (`clip_l`, `t5xxl`, `ae`).



---

## 🚀 Quick Start: Installation & First Launch

1. Download **`RepetereAI-Setup-v0.6.9-beta.exe`** from the [Releases](https://www.google.com/search?q=https://github.com/securenrn-del/Repetere-AI_Beta/releases) page.
2. Run the installer. It extracts into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges.


3. Launch **Repetere AI** via your Desktop shortcut or Start Menu.
4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key.


5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM. Click **Confirm Hardware** to enter the main workstation.



---

## 📦 How to Download & Manage AI Models

AI models are local weights that power each workspace. They must be present on disk before generation can proceed.

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**.


2. Review the curated catalog and click **[ Download ]** next to your desired model:


* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B*)[cite: 7]
* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*[cite: 7]
* **Audio / Music Studio (Both Required):**
* `yue2-3b-q4_0.gguf` (~2.48 GB)[cite: 7]
* `yue2-vae-f16.gguf` (~265 MB)[cite: 7]


* **Images Workspace:**
* `flux1-schnell-Q4_0.gguf` (Base diffusion model)


* Companion encoders: `clip_l.gguf`, `t5xxl_q4_k.gguf`, and `ae.gguf`





3. When finished, the status badge changes to green (**Installed**)[cite: 7].

### Option B: Manual File Placement (Advanced)

Place `.gguf` or companion `.safetensors` weight files directly into your local application directory:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```
