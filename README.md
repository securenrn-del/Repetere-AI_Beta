Here is the updated, unified documentation file edited specifically for your new **`v0.9-Vulkan-Cuda_Hybrid-beta`** release, maintaining the complete cumulative history from **v0.7.0** up to the new build:

```markdown
# ⚡ Repetere AI (v0.9-Vulkan-Cuda_Hybrid-beta FINAL) ⚡

By Nathaniel Richardson Jr.

---

> [!WARNING]
> ### 🛑 PLEASE READ: THIS IS LOCAL AI!
> 
> **Everything you do runs directly on your machine and will take time.** Model weight streaming, prompt ingestion, neural audio synthesis, and image generation are compute-heavy processes. Also this an unsigned installer, so it may show an unsafe warning when you attempt to install, click show more then install anyway. I will begin signing in 1.0[cite: 1].

> **If the status bar is moving and not throwing an error, IT IS STILL WORKING!** Please be patient and allow the generation pipeline to complete[cite: 1].

I am in dire need of anyone who has issues or wants to talk about the architecture, please drop a line on our reddit:

[https://www.reddit.com/r/RepetereAI/s/qo7zFqwHjo](https://www.reddit.com/r/RepetereAI/s/qo7zFqwHjo)

---

### Compute Sovereignty Restored

**Repetere AI** is a decentralized, self-hosted Artificial Intelligence ecosystem engineered to restore computing sovereignty, eliminate recurring cloud subscription fees, and provide uncensored, 100% private multimodal generation directly on consumer-grade hardware[cite: 1].

Named after the Latin verb *repetere* ("to demand back / reclaim" compute sovereignty, and "to repeat / iterate" computational forward loops), this repository houses the native C++ desktop host application for Windows[cite: 1].

---

> [!IMPORTANT]
> **Zero Cloud Telemetry & True Hardware Neutrality:** All inference requests, prompts, code modifications, transcripts, audio arrangements, and image generations execute 100% offline and locally on your host silicon[cite: 1]. Built natively in bare-metal C++, GLFW, and Dear ImGui over OpenGL 3—completely bypassing Electron, Python, or Chromium webview wrapper overhead[cite: 1].
> 
> Unifies native **NVIDIA CUDA 12** and **Universal Vulkan 1.3** compute engines with dynamic **Hybrid Layer Splitting**[cite: 1, 19], unlocking native hardware acceleration across **NVIDIA GeForce RTX, AMD Radeon, Intel Arc, and modern APU/iGPU architectures**[cite: 1].

---

## ⚡ System Requirements

| Component | Minimum Specification (Universal Vulkan / APU)[cite: 1] | Recommended Specification (NVIDIA CUDA / High-End Hybrid)[cite: 1] |
| :--- | :--- | :--- |
| **Operating System** | Windows 10 (64-bit)[cite: 1] | Windows 11 (64-bit)[cite: 1] |
| **GPU Acceleration** | Vulkan 1.3-compatible GPU / APU (AMD Radeon, Intel Arc, NVIDIA, or modern APU)[cite: 1] | NVIDIA RTX 40/50-Series (12 GB+ VRAM) or AMD Radeon RX 7000-Series[cite: 1] |
| **Display Drivers** | Latest AMD Software: Adrenalin Edition / Intel Arc / NVIDIA Drivers[cite: 1] | Latest NVIDIA Game Ready / Studio Drivers (CUDA 12+)[cite: 1] |
| **System Memory** | 16 GB Physical RAM (Unified Memory for APUs)[cite: 1] | 32 GB+ Physical RAM (Required for Hybrid & Large Quant Offloading)[cite: 1] |
| **Target Storage** | 20 GB free space on SSD[cite: 1] | 50 GB+ free space on NVMe SSD[cite: 1] |

---

## 📋 Comprehensive Changelog & Version History

### Version v0.9-Vulkan-Cuda_Hybrid-beta — Unified Hybrid Offload Architecture, Dynamic Backend Hot-Swapping & Stability Hardening

Version `v0.9-Vulkan-Cuda_Hybrid-beta` unifies Repetere AI's hardware-agnostic runtime pipeline[cite: 1]. It hardens isolated sidecar execution domains (`bin/cuda/` and `bin/vulkan/`)[cite: 1], expands the dynamic `[CUDA] <-> [VULKAN]` runtime switch[cite: 1], and deploys full **Hybrid Layer Offloading** across both backends (`CUDA + Hybrid` and `Vulkan + Hybrid`) to safely span 14B–32B parameter models across host system RAM and GPU video memory without out-of-memory faults[cite: 1, 19].

```diff
+ Updated deployment versioning to v0.9-Vulkan-Cuda_Hybrid-beta
+ Unified Hybrid compute mode across both CUDA and Vulkan backends (-ngl dynamic layer allocation)
+ Hardened runtime isolation: bin/cuda/ (CUDA 12 / cuBLAS) and bin/vulkan/ (SPIR-V / ggml-vulkan)
+ Maintained dynamic [CUDA] <-> [VULKAN] backend hot-swapping directly in the primary menu bar
+ Enforced low-level Win32 Job Object containment (JOB_OBJECT_LIMIT_KILL_ON_JOB_CLOSE) across all sidecars
+ Preserved temporary file streaming (--prompt-file, --negative-prompt-file) to eliminate shell arg truncations
+ Preserved in-place AST diff patching (<<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE) in CodingUI
+ Preserved full YuE2 vocal timeline synthesis up to 360s with isolated audiocpp_cli.exe routing
+ Preserved companion weight verification (.gguf and .safetensors) for FLUX diffusion pipeline
+ Integrated EULA (EULA.txt) covering software rights, beta disclaimer, and local privacy guarantees
! Fixed sidecar process cleanup during high-frequency backend transitions
! Resolved memory leakage during sequential diffusion-to-audio workspace switches

