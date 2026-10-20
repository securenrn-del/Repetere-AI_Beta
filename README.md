# ⚡ Repetere AI (v0.7.0-Cuda_beta_stable) ⚡

By Nathaniel Richardson Jr.

---

> [!WARNING]
> ### 🛑 PLEASE READ: THIS IS LOCAL AI!
> 
> 
> **Everything you do runs directly on your machine and will take time.** Model weight streaming, prompt ingestion, neural audio synthesis, and image generation are compute-heavy processes.
> **If the status bar is moving and not throwing an error, IT IS STILL WORKING!** Please be patient and allow the generation pipeline to complete.

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

### Version 0.7.0-Cuda_beta_stable — CUDA Runtime Hardening, Split-Pane IDE, Creative Studio & Multimodal Stabilization

Version 0.7.0-Cuda_beta_stable establishes a production-grade milestone for native Windows execution on NVIDIA CUDA hardware. It hardens the embedded sidecar supervisor and CUDA backend dispatch, introduces an interactive split-pane IDE development environment in **CODING**, deploys a dedicated Three-Pane Novelist Studio in **CREATIVE WRITING**, enforces whitespace-tolerant AST patch diffing, provides automated session archiving, and decouples media translation units into modular native architectures.

```diff
+ Stabilized native NVIDIA CUDA 12 execution runtime backend for local inference sidecars
+ Added interactive Split-Pane IDE workspace in CodingUI: 38% agent prompt/transcript pane, 62% code canvas
+ Added synchronized dual-column line-number gutters aligned with active code buffer
+ Added multi-pattern <<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE in-place AST diff parser
+ Added whitespace- and indentation-tolerant search matching (tab/space normalization and line-ending trims)
+ Added smart markdown code-fence fallback replacing matching functions directly in the editor buffer
+ Added manual [Apply Response to Editor] toolbar action to push raw completions into the live canvas
+ Added automated turn and patch archiving to chat_history.json via SaveSessionToDisk on generation and clear
+ Added dedicated Three-Pane Novelist Studio in CreativeUI: Lore Bible drawer, Live Prose Canvas, Directive Console
+ Added persistent Story Bible & Lore reference document loader (.txt, .md) with autoInjectBible context toggling
+ Added 1 MB dynamic manuscript buffer with 30-step undo/redo snapshot ring buffer (PushManuscriptSnapshot)
+ Added in-place narrative AST scene diff patcher (ApplyNarrativeDiff) with relaxed spacing and prose rewrite fallbacks
+ Added narrative directive presets (Sensory, Cadence, Dialogue Pass) targeting Hermes 3 Llama 3.1 8B
+ Added word count, character count, and modified status badges to the manuscript editor
+ Added green dynamic active model indicator badge in workspace headers and Model Manager ([model] (active))
+ Added modular UI translation unit decoupling: isolated ImageStudioUI, MusicStudioUI, and CreativeUI out of FREEAI.cpp
+ Added complete FLUX diffusion multi-component catalog: clip_l.gguf, t5xxl_q4_k.gguf, and ae.gguf
+ Added dual format support for encoders: accepts both .gguf and .safetensors variants (clip_l, ae, t5xxl_q4_k)
+ Added persistent red UI warning badges and action cards for missing companion weights in Image Studio
+ Added CPR follow-redirect flags (cpr::Redirect{10L, true, true, ...}) for Hugging Face LFS downloads
+ Added normalized single-root pathing (<repo_root>/output/music) to eliminate nested directory duplication
+ Added automated VRAM unloading on tab exit via ImageStudioUI::UnloadFromMemory
! Hardened CUDA PTX JIT compilation and process supervisor sidecar execution stability
! Fixed editor replacement failures by strictly enforcing system prompt diff formatting over raw markdown
! Fixed narrative prose line wrapping and dual-pane chat bubble duplication inside CreativeUI
! Fixed coding and creative session history omissions by hooking SaveSessionToDisk into completions, clears, and shutdown
! Fixed About dialog repository navigation to route directly to beta repo via Win32 ShellExecuteA
! Fixed "Open Output Folder" in Music Studio to ensure directory creation prior to shell dispatch
! Fixed splash screen startup failure by adding multi-level relative path resolution (./, ../, ../../)
! Fixed History transcript modal closing mechanics (Escape, title bar [X], and Return buttons restored)
! Fixed Settings menu to restore Hardware Diagnostics Profile access

```

---

## 🧭 Active Workspaces (Current Implementation)

1. 💻 **CODING (Interactive IDE):** Interactive split-view programming studio powered by Qwen 2.5 Coder checkpoints (7B, 14B, 32B Hybrid). Features line-numbered guttering, in-place AST diff patching (`SEARCH/REPLACE`), whitespace-tolerant snippet matching, manual editor injection, file loading/saving, and turn archiving.


