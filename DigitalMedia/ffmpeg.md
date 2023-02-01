---
tags: [ffmpeg, video, transparency, webm, obs, transition, stringer, image]
---

### Compressing video and replacing audio and adding subtitles to webm
```powershell
ffmpeg -i input_video.mkv -i audio.flac -i webvtt_subs.vtt -c:s webvtt -c:v libvpx-vp9 -b:v 0 -c:a libvorbis -b:a 128k -crf 30 -map 0:v:0 -map 1:a:0 -map 2 output.webm
```
Can adjust `-b:a 128k` for audio bitrate and `-crf 30` for video quality (0-51), **lower is higher quality**
*note this doesn't allow subtitles on the browser, but if downloaded, allows subtitles on video player, subtitles in browser requires the subs to be separate and added via html or css (not 100% sure and haven't tested subs in browser)*

#### Creating transparent webm video from TRANSPARENT png image sequence (Can be used for OBS Transition Stingers)
```bash
ffmpeg -framerate 60 -f image2 -i %04d.png -c:v libvpx-vp9 -pix_fmt yuva420p output_name.webm
```

#### Check if video is actually transparent
1. Go to chrome/chromium based browser
2. Drag video to browser window
3. Change HTML background by adding this in `<body>`:
```css
style="background-color:#FF0000;"
```
Should look like:
```html
<body style="background-color:#FF0000;">
```
![[Transparent WebM Test.gif]]
![[Transparent WebM Test.mp4]]

### Make Twitter Video's Audio work (usually breaks when using avidemuxe or merging video and audio using ffmpeg)
```
ffmpeg -i input.mp4 -c:v libx264 -crf 22 -c:a aac -b:a 128k output.mp4
```

### Batch Convert .wav files to .flac
```powershell
ls *.wav | foreach-object { $newname = $_.Name.Remove($_.Name.Length - $_.Extension.Length) + ".flac"; ffmpeg -i "$_" -compression_level 0 $newname}
```

### Recursively convert from one format to another
*The example converts wav to flac*
Change extensions and ffmpeg line
```powershell
$getext = 'wav'; $setext = 'flac'; echo "converting .$getext to .$setext :"; dir "*.$getext" -Recurse; Start-Sleep -s 5; dir "*.$getext" -Recurse | foreach-object { $newname = $_.Directory.FullName + '\' + $_.Name.Remove($_.Name.Length - $_.Extension.Length) + ".$setext"; ffmpeg -i $_ -compression_level 0 $newname}
```