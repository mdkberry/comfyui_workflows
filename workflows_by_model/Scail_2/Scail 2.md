# SCAIL 2

first tests - July 2026

this is an amazing model. Wan based but useable in LTX too.

video discussing the workflow - https://www.youtube.com/watch?v=EARvvjztVDI

## My thoughts on Scail 2

- **I have tested it for motion transfer of a dancer, using padding to adjust the inbound video to match the ref image in order to place the dancer in the correct position on the stage.** Works amazingly well. I then upscale the result in LTX but the challenge is to keep the motion and fast body movement. I am working on an adapted LTX upscaler for this purpose but currently LTX tends to damage the dance motion or produce very dark results. so more work needed.

- **Where this is most exciting to me, is in lipsync and "actor" transfer when combined with LTX to upscale the results with the audio and lipsync.** The results from scail 2 even at 832 x 480 and 161 frames (16fps) produced relatively good facial control even if the lipsync mouth movement was weak. I then took that using ref image and v2v into LTX for dual sampler upscaling with audio of the lipsync driving it and got amazing results. Very realistic. excellent mouth movement. All I need now is acting skills, and mine are terrible.