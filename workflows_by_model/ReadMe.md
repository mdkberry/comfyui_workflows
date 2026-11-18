## WORKFLOWS BY MODELS README

Any updates get announced via my YT channel - [https://www.youtube.com/@markdkberry](https://www.youtube.com/@markdkberry)

and Patreon (free) - [https://www.patreon.com/c/AIMakingMovies](https://www.patreon.com/c/AIMakingMovies)

Workflows: [https://github.com/mdkberry/comfyui_workflows](https://github.com/mdkberry/comfyui_workflows)

---

### WHAT'S IN "WORKFLOWS_BY_MODELS" FOLDER

This folder will contain all workflows I am researching and testing currently. It will contain the most up-to-date versions. I'll add version number on the end of workflows. Previous versions will be found in `\superceded` folder for each model.

I'll `\archive` off models as they become unused by me and I stop research into them. I'll pull them back to this folder if that changes. I won't remove them completely as sometimes they come back to life or carry info worth revisiting.

More info can be found in the `ReadMe.md` of each model folder, which will be kept updated on changes and versions.


---

## UPDATES TO WORKFLOWS:

*I'll be posting workflow update info in this readme from now on (Nov 2026) - MB*

## 18th November 2026 (AEST)

1. **New workflow for higher quality Minimax H3 output:**

	- **1 hour video discussion on the workflows and making of "Sapphires Part 2"**: [https://youtu.be/SzfdZ8nfMi4](https://youtu.be/SzfdZ8nfMi4)

	- **6 min video of** [Sapphires Part 2 - "Second Victim"](https://youtu.be/5aFK6jr-PN4?si=Xwuoz_VJX-aAUREH)


	**Folder**: `Minimax-H3\`
	
	**new workflow**: `MEDIT-Higher-Quality-Storyboard_FastGen_vXX.json`
	
	*This is for making higher quality video clips. This is the same as the "fast storyboard" workflows but I have changed out the loras because I discovered later loras (dmad, pdmd, pika etc...) all damage character consistency. I didnt care much with parody creation but working on my higher quality projects it matters. So I tested all of them going back and I recommend using Loras that were created in the first few weeks of turbo loras being out. I use FlashGen here but early ones work better to keep consistency. This also helps me stay out of the endless "new turbo lora testing" frenzy.* 
	
	**Here is my current video pipeline workflow process using this workflow** in the first step for getting results.

	- **1st sampler, time taken to test the prompt to get it structured is about 6 mins per go at 0.4mp for a 15 second clip. (on 3060 RTX 12GB VRAM).**
	- **Then when its working, I let it run through the 2nd upscaling sampler to 1mp takes about 25 mins.**
	- **The second step I use the upscaler workflow (`MBEDIT - MH3-rv2v_PixelSpace-Upscaler-CtxtWndws_vXX.json`), v2v that result to 2mp takes another 25 mins (or 3mp if I really need it but takes longer).**
	- **then face fixing (pushing faces into the original video at 1mp) and so on, add the same time again, maybe longer depending on whats needed.**
	- All that just for a 15 second video clip!

2. **New SDR to HDR video converter workflow**:

	**Folder:** `workflows_by_model\AAA-Misc-Tools`
	
	**Workflow**: `MBEDIT - RTX-Video-To-HDR-convert_vXX.json`
	

	- **I tested this out and found it to be useful on shots that needed colou or exposure rescuing once I went into Davinci Resolve.** I used this on one shots from [Sapphires Part 2 "Second Victim"](https://youtu.be/5aFK6jr-PN4?si=Xwuoz_VJX-aAUREH)
	 at 01:29 the woman looking through the gate. It helped stop some issues in the original as I had some color problems in that shot that needed adjusting to match the others around it.
	 
	 - **The settings for output are set in the workflow as they are because its the only format that will work in the free version of Davinci Resolve.** *(If the price of GPU's ever comes back down I will buy DR as it is such a good tool)*.
	 

	
3. **Various workflows updated or new ones uploaded**:

	- **I'm switching all "resize nodes" in image pipeline workflows to use "lanczos" not "nearest-exact"** after discovering bad pixellation in the latter.
	
	- **A depthmap workflow has been added** to `workflows_by_model\AAA-Misc-Tools` I use it to blend depthmap and pose when fixing new camera POV and restyling an image, and talk about that in [this video](https://youtu.be/coFrX01h49M?si=p-C2IS9_4HorPcYY) .
	
	- **renamed my main Qwen 2.1 workhorse workflow** to `MBEDIT-QWEN-2.1_image-edit-i2i_vXX.json`
	
	- **Lots of testing with Z-Image i2i for fixing skin has taken place** and I updated the workflow with new model (int8 convrot) and new settings and info on what I have changed and why `MBEDIT-i2i-zimage_add-realism_vrsXX.json`
	
	- **Even my Klein workflow that I never touch got an update**, with the lanczos resize setting mentioned above, now its on, `MBEDIT-Klein_image_edit_9b_fp8_vrs24.json` 

---