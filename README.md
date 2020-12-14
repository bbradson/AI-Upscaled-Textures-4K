# AI-Upscaled-Textures-4K
Upscaled textures through AI for Rimworld. This repository is for 4x upscaled textures. The folders starting with "AI Upscaled Textures - " contain complete mods to use just like steam mods. Other folders only contain upscaled texture files for the relevant mod. To use those, copy-paste the texture folder into a working mod and activate. Dependencies, patches or edits to the About.xml are not necessary.

Most of the results are absolutely great, but please note that AI has its limitations, mainly on textures that are not very detailed.
This won't entirely transform the quality of textures designed by the talented artists of this community, but it will most of the time be a visible improvement when it comes to pixelated textures.

Workflow used to achieve this:

Initial upscaling is done with Waifu2x-ncnn-vulkan using the Waifu2x-Extension-Gui (https://github.com/AaronFeng753/Waifu2x-Extension-GUI)
The settings used there are:
image scale 2 or 4 depending on the source
image denoise level 3
waifu2x-ncnn-vulkan engine
cunet model
TTA enabled
tile size 128 or 256 depending on the source
and "replace original file" as additional setting, because the output path setting wouldn't keep subfolders

Sometimes, ~1% of the time, it'd also throw an error about a broken alpha level, which results in images with black background. Whenever this happens the specific images are remade with the caffe variant of waifu2x.
The Waifu2x-Extension-Gui shows errors for that happening in the log, and Waifu2x-caffe is used with similar settings to repeat the process for those images in the log.
https://github.com/lltcggie/waifu2x-caffe

Once upscaling is done and corrected, all images are compressed with pngyu, reducing their file size by roughly ~75% depending on their content.

Then, before uploading the finished mod, all useless files get removed, as the game would otherwise load them into RAM, even if it doesn't have to.
This includes PSDs, ZIPs, RARs, 7z, but also transparent dummy files, single-colored dummy files, as well as many other files where upscaling generally doesn't result in visible gains.
Note here, RAM usage of Rimworld does not equal file size. A single 5000x5000 transparent dummy file can use up half a gb of RAM just by existing, despite Windows showing a file size of a few bytes for the PNG.