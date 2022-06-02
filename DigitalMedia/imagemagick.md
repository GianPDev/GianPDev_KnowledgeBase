
#### Convert image sequence to gif with transparent background
```bash
magick convert -resize 256x256 -delay 1x24 -dispose Background *.png anim-nodelayset256x.gif
```