2. 💬 **CHAT (Conversational Assistant):** General instruct reasoning powered by Meta Llama 3.1 8B Instruct with multi-turn context serialization and safety-prompted context clears.


3. ✍️ **CREATIVE WRITING (Novelist Studio):** Uncensored long-form narrative workstation powered by Hermes 3 Llama 3.1 8B. Includes Lore Bible context injection, a 1 MB manuscript canvas with undo/redo snapshot history, directive action chips, and in-place prose patching.


4. 🎵 **AUDIO (MUSIC) Studio:** Full vocal and instrumental song synthesis powered by YuE2 3B weights (`yue2-3b-q4_0.gguf` + `yue2-vae-f16.gguf`). Features an 8,192-byte multiline lyrics buffer, structured tag parsing (`[Verse]`, `[Chorus]`), timeline synthesis up to 6 minutes (360s), CLI argument sanitization, and Win32 transport playback.


5. 🎨 **IMAGES (Diffusion Studio):** Text-to-image and image-to-image canvas powered by FLUX.1 Schnell. Includes dual positive/negative prompt buffers, steps/CFG tuning, resolution presets, and companion encoder detection (`clip_l`, `t5xxl`, `ae`).



---

## 📖 Workspace User Guides: How to Use Each Tab

### 🎨 IMAGES (Diffusion Studio)

The **IMAGES** tab generates high-fidelity local artwork via FLUX.1 Schnell and companion diffusion encoders.

* **Prerequisites:** Ensure `flux1-schnell-Q4_0.gguf` and companion encoders (`clip_l`, `t5xxl_q4_k`, and `ae` in `.gguf` or `.safetensors` format) are installed via **Settings ➔ Repetere Models**.


* **Step-by-Step Workflow:**
1. Click the **IMAGES** tab in the main header.


2. In the **Prompt** box, describe the subject, style, lighting, and composition (e.g., `crazy mushrooms in vibrant bioluminescent forest, 8k`).


3. *(Optional)* In the **Negative Prompt** field, specify elements to exclude (e.g., `blurry, bad hands, low quality`).


4. *(Optional Image-to-Image)* Click **Upload Base Image File...** to select a reference photo using the native file picker.


5. Select a **Resolution Preset** (e.g., `512x512`, `768x768`, `1024x1024`, `1280x720`) and set your **Inference Steps** (e.g., `4` for Schnell/Turbo, or up to `20–50` steps) and **CFG Scale**.


6. Click **[ Render Image ]** (or **Generate New Image**).


7. The image will render directly onto the center canvas and automatically save to `output/images/`. Previous renders remain accessible in the right-hand **Project Explorer** gallery.





---

### 💻 CODING (Interactive IDE)

The **CODING** tab operates as an integrated, two-pane live development environment powered by Qwen 2.5 Coder.

* **Workspace Layout:**
* **Left Pane (38%):** Agent transcript, multi-turn reasoning logs, and directive input prompt.


* **Right Pane (62%):** Live code editor canvas with line-number gutters and buffer controls.




* **Step-by-Step Workflow:**
1. Click the **CODING** tab.


2. To start fresh, simply type a directive into the prompt field (e.g., `create a hello world app in cpp`). To work on an existing file, click **Open...** in the right canvas toolbar to load your source code.


3. Click **Dispatch Diff** or press **Enter**.


4. The model automatically streams changes formatted in `<<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE` AST patch blocks.


5. The in-place diff engine normalizes whitespace and merges code updates directly into the right-hand editor buffer.


6. *(Fallback Action)* If the model returns markdown code fences instead of a patch, click the **[Apply Response to Editor]** toolbar action to manually push completions into the live canvas.


7. Click **Save** or **Save As...** in the editor toolbar to commit the modified buffer to disk. Click **[ Copy Full Response ]** below any assistant bubble to copy raw text to your clipboard.





---

### ✍️ CREATIVE WRITING (Novelist Studio)

The **CREATIVE WRITING** workspace is an uncensored authoring desk powered by Hermes 3 Llama 3.1 8B, engineered for long-form narrative drafting, character tracking, and scene revisions.

* **Workspace Layout:**
* **Left Pane (Story Bible Drawer):** Local world-building notes, faction profiles, and character sheets.


* **Center Pane (Live Prose Canvas):** A 1 MB word-wrapped manuscript canvas equipped with line gutters, real-time word/character telemetry, and a 30-step undo/redo stack.


* **Right Pane (Directive Console):** Scene revision inputs, status logs, and quick style chips.




* **Step-by-Step Workflow:**
1. Click the **CREATIVE WRITING** tab.


2. In the left **Story Bible** panel, click **Browse Project Folder...** to point to a folder of your `.txt` or `.md` reference files. Toggle **Inject into Narrative Engine** (`autoInjectBible`) to automatically seed your lore into the local model's prompt payload.


