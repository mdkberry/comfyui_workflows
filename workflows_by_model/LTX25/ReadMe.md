# LTX 2.5 Model

**14th August 2026 (AEST)**

**upscaler/detailer v2v workflow**

**workflow: `MBEDIT-v2v_LTX25_ResizeRefiner-w-SingleSampler_vXX.json`**

**Examples**:

[Original Minimax H3 video of ballerina](examples/upscale-refiner/MiniMax_H3_int8-best-2mp.mp4)

<video src="examples/upscale-refiner/MiniMax_H3_int8-best-2mp.mp4" controls width="100%"></video>

[Upscaled using the workflow in LTX25](examples/upscale-refiner/LTX25-Upscl__00010-audio.mp4)

<video src="examples/upscale-refiner/LTX25-Upscl__00010-audio.mp4" controls width="100%"></video>

*note: this workflow is a big mess because I was only testing settings and didnt plan to keep it. but those settings are informative which is why I share it here.*

I have only quickly tested this 2.5 model, and only for upscaler/refining v2v using low denoise.
the workflow shared is a big mess and a wip. It is taken from LTX 2.3 which it turns out you can almost straight swap the models from 2.3 with 2.5 and it works. 

One thing I did here is kept the 2.3 vae video model because currently it runs at half the speed of the 2.5 vae video model and the results look exactly the same. go figure. But by the time you use it maybe that is addressed.

I really only recommend using this workflow for checking the settings I used and building your own. I found LTX 2.5 needed lower denoise sigma starting at 0.5 (not 0.7 as I was using with 2.3). It also doesnt do the weird dimming that 2.3 does on low sigmas and steps.

Notice there is no spatial upscaler in this (its bypassed), I was resizing video in to 2304 on long edge effectively running at 3mp (I'd have gone for 4K but it oomed). Took about 17 mins for 8 second video on my 3060 RTX.

**RESULTS OF 2.5 as V2v upscaler/detailers** good consistency attempt, but not perfect. motion is still not great if fast, even with x2 temporal upscale which is enabled in the wf. there is a weird slight "oil painting filter" effect on everything, but I think it is because of using only one sampler, 4 steps, and low sigma start point. you could fiddle further with it, I wont because I am now going to wait for Minimax H3 to release their refiner/upscaler.

One good bit of news is Lightworks have promised a future release of ref image character control which is where Minimax H3 (and Bernini) lead the pack at this time.