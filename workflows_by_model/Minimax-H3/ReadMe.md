## Minimax H3 workflow update info

Any updates get announced via my YT channel - [https://www.youtube.com/@markdkberry](https://www.youtube.com/@markdkberry)

and Patreon (free) - [https://www.patreon.com/c/AIMakingMovies](https://www.patreon.com/c/AIMakingMovies)

Workflows: [https://github.com/mdkberry/comfyui_workflows](https://github.com/mdkberry/comfyui_workflows)

---

### 26th August 2026 (AEST)


**My video pipeline process is now the following**:


1. `MBEDIT - MH3-r2v_2Pass-LatentUpscaler_v5.json` 20 mins to get 8 second 16:9 video to 1mp. (20 mins)

Example of end result here (1mp):

https://github.com/user-attachments/assets/9abb2374-cef0-4647-8364-16498a3ac600




2. `MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_v3.json` to upscale the previous result to 2mp. It improves quality and is best I can get so far. (25 mins)

Example of final result here (2mp):



https://github.com/user-attachments/assets/f4e6968f-1d72-475a-b804-a885ada290ea



*Total time is about 45 minutes for 8 second video at 16:9 which is slow, but this is where it is at for 2mp quality at this time with Minimax H3. (on a 3060 RTX 12 GB VRAM, 32GB system ram using 5 ref images (x1 environment, x4 character sheets)*.

### 1. workflow update


*workflow update*: `MBEDIT - MH3-r2v_2Pass-LatentUpscaler_v5.json`

**Changes made**: *basic improvements to speed and quality. This will now serve as first step creation to 1mp in 2 sampler pass using ref images (x1 environment, x4 characters).*

> Changed light2xv lora to comfyui official one seemed to slightly improve quality, increased strength to 0.8. testing change of sampler and scheduler in 1st pass to euler/simple (was er_sde/beta) to make it faster, kept it at 8 steps. Reduced 2nd pass to 1mp (was 2mp) and 3 manual sigmas (was 5). this finished 8 seconds clip to 1mp (16:9) in 20 mins. Taek result to final run through context windows upscaler to polish eyes at 2mp. *(I'm still fighting speckleding eyes during motion at this time)*. Bypassed the chunk nodes seemed to do nothing. Less is more so leaving it that way. Looking at ways to speed this up while raising quality now. Removed "save video" and replaced it with "VHS Combine" node due to issues with file numbers not the same between png and mp4 output.

### 2. workflow update

*workflow update*: `MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_v3.json`


**Changes made:** *minimal changes to lora and video saving output node*.


> Changed light2xv lora to comfyui official one seemed to slightly improve quality on other workflow, increased strength to 0.8. Removed "save video" replaced with VHS Combine as not saving png workflow out properly named. Testing as basic 2mp upscale-polisher after running through 2pass latent upscaler to create 1mp. Adjusting settings to suit. Fighting minor issue with speckleding eyes still in final results. Kept settings as *er_sde, 0.75 start sigma, 2 steps* for now.

---

### 25th August 2026 (AEST)

**Today**: *updated context windows upscaler workflow, changed video output method*

**workflow update:** `MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_v2.json` 

> **Fixed issue with weak ref image use**.  switched out the "batch image" for "MMH3 Image List" node has resolved it. More tests with sigma settings, for dialogue scene got stronger results with Clownscheduler node set to 0.75 start_value, "simple" scheduler,  2 steps. Still using "er_sde" sampler. Changed video output to use newer method with png workflow save.




---

### 23rd August 2026 (AEST)

**Today**: *Upscaler workflows in pixels space and Latent Space. If you want the best, see #3.*


#### **1. FIXED DIALOGUE ISSUE IN V2V "PIXEL SPACE" UPSCALER WORKFLOW**:

*Takes around 25 mins for 8 sec dialogue scene, x5 ref images, output 1mp on a 3060 RTX (12GB VRAM)*

- *workflow renamed and updated to:* `MBEDIT - MH3_rv2v_PixelSpace_Upscaler_v18.json`

*(Note that this workflow was previously called "MBEDIT - MH3_r2v_SingleSampler_Detailer_v17.json" and the old version can be found in "\superceded" folder)*

**Changes in this update:** *It works for dialogue scenes now, but it isnt my preferred choice for upscaling dialogue scenes. It is best for fixing "faces at distance" where no mouth movement lipsync is required. The Latent Space upscaler (see #2) is stronger for dialogue scenes & lipsync upscaling. And #3 below is probably the best.* 

***FIXED: issue with dialogue lipsync mouth movement degrading when upscaling, is now resolved.***


*Notes on changes*:

> **Error found in the audio latent connection order** up to and including v17, `MBEDIT - MH3_r2v_SingleSampler_Detailer_v17.json`. It was pulling the audio latent from the H3 reference to video node (using the prompt) instead of the inbound video (video audio). This is now fixed and tested working with dialogue scenes. Adjust denoise to taste.

> **NOTE: if you have silent video inbound then you will need to provide audio of some kind for this worklow to function without error**. I have added in an audio loader node. Just use any mp3 of music or sound. If you prompt N/A in sound description it will use it, but if you prompt for some music it will likely use the prompt not the inbound audio.

#### **2. LATENT SPACE UPSCALER FOR DIALOGUE SCENES - DUAL PASS**:

*Takes around 30 mins for 8 seconds dialogue scene, , x5 ref images, output 1.4mp on a 3060 RTX (12GB VRAM).*

- **New workflow**: `MBEDIT - MH3-r2v_2Pass-LatentUpscaler_v1.json`

- **Custom node required:** uses https://github.com/LBH-123-AI/Comfyui_Minimax_h3_latent_Upscaler

*Notes on use*:

> This workflow adaptation was created to address dialogue issues in the "pixel space" upscaler/detailer *(which works now but has caveats for lowVRAM GPUs)*. This is a Latent Space upscaler. It requires character ref images and good prompting as a start point. This workflow runs through 2 samplers and does the upscaling before the second pass. Details on use are in the workflow. This workflow is better for dialogue scenes, as the results are stronger in early tests and I can get to 1.4mp for 8 second video clips on my 3060 RTX where I cannot get above 1mp on the pixel space upscaler for 8 sec long video clips with dialogue (with x4 character ref images).

#### **3. CKINPDX "PIXEL SPACE" UPSCALER WITH CONTEXT WINDOWS**: 

***Best Upscaler-Refiner I tested so far and fastest - I was able to upscale an existing 8 second dialogue video clip to 2mp in 26 minutes on a 3060 RTX.***

*This offers "context windows" plus an upscaling step, so splits longer videos in to multiple runs, thus reducing VRAM. This means higher resolution is possible with existing clips.* 

- **New workflow**: `MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_v1.json`

- **Custom node required:** I used only some of the nodes from https://github.com/ckinpdx/ComfyUI-MMH3Tools but if you have a good GPU I recommend using their workflows for optimum results.

*(NOTE: if you have a decent GPU then maybe try ckinpdx example workflows instead of mine, they use 5090 GPU in development. I have adapted from it taking only the parts I needed for it to work on my 3060 RTX 12GB VRAM)*.

> This was tested with 1824 x 736 video inbound and so only needed a refining pass. Being able to get to 2mp was the magic. I wasnt expecting it to be as fast as it was since it split the 192 frame run into 2 "chunks" or context windows and ran them both through the VRAM seperately. I havent tested longer than 8 second videos with it, but it should be good for it even to 2mp.


---

### 21st August 2026 (AEST)

**workflow update (info):** `MBEDIT - MH3_r2v_SingleSampler_Detailer_v17.json`

**Useage**: a refiner/detailer using v2v with low steps and low denoise to fix "faces at distance" using ref images for consistency, *(see notes from 20th August 2026 for more details on it).*
	
- **NOTE**: <span style="color: red;">***This workflow is great for visual shots but isnt working very well for dialogue shots, and will likely remove the mouth movements somewhat. So, I wont be using it for those at this time. If I find a solution I will update. Most dialogue shots I do close up anyway, so will have to find a solution that runs in the same workflow as they are created. This means I will likely now have to test a Latent Upscaler for dialogue shots, but will still use this workflow for non-dialogue video clips as it works well for fixing "faces at distance".***</span>


---

### 20th August 2026 (AEST)

*Video explanation about the v2v refiner workflow described in the video*

**YT 15 min explainer video - "Minimax H3 - v2v Fixing Faces At Distance"** can be viewed here -  https://youtu.be/d1h5-E7NpuY

*Updated workflow: `MBEDIT - MH3_r2v_SingleSampler_Detailer_v16.json`* 

> The results of this workflow have been amazing, and I am using it to fix up all my previous clips using character refs. Best of all it's fast because 3 steps are enough (with Lightx2v lora), completing in 20 mins (on my 3060 RTX) for 5 secs, 8 secs, or even 10 seconds. I have to reduce the resolution to avoid oom as the clip length increases, making the final time the same in each case. My results come out between 1mp to 2mp depending on length, and have excellent face structure at those sizes. See the video explanation above for details. An example video clip is shared below on 17th August 2026 of the ballerina leaving a stage and kissing the woman on the cheek as she does so. This is by far the best refiner/detailer I have used to date. 

> Note: This workflow does not use latent upscaling, and tbh I probably wont bother testing that now since this works to the quality I need, while latent upscaling will probably need full steps run on it, making this workflow faster. I also mention in the above video about a stuttering problem discovered when "double sampler" is used with Minimax in the same workflow run. For some reason it works better if you save out to pixel space first (as a video clip), then run the entire thing again through a fresh start workflow.

**My video creation pipeline from this point on will be**:

1. Create a 480p video using any model (LTX, H3, Bernini, or other) - *takes 10 mins on average (3060 RTX)*.
2. Run the result through the above workflow upscaling to 1mp or 2mp depending on clip length - *takes 20 mins on average*.

The result from this are easily good enough as final clips. This makes it the fastest and highest qualty approach I have found to date, and all with ref image based character consistency.

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



 
