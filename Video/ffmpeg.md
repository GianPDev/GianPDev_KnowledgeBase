

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

![[Transparent WebM Test.mp4]]
