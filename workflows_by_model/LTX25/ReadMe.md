# LTX 2.5 Model

Any updates get announced via my YT channel - https://www.youtube.com/@markdkberry

and Patreon (free) - https://www.patreon.com/c/AIMakingMovies

---

### 15th August 2026 (AEST)

#### Updated LTX2.5 Upscaler/Detailer workflow to vrs6

*Workflow: `MBEDIT-v2v_LTX25_ResizeRefiner-w-SingleSampler_vrs6.json`*

- **Summary**: *Improved end result in vrs6 by switching "resize" node for "upscaler" node on way in*

**Example videos** *(right click to download, < 6.5 mb file size each)*:

**H3 example that was used to test this workflow**:

https://github.com/user-attachments/assets/bed83e17-8bff-41c4-84e1-58d50dd25828


**Result after it passed through this workflow**:


https://github.com/user-attachments/assets/bdccebc7-4713-418c-a082-6face02b2960


> I ran an 8 second video from H3 through this vrs6 workflow, and it completed at 3mp in 18 minutes on my 3060 RTX. *(Compared to 45 mins using H3 dual-sampler upscaler (about to be released today too))*. Inbound video was 1824 x 736 x 8 seconds from H3. The result through this LTX upscaler workflow can be seen in the 2nd video linked above.

**Changes in vrs6 of this workflow**:

- I updated the upscaler to use RTX NVidia instead of using resize. I realised resize at 3 mp was causing small pixel tiling to be observed as it was such a big leap from inbound video size. So use an upscaler not a resize node for this workflow. It works better. See the example.

- I also tidied it up from previous version and removed unneeded nodes. It is now strictly a 3mp *(or try 4K if you can do it)* upscaler for v2v. It is actually pretty good.

- LTX let down is the motion, else it would maybe be my upscaler of choice due to speed, but having just tested H3 dual-sampler for upscaling I will probably use that for finals despite lenght it takes to complete. But this LTX workflow is very fast, so it has that going for it!




---

### **14th August 2026 (AEST)**

#### Released LTX2.5 Upscaler/detailer v2v workflow (vrs5)

*workflow: MBEDIT-v2v_LTX25_ResizeRefiner-w-SingleSampler_vrs5.json*

**Example Videos** *(right click to download, < 5mb file size each)*:

[Original Minimax H3 video of ballerina](examples/upscale-refiner/MiniMax_H3_int8-best-2mp.mp4)


https://github.com/user-attachments/assets/0725e8ec-3b2a-4a8e-a793-473e738e4ca2

[Upscaled ballerine H3 v2v using the workflow in LTX25](examples/upscale-refiner/LTX25-Upscl__00010-audio.mp4)


https://github.com/user-attachments/assets/b4093e0e-4c74-4662-8202-5920f76b8346


*(NOTE: this workflow is a big mess because I was only testing settings and didnt plan to keep it. but those settings are informative which is why I share it here.)*

I have only quickly tested this 2.5 model, and only for upscaler/refining v2v using low denoise. The workflow shared is a big mess and a wip. It is taken from LTX 2.3 which it turns out you can almost straight swap the models from 2.3 with 2.5 and it works. 

One thing I did is kept the 2.3 vae video model because currently it runs at half the speed of the 2.5 vae video model and the results look exactly the same. go figure. But by the time you use it maybe that is addressed.

I only recommend using this workflow for checking the settings I used, and building your own. I found LTX 2.5 needed lower denoise sigma starting at 0.5 (not 0.7 as I was using with 2.3). It also doesnt do the weird dimming that 2.3 does on low sigmas and steps.

Notice there is no spatial upscaler in this (its bypassed), I was resizing video in to 2304 on long edge effectively running at 3mp (I'd have gone for 4K but it oomed). Took about 17 mins for 8 second video on my 3060 RTX.

**RESULTS OF 2.5 as V2v upscaler/detailers**:

> Good consistency attempt, but not perfect. Motion cohesion is still not great if fast movement, even with x2 temporal upscale. There is a weird slight "oil painting filter" effect on everything, but I think it is because of using only one sampler, 4 steps, and low sigma start point. You could fiddle further with it to improve results, I wont because I am now going to wait for Minimax H3 to release their refiner/upscaler.

One good bit of news is Lightworks have promised a future release of ref image character control which is where Minimax H3 (and Bernini) lead the pack at this time.
