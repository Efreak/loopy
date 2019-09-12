# Looping videos

Looping videos. Like [leekspin](leekspin). Or Caramelldansen (tbd).

### How to download crap from crunchyroll (leekspin is ep2 of bleach at around 13:30)

```
# download file with seiya-dev/crunchyroll-downloader-nx
nvs add current
nvs use current
npm install -g seiya-dev/crunchyroll-downloader-nx

mkdir tmp
cd tmp

npm link crunchyroll-downloader-nx
node node_modules/crunchyroll-downloader-nx/crunchy.js --search bleach
node node_modules/crunchyroll-downloader-nx/crunchy.js -s 19324 -e 2 --skipmux
cd ..
```

# How to convert files using ffmpeg.
```
# Step 1: extract the necessary frames from your video file
# in example, I'm removing 150 frames starting at 13:29, and saving them as thumb####.png. 
ffmpeg -i "tmp/[CR] Bleach Season 1 - 02 [480p].ts" -ss 00:13:29.000 -vframes 150 tmp/thumb%04d.png

# Step 2: edit your images if necessary.
#   Cropping can be done by ffmpeg (see the -filter:v "crop...)

# Step 3: convert the images back into a video. Use high quality, because it looks better (crf). If your video is much longer, decrease the crf number. If you want to try lossless vp9, replace `-b:v -crf 20` with `-lossless 1`. I used handbrake to try and shrink it more
ffmpeg -framerate 29.7 -pattern_type sequence -start_number 102 -c:v png -f image2 -i tmp/thumb%04d.png -filter:v "crop=460:430:196:0" -c:v libvpx-vp9 -b:v 0 -crf 20 -framerate 29.7 -pix_fmt yuv420p out.webm
# now delete intermediate files
rm -rf tmp
```
## TODO:
Caramelldansen
Another leekspin: https://www.youtube.com/watch?v=c17xydS2vgU
leekspin: get net frames, mouth doesn't move
