## Minimax H3 workflow update info

Any updates get announced via my YT channel - https://www.youtube.com/@markdkberry

and Patreon (free) - https://www.patreon.com/c/AIMakingMovies

---

### 15th August 2026 (AEST)

- renamed a previous workflow for clarity `MBEDIT - MH3_r2v_TurboLora_v26` *(was MBEDIT-MMH33_r2v_TurboLora_v26.json)*

#### **H3 Dual-Sampler Upscaler (best yet)**

*added workflow `MBEDIT - MH3_r2v_DualSampler_v12.json`*

**Example Videos** *(right click to download, < 6mb file size each)*:

[int8-1120x448-8secs-45mins mp4](example_videos/upscaler/int8-45mins-1120x448-8secs-45mins_MH3x2Smpl__00008-audio.mp4)

[w4a8-1280x512-8secs-55mins mp4](example_videos/upscaler/w4a8-55mins-1280x512-8secs-MH3x2Smpl__00009-audio.mp4)

*Both the above were from ref images into the H3 model 1st sampler set at those sizes then upscaled x1.5 between samplers in pixel space and run through the final sampler to produce final result. x4 ref images for characters and x1 for environment was used.* 

> This works using 2 samplers and the same H3 model for both. In between the samplers it comes out to pixel space, upscales x 1.5 using RTX NVDIA (or use your preferred upscaler, dont just resize it) and then passes it through the 2nd upscaler at low denoise. This is the best results I have seen so far, but it ooms very easily and takes 40 minutes or more to finish *(on my 3060 RTX 12 GB VRAM with 32 gb system ram)*. More info in the notes of the workflow. Use the w4a8 model to reduce ooms and get higher resolutions *(I can go in at 1280 x 512 x 8 seconds without oom takes 55 mins)*, or use int8 model for lower resolution but slightly better quality *(I use 1120 x 448 x 8 seconds takes 45 mins)*. I havent been able to decide which looks better, more tests needed. At this time it is the best I have achieved. One bonus is if you oom you can run the preview saved video through just the 2nd sampler using the same seed and it works fine, but for long-term solutions that is not ideal.

---

### 13th August 2026 (AEST)

`MBEDIT-MMH33_r2v_TurboLora_v26.json`

video on this is here https://www.youtube.com/watch?v=cTVXNlHqfAI

I am now using `comfyui kitchen attention` *(sage attention is disabled but nodes are in workflow as some find it faster, some not)*. If you can do it go for 2mp with Minimax H3 i2v. If you cant (I only get 5 seconds, any more ooms) then you may find faces at distance difficult to fix in r2v runs of Minimax. The video above also discusses the other methods I use (USDU and LTX) to fix face at distance issues when needed. It's still a wip.  


---

### 10th August (AEST) 2026

I was suggesting LTX as an upscaler before, but as of 10th August (AEST) 2026 I am suggesting trying to get to 2mp in Minimax H3 instead even with LowVRAM it can be done with short i2v videos. Then you keep the benefit of the power the model has to maintain accuracy of your ref image characters. 

See the video here https://www.youtube.com/watch?v=Os3yFgYHJ1Q for why I am now suggesting it and more info on the current workflow: `MBEDIT-MMH33_r2v_TurboLora_v12.json`
There are more methods in the pipeline I will share them as I know them and update this and the Patreon and YT channels with the information as soon as I know more. 



 