```

---

### Version Beta .08-Vulkan-Cuda_stable — Universal Vulkan Runtime, AMD/Intel Support, Isolated Backend Staging & Prompt Streaming Hardening

Version Beta .08-Vulkan-Cuda_stable establishes an architectural milestone by evolving Repetere AI from an NVIDIA-only workspace into a hardware-agnostic workstation powered by dual **NVIDIA CUDA** and **Universal Vulkan** runtimes. It introduces segregated backend directory isolation (`bin/cuda/` and `bin/vulkan/`), eliminates the startup APU abort gate to welcome AMD Radeon and Intel Arc graphics adapters, hardens the prompt pipeline against Windows shell escaping faults, resolves neural audio synthesis path resolution, and enables instant, zero-downtime backend hot-swapping from the top menu bar.

```diff
+ Added Universal Vulkan compute backend support across all 5 production workspaces
+ Added dynamic [CUDA] <-> [VULKAN] runtime switch buttons directly in the top-level menu bar
+ Added segregated dual-backend runtime architecture: bin/cuda/ and bin/vulkan/ directory isolation
+ Added dedicated Vulkan sidecar staging: llama-server.exe, sd.exe (sd-cli.exe), and audiocpp_cli.exe with ggml-vulkan.dll
+ Added automated AMD Radeon, Intel Arc, and APU/iGPU detection and auto-routing in HardwareScanner.h
+ Added temporary file streaming (--prompt-file, --negative-prompt-file) in ImageStudioUI to eliminate shell argument truncations
+ Added isolated backend directory resolution in MusicStudioUI to enforce bin/vulkan/audiocpp_cli.exe execution
+ Added cooperative matrix shader acceleration (NV_coopmat2 / KHR_coopmat) bypassing Blackwell PTX JIT stalls
+ Added End User License Agreement (EULA.txt) covering beta rights, local privacy guarantees, and software terms
+ Added Inno Setup packaging updates bundling the complete Vulkan toolchain and license acceptance flow
! Fixed audio synthesis failures on non-NVIDIA/Vulkan configurations caused by missing Vulkan backend registrations
! Fixed shell parsing, quotation truncation, and newline stripping during multi-line image diffusion prompts
! Fixed process supervisor sidecar execution to guarantee clean Win32 Job Object containment across both backends
! Removed hardcoded APU startup abort gate, allowing unified memory systems to compute safely

