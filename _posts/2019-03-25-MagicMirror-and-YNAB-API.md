---
published: false
---
Finally had some time at home today to just tinker. Broke out the [Magic Touch 10in Touchscreen](https://www.mimomonitors.com/products/mimo-magic-touch) and got it working with a [Raspberry Pi 3](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/). Luckily, Mimo had an excellent [guide](https://www.mimomonitors.com/pages/using-our-usb-displays-with-the-raspberry-pi-3) for setting up their monitors with a RPi3.

Followed along with this for a bit until I couldn't for the life of me persist the "Coordinate Transformation Matrix" (needed to calibrate the touchscreen input appropriately). I could run a command after boot and it worked fine but no persistence. After some Google Fu involving Linux exorg and determining Device Vendor, I used [this stackexchange](https://unix.stackexchange.com/questions/58117/determine-xinput-device-manufacturer-and-model) to get the answer I needed.

Lo-and-behold! The touchscreen settings now persist after reboot.

The next step was to install MagicMirror on my RPi3. SUPER EASY, since the author put a [RPi3 Section](https://github.com/MichMich/MagicMirror#raspberry-pi) in his README.md. Got it installed and running but it only runs on the primary monitor (HDMI output) so I'll have to do some more tinkering later to have it auto-boot onto my touchscreen display.

End goal is to have a Google calendar HUD for the family and use the [YNAB API](https://api.youneedabudget.com/) to populate some data regarding out family budget at a glance.

 ## Update 2019-03-26
Just had to change some things in /etc/X11/xorg.conf - Per the guides above, in the "ServerLayout" for the screens, it had "HDMI" set as Screen 0. By telling it to set "UGA" as Screen 0 and setting HDMI as Screen 1, we now have the main task bar on our tiny touchscreen. That got the display to be primary but now the touchscreen calibration is off. We have to adjust the "Coordinate Transformation Matrix" again.

Let's look at that:

We have a 24in monitor that I've set to have a static (static should make this stick across setups) resolution of 1280x720 and a 10in touchscreen with 1024x600.

According to (https://wiki.archlinux.org/index.php/Calibrating_Touchscreen)[this helpful wiki entry] we need to calculate a matrix of c0 0 c1 0 c2 c3 0 0 1 using 
            
```
c0 = touch_area_width / total_width
c2 = touch_area_height / total_height
c1 = touch_area_x_offset / total_width
c3 = touch_area_y_offset / total_height
```
For my setup:
```
c0 = 1024 / 2304 ~= 0.44444
c2 = 600 / 720 ~= 0.83
c1 = 1280 / 2304 ~= 0.55555
c3 = 0 / 720 = 0
```

This got the calibration we needed. Onto implementing and changing up the MagicMirror itself!

## Update 2019-03-27

Had to install xscreensaver on the RPi to make it stop blanking itself after 10-15min. That was simple. Then, finally got it running! Linked up the family calendar and put nice things to know.            
	![Display image](https://www.dropbox.com/s/0s2wf5voaa42cfy/2019-03-27%2021.14.21.jpg?raw=1)

Time to start writing my own module!
