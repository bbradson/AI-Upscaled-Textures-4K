# AI-Upscaled-Textures-4K
Upscaled textures through AI for Rimworld. This repository is for 4x upscaled textures. The folders in here contain complete mods to use just like steam mods, with those having 4K in their name including a loadfolders.xml for efficiently loading only what's actually used ingame, and the others not including said function. As a rule of thumb, either way, 4K textures require a certain amount of extra RAM. AUTOMATIC's high res textures mod is recommended for dds support to help with RAM and load times.

This AI upscaling generally yields fairly great results anyway, though something looking out of place isn't gonna get magically rimworldified, unfortunately.
If you're playing with Camera+, these textures should be sharp enough to not look pixelated or blurry when fully zoomed in on a 4K monitor.

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

Once upscaling is done and corrected, all images are compressed with pinga, reducing their file size by roughly ~75% depending on their content.
DDS files are generated using ImageMagick with a script I have in another one of my repositories. You just drop it in a folder with textures, run with powershell, and it'll do the job.

Then, before uploading the finished mod, all useless files get removed, as the game would otherwise load them into RAM, even if it doesn't have to.
This includes PSDs, ZIPs, RARs, 7z, but also transparent dummy files, single-colored dummy files, as well as many other files where upscaling generally doesn't result in visible gains, like masks for example.
Note here, RAM usage of Rimworld does not equal file size in the case of PNG files. Those always have to be fully decompressed by Rimworld before being loaded. As a result, a single 5000x5000 transparent dummy file can use up half a gb of RAM just by existing, despite Windows showing a file size of a few bytes for the PNG.
DDS files get loaded 1:1 as they are, which means they load quick and don't use as much RAM.