```

---

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

1. 💻 **CODING (Interactive IDE):** Interactive split-view programming studio powered by Qwen 2.5 Coder checkpoints (7B, 14B, 32B Hybrid). Features line-numbered guttering, in-place AST diff patching (`SEARCH/REPLACE`), whitespace-tolerant snippet matching, manual editor injection, file loading/saving, and turn archiving. Supports both CUDA and Vulkan backends.


2. 💬 **CHAT (Conversational Assistant):** General instruct reasoning powered by Meta Llama 3.1 8B Instruct with multi-turn context serialization, safety-prompted context clears, and zero-downtime backend switching.


3. ✍️ **CREATIVE WRITING (Novelist Studio):** Uncensored long-form narrative workstation powered by Hermes 3 Llama 3.1 8B. Includes Lore Bible context injection, a 1 MB manuscript canvas with undo/redo snapshot history, directive action chips, and in-place prose patching.


4. 🎵 **AUDIO (MUSIC) Studio:** Full vocal and instrumental song synthesis powered by YuE2 3B weights (`yue2-3b-q4_0.gguf` / `yue2-3b-q8_0.gguf` + `yue2-vae-f16.gguf`). Features an 8,192-byte multiline lyrics buffer, structured tag parsing (`[Verse]`, `[Chorus]`), timeline synthesis up to 6 minutes (360s), CLI argument sanitization, and Win32 transport playback across CUDA and Vulkan.


5. 🎨 **IMAGES (Diffusion & Photoshop Studio):** Text-to-image and image-to-image canvas powered by FLUX.1 Schnell and SDXL Turbo via `sd.exe`. Includes dual positive/negative prompt buffers, steps/CFG tuning, resolution presets, companion encoder detection (`clip_l`, `t5xxl`, `ae`), in-place grading effects (brightness, contrast, saturation, filters), and low-memory project file browsing.



---

## 📖 Workspace User Guides: How to Use Each Tab

### ⚙️ Selecting Your Compute Backend & Compute Modes (CUDA vs. VULKAN | GPU vs. HYBRID)

Before generating in any workspace, you can verify or toggle your active compute settings in the top-right header strip:

* **Compute Backends:**
* **CUDA Mode:** Recommended for discrete NVIDIA GeForce RTX systems (RTX 30/40/50 series) for maximum raw throughput.


* **VULKAN Mode:** Recommended for AMD Radeon GPUs, Intel Arc graphics, high-RAM integrated APUs, or NVIDIA cards experiencing driver JIT compiler overhead.


* **Toggling Backends:** Simply click **[CUDA]** or **[VULKAN]** in the header. Repetere AI gracefully shuts down the running background sidecar and spins up the newly selected toolchain automatically.




* **Compute Modes:**
* **GPU Mode:** Locks execution entirely within dedicated VRAM for maximum speed and token throughput.


* **HYBRID Mode:** Spans model layers across host system RAM and GPU VRAM via dynamic layer splitting (`-ngl`). Works across **both CUDA and Vulkan**, allowing consumer cards with 8 GB–12 GB VRAM to load and execute heavier 14B and 32B models without Out-Of-Memory crashes.





---

### 🎨 IMAGES (Diffusion & Photoshop Studio)

The **IMAGES** tab generates high-fidelity local artwork via FLUX.1 Schnell or SDXL Turbo with companion diffusion encoders, featuring an in-place post-processing canvas.

* **Prerequisites:** Ensure `flux1-schnell-Q4_0.gguf` (or SDXL) and companion encoders (`clip_l`, `t5xxl_q4_k`, and `ae` in `.gguf` or `.safetensors` format) are installed via **Settings ➔ Repetere Models**.


* **Step-by-Step Workflow:**
1. Click the **IMAGES** tab in the main header. Confirm the header reads `PHOTOSHOP & DIFFUSION STUDIO (CUDA)` or `(VULKAN)`.
2. In the **Prompt** box, describe the subject, style, lighting, and composition (e.g., `a cybernetic falcon perched on a neon tower, 8k, cinematic lighting`). Multi-line prompts are fully supported.
3. *(Optional)* In the **Negative Prompt** field, specify elements to exclude (e.g., `blurry, bad anatomy, deformed wings`).
4. Select a **Resolution Preset** (e.g., `512x512 (Standard - Fast)`, `768x768`, `1024x1024`, `1280x720`).
5. Set your **Inference Steps** (`4` steps for Schnell) and **CFG Scale**.
6. *(Optional Image-to-Image / Canvas Load)* Click **Browse Image File...** under section 2 to import a reference image, or click **Load to Canvas**.
7. Click **Generate New Image**. The background engine parses the prompt file, streams live denoising telemetry (`Denoising step 1 of 4...`), and binds the completed render directly to the center OpenGL canvas quad.
8. **In-Place Photoshop Grading:** In Section 3, adjust sliders for **Brightness**, **Contrast**, and **Saturation**, or select filters like **Sepia**, **Color Tint**, or **Linear Gradient**. Click **Save Image to Files...** to export your final graded artwork.



---

### 💻 CODING (Interactive IDE)

The **CODING** tab operates as an integrated, two-pane live development environment powered by Qwen 2.5 Coder.

* **Workspace Layout:**
* **Left Pane (30%–38%):** Agent transcript, multi-turn reasoning logs, and directive input prompt.


* **Right Pane (62%–70%):** Live code editor canvas with line-number gutters and buffer controls.




* **Step-by-Step Workflow:**
1. Click the **CODING** tab.
2. To start fresh, type a directive into the prompt field (e.g., `create a multi-threaded thread pool class in C++`). To work on an existing file, click **Open...** in the right canvas toolbar to load your source file.
3. Click **Dispatch Diff** or press **Enter**.
4. The model streams changes formatted in `<<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE` AST patch blocks.


5. The in-place diff engine normalizes whitespace and merges code updates directly into the right-hand editor buffer.


6. *(Fallback Action)* If the model returns markdown code fences instead of a patch, click the **[Apply Response to Editor]** toolbar action to manually push completions into the live canvas.


7. Click **Save** or **Save As...** in the editor toolbar to commit the modified buffer to disk.



---

### ✍️ CREATIVE WRITING (Novelist Studio)

The **CREATIVE WRITING** workspace is an uncensored authoring desk powered by Hermes 3 Llama 3.1 8B, engineered for long-form narrative drafting, character tracking, and scene revisions.

* **Workspace Layout:**
* **Left Pane (Story Bible Drawer):** Local world-building notes, faction profiles, and character sheets.


* **Center Pane (Live Prose Canvas):** A 1 MB word-wrapped manuscript canvas equipped with line gutters, real-time word/character telemetry, and a 30-step undo/redo stack.


* **Right Pane (Directive Console):** Scene revision inputs, status logs, and quick style chips.




* **Step-by-Step Workflow:**
1. Click the **CREATIVE WRITING** tab.
2. In the left **Story Bible** panel, click **Browse Project Folder...** to point to a folder of your `.txt` or `.md` reference files. Toggle **Inject into Narrative Engine** (`autoInjectBible`) to seed your lore into the model's context.


3. Click **Open...** on the center canvas toolbar to load a chapter, or click into the manuscript canvas to draft directly.
4. Enter targeted scene revisions or passage continuation requests in the right pane (e.g., *"Make the pacing faster and emphasize sensory details of the storm"*).
5. Click quick preset chips such as **Sensory**, **Cadence**, or **Dialogue Pass** to pre-fill targeted stylistic directives.


6. Click **Dispatch Directive**. The narrative AST diff parser updates affected scenes directly within the center manuscript canvas.


7. Use **Undo** and **Redo** in the manuscript toolbar to step through snapshots, and click **Save** to write changes to disk.





---

### 🎵 AUDIO (MUSIC Studio)

The **AUDIO (MUSIC)** workspace synthesizes complete vocal and instrumental audio compositions up to 6 minutes (360s) via the YuE2 engine across CUDA or Vulkan.

* **Prerequisites:** Ensure both `yue2-3b-q4_0.gguf` (or `yue2-3b-q8_0.gguf`) and `yue2-vae-f16.gguf` (~265 MB) are present in `models/`.


* **Step-by-Step Workflow:**
1. Click the **AUDIO (MUSIC)** tab. Confirm the title displays `MUSIC PRODUCTION RACK (YuE2 CUDA)` or `(YuE2 VULKAN)`.
2. *(Optional Reference)* In the **Artist / Band Reference Style** field, enter reference artists (e.g., `Boston, Journey, Toto, classic 80s arena rock`).
3. In **Musical Style & Acoustic Tags**, specify genre, instruments, and acoustic properties (e.g., `Classic rock ballad, soaring vocal harmony, clean electric guitar solo, 95 bpm`).
4. In the **Song Lyrics & Structural Arrangement** buffer (supports up to 8,192 bytes), structure your lyrics using bracket tags:





```text
[Verse]
Code running clean through the silicon night
Vulkan shaders glowing bright
[Chorus]
Reclaim the compute, break through the screen
The sovereignty of the machine

