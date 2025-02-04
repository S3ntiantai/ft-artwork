# ft-artwork (Raspberry Pi Album Art Display)

### As seen [on reddit](https://www.reddit.com/r/raspberry_pi/comments/ombwwg/my_64x64_rgb_led_matrix_album_art_display_pi_3b/) and featured [on raspberrypi.org](https://www.raspberrypi.com/news/raspberry-pi-displays-album-art-on-led-matrix/)

---

PowerShell script and modifications for the [Monstercat Visualizer Rainmeter skin](https://github.com/marcopixel/monstercat-visualizer) to send now playing album artwork to a running flaschen-taschen server. In my case, this allows displaying live album art from iTunes/Apple Music on a 64x64 rgb led matrix connected to my raspberry pi.

Files go in `C:\Users\<username>\Documents\Rainmeter\Skins\monstercat-visualizer\Song Information\Cover`

### Notes

* send-image is from the [flaschen-tachen](https://github.com/hzeller/flaschen-taschen/tree/master/client) project and may need to be compiled in your own WSL environment (my compiled version is included in case it just works)
* the powershell script executes the send-image command using WSL (version 1)
* if the skin shows album art for an alternative media player, it's compatible

![pi screenshot](screenshot.png)
![matrix screenshot](https://i.imgur.com/YwgyrJU.jpeg)


If you have modified the skin already or just want the changes to Cover.ini, here you go!

`[Rainmeter]` \
`OnRefreshAction=...[!CommandMeasure MeasureUpdateArt "Run"]`

`[MeasureUpdateArt]` \
`Measure=Plugin` \
`Plugin=RunCommand` \
`Program=PowerShell.exe` \
`Parameter=-ExecutionPolicy Bypass -Command ".\UpdateArt.ps1 [MeasureCover]"` \
`OutputType=ANSI` \
`DynamicVariables=1` \
`FinishAction=[!CommandMeasure MeasureUpdateArt "Run"]`
