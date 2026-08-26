# USDU Ultimate SD Upscaler 

Any updates get announced via my YT channel - [https://www.youtube.com/@markdkberry](https://www.youtube.com/@markdkberry)

and Patreon (free) - [https://www.patreon.com/c/AIMakingMovies](https://www.patreon.com/c/AIMakingMovies)

Workflows: [https://github.com/mdkberry/comfyui_workflows](https://github.com/mdkberry/comfyui_workflows)

## 26th August 2026 (AEST)

*Moved this to the `workflows_by_model` folder from `workflows_by_use` folder to consolidate workflows into one place*

- **workflow updated**: `MBEDIT-USDU_HuMO_14B_vrs10.json`*added in resize method with auto scaling (width: 1920, height: 0)* 

---

## **13th August 2026 (AEST)**

**USDU HuMO**
	- This is actually very good and works even for lowVRAM but it takes ages. an 8 sec video resized to 1920 long edge on the way in will take 25 mins on my 3060 RTX when tiled at 2:3 ratio.
	- model links and node links are in the workflow. its old now, but I tested it with Minimax h3 and it was best at keeping consistency of faces but it does need the result to be fairly good already. This is just a polisher, not a big fixer.
	- inside the workflow is an LTX option but it never worked as well as HuMO so its all bypassed. Maybe LTX 2.5 will show better results in which case I might test it. However, I think this will eventually be superceded by LTX itself anyway once they release ref image control for character consistency. See my LTX model notes for how I can get to 3mp which offers better fix, albeit without consistency yet. 

---