```

5. Adjust the **Track Duration** slider (e.g., `30`–`60` seconds for quick tests, or up to `180`–`360` seconds for full tracks).
6. Click **[ Generate Full Song (With Vocals) ]**.
7. The system dispatches the verified backend binary (`bin/cuda/audiocpp_cli.exe` or `bin/vulkan/audiocpp_cli.exe`).


8. Once generated, status turns green (`Ready: track_name.wav`). Click **Play Master Audio** to trigger instant hardware playback via native Win32 `PlaySoundA`.



---

## 🚀 Quick Start: Installation & First Launch

1. Download **`RepetereAI-Setup-v0.9-Vulkan-Cuda_Hybrid-beta.exe`** from the Releases page.
2. Run the installer. Read and accept the **End User License Agreement (EULA)** outlining your local compute rights and beta terms.


3. The installer extracts cleanly into `%LOCALAPPDATA%\Programs\Repetere AI\` without requiring administrative privileges.


4. Launch **Repetere AI** via your Desktop shortcut or Start Menu.


5. Dismiss the startup splash screen by **clicking anywhere** or pressing any key.


6. The **Hardware Configuration Diagnostic** modal inspects your GPU adapters, VRAM, and system RAM, automatically selecting **CUDA** for discrete NVIDIA cards or **VULKAN** for AMD, Intel Arc, and APU configurations. Select your compute mode (**GPU** or **HYBRID**) and click **Confirm Hardware** to enter the workstation.



---

## 📦 How to Download & Manage AI Models

AI models are local weights that power each workspace. They must be present on disk before generation can proceed.

### Option A: In-App Model Downloader (Recommended)

1. In the top menu bar, click **Settings ➔ Repetere Models**.


2. Review the curated catalog and click **[ Download ]** next to your desired model:


* **Coding Workspace:** *Qwen 2.5 Coder 7B Instruct* (or *14B* / *32B* for Hybrid mode)


* **Chat Workspace:** *Meta Llama 3.1 8B Instruct*

* **Creative Writing Workspace:** *Hermes 3 Llama 3.1 8B*

* **Audio / Music Studio (Both Required):**
* `yue2-3b-q4_0.gguf` (or `yue2-3b-q8_0.gguf`)


* `yue2-vae-f16.gguf` (~265 MB)




* **Images Workspace:**
* `flux1-schnell-Q4_0.gguf` (Base diffusion model)


* Companion encoders: `clip_l.gguf`, `t5xxl_q4_k.gguf`, and `ae.gguf` (or `.safetensors` variants)






3. When finished, the status badge changes to green (**Installed**).

### Option B: Manual File Placement (Advanced)

Place `.gguf` or companion `.safetensors` weight files directly into your local application directory:

```text
%LOCALAPPDATA%\Programs\Repetere AI\models\

