# Minimax-H3 Workflows

This directory contains ComfyUI workflows for the MiniMax H3 video generation model, organized by category/subfolder. 

*(it's been written by LLM so might have odd results but should give enough info, if you see any glaring errors let me know - Mark)*

---

## Root Folder Workflows

### MEDIT-Fast-Storyboard_MMH3-DMAD-Taomate-VEDA_v8.json
A fast storyboarding workflow optimized for quick iteration using the MiniMax H3 model. This version (v8, dated 20th October 2026) incorporates RefMod features and uses Taomate LoRA at 3 steps for initial generation with a second sampler at 6 steps. It experiments with various speedup LoRAs including VEDA (faster but quality hit), DMAD (layered with Taomate for quality improvement), and LightVAE (faster decoding). The workflow uses the reference model with shift_audio reduced to 2 to minimize metallic audio artifacts. Includes detailed notes on LoRA testing results and recommended settings for fast storyboarding on RTX 3060.

### MEDIT-Fast-Storyboard_MMH3_-DMAD-PDMD-VBVR_v18.json
An updated fast storyboarding workflow (v18, dated 29th October 2026) that significantly changes the LoRA stack for improved speed and quality. Key changes: uses Sol VAE in the first sampler only (halving encoding time while maintaining quality), increases second sampler to 3 steps, returns to the ref base model, uses VBVR LoRA at strength 1 for physics fixes, DMAD at 1.0, and replaces Taomate with PDMD 4-step at 0.5. Also includes Pika LoRA for dialogue audio in the second sampler. Removes VEDA and sol_attn due to quality concerns. Targets ~13 minutes for 15-second video at 0.8mp on RTX 3060 with Sol VAE.

### MEDIT-Higher-Quality-Storyboard_FastGen_v5.json
A higher-quality storyboarding workflow (v5, dated 9th November 2026) branched from the fast storyboard workflows, designed for mid-quality outputs intended to be passed through additional upscaler-detailer pipelines to reach 2mp+. Uses FlashGen 4-step v1 FL2VA pruned LoRA at strength 0.6 with 5 steps as the primary LoRA, with testing notes on Singularity v2, DRBaphs, and other LoRA combinations. Includes Power LoRA Loader for proper AdaLN handling. Documents extensive LoRA testing comparing ref2va base vs Singularity V2 for dialogue accuracy vs action quality.

---

## Bridge-2-Videos

### MBEDIT - AV Bridge_v10.json
An audio-video bridging workflow originally from Seitanism, for connecting two video clips using MiniMax H3. Loads two reference videos (Video A and Video B), encodes them to latent space, and generates a transition bridge between them. Uses MiniMaxH3ReferenceToVideo node with dual reference images, chunked feed-forward processing (4 chunks), low VRAM attention, and kitchen attention backend. Includes video/audio loading, VAE encoding/decoding, and CreateVideo output. Designed for seamless transitions between existing video clips with configurable resolution (default 864x480 / 0.4MP).

---

## Camera-Angles

### MBEDIT - H3_Cinematic_Multishot_Coverage_v3.json
A cinematic multi-shot coverage workflow that generates 8 static camera angles of the same scene from a single reference image. Uses a structured prompt system with subject definitions and eight hard-cut shots (wide, medium, close-up, over-shoulder, low-angle, high-angle, detail/insert, reverse). Implements a subgraph  Eight cinematic views that takes a source image and produces a contact sheet of 8 views plus selected outputs. Designed for creating consistent multi-angle coverage of a scene for storyboarding or pre-visualization, maintaining frozen world-state across all shots. This workflow is from Ethanfel.

---

## Masked-Inpainting

### MBEDIT - MH3-drozbay_inpainting_v3.1_v12.json
A masked inpainting workflow for MiniMax H3 based on the drozbay inpainting approach. Supports loading a reference video, creating masks for inpainting regions, and regenerating only masked areas while preserving the rest. Uses MiniMaxH3ReferenceToVideo with reference images, SetLatentNoiseMask for masking, and dual-sampler pipeline (first sampler for structure, second for detail). Includes VAE encoding for both video and audio, mask creation tools, and video output assembly. Designed for targeted edits like object removal, background replacement, or localized modifications.

---

## MMH3_Image-Editing

### MBEDIT - MMH3-QuintForms-image-creation-t2i-8k_v5.json
A text-to-image creation workflow using MiniMax H3 ref to video model at 8K resolution (7680x4320 / ~33MP) via the QuintForms approach. Uses FL2VA Minimax model with Qwen3VL 32B text encoder, MiniMaxH3TextToVideo node for image generation, and multiple LoRA loaders (PowerLoraStack for proper AdaLN handling). Includes ResolutionSelector for aspect ratio/megapixel control, KSampler with euler scheduler, and VAEDecode for output. Organized into Models, Sampling, Conditioning, and Decoding groups. Designed for high-resolution still image generation using the video model.

### MBEDIT - MMH3-Ryko_Image-edit_v3.json
An image editing workflow for single-shot image manipulation using MiniMax H3 video model (by Ryko from Discord). Uses FL2VA int8 model with dual VAEs (video and audio). Takes a source image and edit prompt to modify specific elements (hair color, object replacement, etc.). Generates 5 candidate images per run for selection. Includes detailed test notes: successfully changes hair via prompt (\change the hair of the woman on the left to be black with a bob cut\), but struggles with complex replacements like person-swapping between images. Uses MiniMaxH3TextToVideo with reference images for editing.

---

## MMH3_TTS

### MBEDIT- MMH3-Fast-audio-TTS-only_v7.json
A text-to-speech (TTS) only workflow using MiniMax H3 for audio generation without video. Version 7 (14th November 2026) removes speedup LoRAs and uses 25 then 30 steps for quality, taking ~4 minutes for 15 seconds on RTX 3060. Uses Qwen3VL 32B text encoder, MiniMaxH3TextToVideo configured for audio-only generation, dual samplers (first at 25 steps, second at 30), and VAEDecodeAudio for output. Includes detailed prompt structure with subject definitions for two speakers (S1, S2) with voice timbre references from audio files. Designed for packing dialogue without pauses for later editorial timing adjustment.

---

## Prompt-Creator

### MBEDIT-MiniMax-H3-1038lab_Promptor_v2.json
A prompt creation assistant workflow using the 1038lab MiniMax-H3-Promptor custom node (H3_PromptEditor). Helps structure complex MiniMax H3 prompts with subject definitions, shot breakdowns, retention analysis, and detailed descriptions. Includes example pre-prompts for controlling floral embellishment, static camera enforcement, and multi-speaker dialogue formatting. Provides template for 4-person webcam conversation scenarios with accent/voice specifications. Notes issues with local LM Studio integration and links to GitHub issues for improvements. Outputs formatted STRING prompt for use in generation workflows.

---

## Upscalers

### MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_v8.json
A pixel-space video upscaler using CKNPDX context windows for MiniMax H3. Uses MiniMaxH3ReferenceToVideo with reference images, MMH3LoopingSampler for chunked processing (136 frames per chunk, 22 overlap frames), and context window conditioning via MMH3CondSet/MM3HCondSelect. Implements ConditioningZeroOut for clean conditioning, ModelAttentionBackend with kitchen attention, and BasicScheduler with simple 12-step sampling. Designed for upscaling existing video to higher resolution while maintaining temporal consistency through overlapping chunks and context conditioning. Includes resolution reference table (0.2MP to 2.0MP at 16:9) and VRAM optimization notes for RTX 3060.

