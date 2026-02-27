<p align="center">
  <img src="https://img.shields.io/badge/ComfyUI-Wan2.1-blueviolet?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xOCA0bDIgNGgtM2wtMi00aC0ybDIgNGgtM2wtMi00SDhsMiA0SDdsLTItNEg0YTIgMiAwIDAwLTIgMnYxMmEyIDIgMCAwMDIgMmgxNmEyIDIgMCAwMDItMlY0aC00eiIvPjwvc3ZnPg==" alt="ComfyUI Wan2.1"/>
  <br/>
  <img src="https://img.shields.io/badge/Google%20Colab-Free%20Tier-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Colab"/>
  <img src="https://img.shields.io/badge/GPU-NVIDIA%20T4-76B900?style=for-the-badge&logo=nvidia&logoColor=white" alt="T4"/>
  <img src="https://img.shields.io/badge/VRAM-15GB-informational?style=for-the-badge" alt="VRAM"/>
</p>

<h1 align="center">🎬 ComfyUI + Wan2.1 — AI Video Generation on Google Colab</h1>

<p align="center">
  <strong>Generate AI videos for free using Wan2.1 models on Google Colab's T4 GPU.</strong><br/>
  Text-to-Video &bull; Image-to-Video &bull; IP-Adapter Face Preservation &bull; No NSFW Filters
</p>

<p align="center">
  <a href="https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/ComfyUI_Wan21_Video.ipynb">
    <img src="https://img.shields.io/badge/Open%20in-Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white" alt="Open In Colab"/>
  </a>
</p>

---

## ✨ Features

| Feature | Description |
|---|---|
| 🎥 **Text-to-Video** | Generate video clips from text prompts using Wan2.1-T2V-1.3B |
| 🖼️ **Image-to-Video** | Animate still images with Wan2.1-I2V-1.3B |
| 👤 **IP-Adapter** | Preserve faces/style from input images during animation |
| ☁️ **Cloudflare Tunnel** | Access ComfyUI's full web UI from your browser |
| 💾 **Google Drive** | Persist models (~14GB) across sessions — download once |
| 🔧 **Fully Automated** | API-driven generation — no manual node wiring needed |
| 📦 **MP4 / WEBP / GIF** | Multiple output formats via VideoHelperSuite + ffmpeg |

---

## 🧠 Models

| Model | Format | Size | Purpose |
|---|---|---|---|
| `wan2.1_t2v_1.3B_fp16` | FP16 | ~2.6 GB | Text → Video diffusion |
| `wan2.1_i2v_480p_1.3B_fp16` | FP16 | ~2.6 GB | Image → Video diffusion |
| `umt5_xxl_fp8_e4m3fn_scaled` | FP8 | ~5.0 GB | Text encoder (UMT5-XXL) |
| `clip_vision_h` | FP16 | ~3.9 GB | CLIP Vision (for I2V) |
| `wan_2.1_vae` | FP32 | ~300 MB | VAE decoder |
| `ip-adapter-plus-face_sdxl_vit-h` | — | ~850 MB | IP-Adapter face model |

> **T2V total: ~8 GB** &nbsp;|&nbsp; **T2V + I2V + IP-Adapter: ~15.3 GB**

---

## 🚀 Quick Start

```
1️⃣  Mount Google Drive (optional — saves models between sessions)
2️⃣  Install ComfyUI + dependencies
3️⃣  Install custom nodes (WanVideoWrapper, GGUF, VideoHelperSuite, IPAdapter)
4️⃣  Download Wan2.1 T2V models (~8 GB)
5️⃣  Launch ComfyUI with Cloudflare tunnel
6️⃣  Generate Text-to-Video via API
```

### For Image-to-Video:
```
4b  Download I2V models (~6.5 GB extra)
4c  Download IP-Adapter model (~850 MB, optional)
7️⃣  Generate Image-to-Video via API
```

> Run cells in order. Cell 5 stays running — execute cells 6 or 7 in parallel.

---

## ⚙️ Recommended Settings (T4 GPU)

| Parameter | Value | Notes |
|---|---|---|
| **Resolution** | `480×320` | Max for T4 — higher causes OOM |
| **Frames** | `33` (2s) or `49` (3s) | Must be `4n+1`: 5, 9, 13, 17, 21, 25, 29, 33, 49, 65 |
| **Steps** | `25` | Good speed/quality balance |
| **Sampler** | `euler` or `uni_pc` | UniPC faster, Euler better quality |
| **Scheduler** | `normal` | Recommended for Wan2.1 |
| **CFG** | `5.0 – 7.0` | 6.0 is the sweet spot |
| **FPS** | `16` | Wan2.1 was trained at 16fps |
| **IP-Adapter Weight** | `0.5 – 0.8` | Higher = more faithful to image, less motion |

---

## 📂 Project Structure

```
├── ComfyUI_Wan21_Video.ipynb    # Main Colab notebook (all-in-one)
├── image_to_video_wan.json       # ComfyUI I2V workflow (for manual use in UI)
└── README.md
```

---

## 🔧 Custom Nodes Included

| Node | Author | Purpose |
|---|---|---|
| [ComfyUI-WanVideoWrapper](https://github.com/kijai/ComfyUI-WanVideoWrapper) | kijai | Advanced Wan2.1 control, LoRA, GGUF, I2V |
| [ComfyUI-GGUF](https://github.com/city96/ComfyUI-GGUF) | city96 | Load quantized GGUF models |
| [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite) | Kosinkadink | Save output as MP4/GIF with ffmpeg |
| [ComfyUI_IPAdapter_plus](https://github.com/cubiq/ComfyUI_IPAdapter_plus) | cubiq | IP-Adapter for face/style preservation |

---

## 🎯 T4 Optimization Flags

The notebook launches ComfyUI with flags optimized for the T4's 15GB VRAM:

```bash
python main.py --listen 0.0.0.0 --port 8188 \
    --lowvram \
    --disable-smart-memory \
    --preview-method auto
```

| Flag | Purpose |
|---|---|
| `--lowvram` | Offloads models to CPU when not in use |
| `--disable-smart-memory` | Prevents caching models that don't fit in VRAM |
| `--preview-method auto` | Real-time preview during generation |

---

## 📋 Tips & Troubleshooting

- **Prompts in English** work best with Wan2.1
- **Generation takes 10–30 min** per clip on T4 — this is normal
- Videos are saved to `/content/ComfyUI/output/`
- If you get **OOM errors**, try reducing resolution or frames
- For the text encoder, you can use the **GGUF Q4_K_M** variant (~2.5GB) via ComfyUI-GGUF
- After downloading new models (cells 4b/4c), **restart ComfyUI** (stop and re-run cell 5)
- The Cloudflare tunnel provides a **public URL** — share it to access ComfyUI from any device

---

## 📜 License

This notebook is provided as-is for educational and personal use. The models and custom nodes are subject to their respective licenses:

- **Wan2.1** — [Alibaba / Wan Team](https://huggingface.co/Comfy-Org/Wan_2.1_ComfyUI_repackaged)
- **ComfyUI** — [GPL-3.0](https://github.com/comfyanonymous/ComfyUI/blob/master/LICENSE)
- **IP-Adapter** — [Apache 2.0](https://github.com/tencent-ailab/IP-Adapter)

---

<p align="center">
  <sub>Made with ❤️ for the AI video generation community</sub>
</p>