```

---

## 🎥 Video Demonstrations

* [https://youtu.be/EbnQngF_XS8](https://youtu.be/EbnQngF_XS8)
* [https://youtu.be/qtKOvZmqiTY](https://youtu.be/qtKOvZmqiTY)
* [https://youtu.be/hymrx6ZanV0](https://youtu.be/hymrx6ZanV0)

---

## 📸 Workspace Screenshots

---
<img width="2560" height="1528" alt="image" src="https://github.com/user-attachments/assets/9fe6f0d4-bbcf-4d90-b07b-4d31e551185d" />
<img width="2560" height="1528" alt="image" src="https://github.com/user-attachments/assets/04229026-f8d2-4e56-8509-f21bb0ff8454" />
<img width="2560" height="1528" alt="image" src="https://github.com/user-attachments/assets/97f689c6-86cd-4bc3-ae25-9fe93680ba32" />
<img width="2560" height="1528" alt="image" src="https://github.com/user-attachments/assets/67aa627e-6e1d-4298-9dfc-82e10431e24d" />
<img width="2560" height="1528" alt="image" src="https://github.com/user-attachments/assets/1aff029e-686c-4d35-a15c-70c4a71632e6" />

---

## 📜 License & Acknowledgments

Engineered by Nathaniel Richardson Jr. as part of the Repetere AI compute initiative. Distributed under the terms outlined in `EULA.txt`. Special thanks to the open-source contributors behind `llama.cpp`, `stable-diffusion.cpp`, `audio.cpp`, `Dear ImGui`, `GLFW`, and `YuE2`.

```

```