3. Click **Open...** on the center canvas toolbar to load an existing chapter, or click into the manuscript canvas to draft directly.


4. To request targeted scene revisions or passage continuations, enter a directive in the right pane (e.g., *"Make the pacing faster and emphasize sensory details of the breach"*).


5. *(Preset Action Chips)* Click quick preset chips such as **Sensory**, **Cadence**, or **Dialogue Pass** to pre-fill targeted stylistic directives.


6. Click **Dispatch Directive**. The narrative AST diff parser (`ApplyNarrativeDiff`) updates the affected scenes directly within your center manuscript canvas.


7. Use the **Undo** and **Redo** buttons in the manuscript toolbar to step through revision snapshots without losing prior work. Click **Save** to write changes directly to disk.





---

### 🎵 AUDIO (MUSIC Studio)

The **AUDIO (MUSIC)** workspace synthesizes complete vocal and instrumental audio compositions up to 6 minutes (360s) via the YuE2 engine.

* **Prerequisites:** Ensure both `yue2-3b-q4_0.gguf` (~2.48 GB) and `yue2-vae-f16.gguf` (~265 MB) are downloaded into `models/`.


* **Step-by-Step Workflow:**
1. Click the **AUDIO (MUSIC)** tab.


2. *(Optional AI Translation)* In the **Artist / Band Reference** field, enter a reference band or artist style (e.g., `Linkin Park, Falling in Reverse`). If a local text model is active, the app automatically translates artist cues into technical acoustic parameters.


3. In **Musical Style & Acoustic Tags**, specify genre, instruments, and acoustic properties (e.g., `Alternative Rock, driving drums, distorted drop-D guitar, 105 bpm`).


4. In the **Song Lyrics & Structural Arrangement** buffer (supports up to 8,192 bytes), structure your lyrics using bracket tags:


```text
[Verse]
Walking down this empty road
[Chorus]
Echoes fade into the night

```


5. Adjust the **Track Duration** slider to your desired length in seconds (e.g., `30`–`60` seconds for quick tests, or up to `240`–`360` seconds for full songs).


6. Click **[ Generate Full Song (With Vocals) ]**.


7. Wait while CUDA processes the neural audio layers. Completed tracks automatically save as `[StyleTag]_[Word1]_[Word2]_[Timestamp].wav` in `output/music/`.


8. Use the **Master Transport Monitor** controls at the bottom of the workspace to **Play**, **Pause**, or **Stop** the audio directly within the application.





---

## 🚀 Quick Start: Installation & First Launch

1. Download **`RepetereAI-Setup-v0.7.0-Cuda_beta_stable.exe`** from the [Releases](https://www.google.com/search?q=https://github.com/securenrn-del/Repetere-AI_Beta/releases) page.


2. Run the installer. It extracts cleanly into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges.


3. Launch **Repetere AI** via your Desktop shortcut or Start Menu.


4. Dismiss the startup splash screen by **clicking anywhere** or pressing any key.


5. The **Hardware Configuration Diagnostic** modal inspects your dedicated VRAM and host RAM. Click **Confirm Hardware** to enter the main workstation.



---

## 📦 How to Download & Manage AI Models

AI models are local weights that power each workspace. They must be present on disk before generation can proceed.

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**.


2. Review the curated catalog and click **[ Download ]** next to your desired model:


* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B*)


* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*

* **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*[cite: 2, 4]
* **Audio / Music Studio (Both Required):**
* `yue2-3b-q4_0.gguf` (~2.48 GB)


* `yue2-vae-f16.gguf` (~265 MB)




* **Images Workspace:**
* `flux1-schnell-Q4_0.gguf` (Base diffusion model)


* Companion encoders: `clip_l.gguf`, `t5xxl_q4_k.gguf`, and `ae.gguf`





3. When finished, the status badge changes to green (**Installed**).



### Option B: Manual File Placement (Advanced)

Place `.gguf` or companion `.safetensors` weight files directly into your local application directory:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```
Video Demonstrations: 
- <https://youtu.be/EbnQngF_XS8>
- <https://youtu.be/qtKOvZmqiTY>
- <https://youtu.be/hymrx6ZanV0>

---

## 📸 Workspace Screenshots

---
<img width="2560" height="1528" alt="audio_demo" src="https://github.com/user-attachments/assets/c306e762-7980-4d75-9cdf-5d123c757b8b" />
<img width="2560" height="1528" alt="intro_demo" src="https://github.com/user-attachments/assets/c104a311-5b12-4608-9506-5a46e9e02c42" />
<img width="2560" height="1528" alt="creative_demo" src="https://github.com/user-attachments/assets/ac76462b-31ac-494b-b3b3-e5645e53c746" />
<img width="2560" height="1528" alt="coder_demo" src="https://github.com/user-attachments/assets/385ddb3d-968a-46c2-a5f1-608fd890e553" />

