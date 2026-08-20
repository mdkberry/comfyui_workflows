## Minimax H3 workflow update info

Any updates get announced via my YT channel - https://www.youtube.com/@markdkberry

and Patreon (free) - https://www.patreon.com/c/AIMakingMovies

---

### 20th August 2026 (AEST)

*Video explanation about the v2v refiner workflow described in the video*

**YT 15 min explainer video - "Minimax H3 - v2v Fixing Faces At Distance"** can be viewed here -  https://youtu.be/d1h5-E7NpuY

*Updated workflow: `MBEDIT - MH3_r2v_SingleSampler_Detailer_v16.json`* 

> The results of this workflow have been amazing, and I am using it to fix up all my previous clips using character refs. Best of all it's fast because 3 steps are enough (with Lightx2v lora), completing in 20 mins (on my 3060 RTX) for 5 secs, 8 secs, or even 10 seconds. I have to reduce the resolution to avoid oom as the clip length increases, making the final time the same in each case. My results come out between 1mp to 2mp depending on length, and have excellent face structure at those sizes. See the video explanation above for details. An example video clip is shared below on 17th August 2026 of the ballerina leaving a stage and kissing the woman on the cheek as she does so. This is by far the best refiner/detailer I have used to date. 

> Note: This workflow does not use latent upscaling, and tbh I probably wont bother testing that now since this works to the quality I need, while latent upscaling will probably need full steps run on it, making this workflow faster. I also mention in the above video about a stuttering problem discovered when "double sampler" is used with Minimax in the same workflow run. For some reason it works better if you save out to pixel space first (as a video clip), then run the entire thing again through a fresh start workflow.

**My video creation pipeline from this point on will be**:

1. Create a 480p video using any model (LTX, H3, Bernini, or other) - *takes 10 mins on average (3060 RTX)*.
2. Run the result through the above workflow upscaling to 1mp or 2mp depending onclip length - *takes 20 mins on average*.

The result from this are good enough as final clips. This makes it the fastest and highest qualty approach I have found to date, and all with ref image based character consistency.

(*Still to research and videos will be done on inpainting/masking to swap things, extending videos, and dialogue. All with Minimax H3 model*.)



---

### 18th August 2026 (AEST)

- updated workflow `MBEDIT - MH3_r2v_TurboLora_v27` *(v26 had Sampler to vae decode nodes unplugged that made it fail to run and wasnt obvious why)* 


---

### 17th August 2026 (AEST)

#### **H3 as a v2v detailer is giving astoundingly better results**

*new workflow: `MBEDIT - MH3_r2v_SingleSampler_Detailer_v11.json` added*

**Example video** *(right click to download, < 6mb file size)*:

**Bernini-clip_into-Minimax-0.4denoise-3steps_25mins**:

https://github.com/user-attachments/assets/d7802b22-7db8-4156-b36f-ddfc1aed74c7


*I havent shared the original Bernini clip only the result after detailing. The original clip was 832 x 480 and low res. I used good prompting and three ref images: x1 the first frame in high resolution, x2 ref character images.*

> With this workflow, I've ripped out the 1st sampler from the dual sampler workflow and just left the 2nd detailer sampler in. I am now using video clips created elsewhere (Bernini, LTX, Minimax, whatever...) and passing them through Minimax H3 as a v2v detailer. The results are amazing. This is by far the best detailer workflow I have tried. Notes in the workflow itself should give you enough to go on. I dont know why I didnt think of this before. Its also a lot faster as I can do less steps which also means more VRAM free to push slightly higher resolution. 



---

### 15th August 2026 (AEST)

- renamed a previous workflow for clarity `MBEDIT - MH3_r2v_TurboLora_v26` *(was MBEDIT-MMH33_r2v_TurboLora_v26.json)*

#### **H3 Dual-Sampler Upscaler (best yet)**

*added workflow `MBEDIT - MH3_r2v_DualSampler_v12.json`*

**Example Videos** *(right click to download, < 6mb file size each)*:

**int8-1120x448-8secs-45mins**:

https://github.com/user-attachments/assets/5637e696-9b9d-4194-a6bf-9243409b860d


**w4a8-1280x512-8secs-55mins**:



https://github.com/user-attachments/assets/5f88c687-840f-43ec-91ec-31952cc772e4



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



 
