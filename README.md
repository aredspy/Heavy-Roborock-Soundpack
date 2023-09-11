# Heavy Weapons Guy Soundpack for Roborock vacuums



https://github.com/aredspy/Heavy-Roborock-Soundpack/assets/106393710/05059d7b-8f91-4ebd-898d-7dc32149dd0a



This is a soundpack for rooted Roborock vacuums that allows you to change the default sounds to that of Heavy from TF2

This requires rooting your Roborock vacuum to gain access to the filesystem for modification.

Although the pack is designed for Roborock vacuums (tested on S5 max), it can be used on other vacuums with modifications (see modify section)

More info about how to root: [Devices](https://valetudo.cloud/pages/general/supported-robots.html), [FEL Rooting](https://valetudo.cloud/pages/installation/roborock.html)

Although Valetudo is not required, it is recommended due to its stability and ease of updating.

## Install

As of the 2023 Roborock firmware, the underlying system uses a read only compressed filesystem for media files known as SquashFS.
Presumably, Roborock does ths to save storage space. However, this means we can't easily modify the original files without making a new SquashFS system every time we want to change something.

(Partially thanks to Valetudo) there is plenty of space on the vacuum storage. We can instead simply bind mount the original soundpack location to a new writable directory [credit u/shompyblah for finding a safe bind](https://www.reddit.com/r/Roborock/comments/tfl9wd/comment/i0wipfm/?utm_source=share&utm_medium=web2x&context=3).

To install this soundpack:

1. SSH into the Roborock vacuum 
2. Create the directory `/mnt/data/voice`
3. Copy the soundpack into the new directory with `scp -r -O -i "~/.ssh/roborock" "Heavy/*" root@[ROBOROCK IP]:/mnt/data/voice
`
4. Add `mount -o bind /mnt/data/voice/ /mnt/resources/audio_custom/` to the `/mnt/reserve/_root.sh` file under the `VALETUDO_CONFIG_PATH` line (last line in the if statement)
5. Reboot to allow the mount bind to apply

Once you have setup the mount bind (steps 2,4,5), you will not need to do it again for any future changes like a different soundpack or your own custom sounds.

## Modify

Tp modify the soundpack (or even make your own), simply browse through the sound files and find what sounds you want to change. After finding a voice command or sound, get your own sound file and convert it to vorbis (.ogg) and replace the original file.
Then, simply run scp to overwrite with the new soundpack.

Example with ffmpeg: `ffmpeg -i Heavy_specialcompleted08.wav -acodec libvorbis zone.ogg`

If you would like to use this soundpack on a different vacuum brand, figure out where the sound files are installed and modify appropriately. Some vacuums may use a compressed format, so find details about their OS specs under Valetudo or other sources of info.
