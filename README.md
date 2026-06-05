# 60mez - custom layout for Moergo Go60 keyboard

This repo offers a ZMK configuration of the MoErgo Go60 wireless split keyboard. It is a custom layout designed for a smooth transition for macOS traditional keyboard users, and it includes per-key RGB underglow for visual help (PR36 community firmware)

The layout has 5 layers:
- Layer 0 (Base Layer): The alphas and numbers and base symbols
- Layer 1 (Keypad Layer): Layer optimised for number data entry
- Layer 2 (Nav Layer): Navigation keys accessible via chording
- Layer 3 (Magic Layer): Access to Go60 control functions such as RGB and Bluetooth
- Layer 4 (Factory Test Layer): This layer is not used for normal typing; it is only for switch testing

To switch to Layer 1 (Keypad Layer), you can hold down RH T2 to temporarily switch into Layer 1, or double tap to persistently switch into Layer 1. You can single tap RH T2 to get back to the Layer 0 (Base Layer), or press LH C1R1.
To switch to Layer 2 (SymbolNav Layer), you can hold down LH T2 to temporarily switch into Layer 2, or double tap to persistently switch into Layer 2. You can single tap LH T2 to get back to the Layer 0 (Base Layer), or press LH C1R1.


## 📂 Resources

If you are looking to dig deeper into ZMK and develop new functionality, it is recommended to follow the steps of installing ZMK as found on the official ZMK documentation site (linked below).

- The [official MoErgo Go60 Support](https://moergo.com/go60-support) web site. Go60 documentation and other technical resources.
- The [official MoErgo Discord Server](https://moergo.com/discord). Instant conversations with other Go60 users.

- The [official ZMK Documentation](https://zmk.dev/docs) web site. Find the answers to many of your questions about ZMK Firmware.
- The [official ZMK Discord Server](https://discord.gg/8cfMkQksSB). Instant conversations with other ZMK developers and users. Great technical resource!

- The [official MoErgo ZMK Distribution](https://github.com/moergo-sc/zmk). Repository for ZMK firmware customized for Go60.

## 🚀 Getting started

1. Edit the keymap file(s) to suit your needs
2. Make sure `go60.conf` contains the following lines for per-key RGB underglow:
```
CONFIG_EXPERIMENTAL_RGB_LAYER=y
CONFIG_ZMK_RGB_UNDERGLOW_AUTO_OFF_IDLE=n
```
3. Commit and push your changes to your personal repo. Upon pushing it, GitHub Actions will start building a new version of your firmware with the updated keymap.
4. Click "Actions" in the main navigation, and in the left navigation click the "Build" link.
5. Select the desired workflow run in the centre area of the page (based on date and time of the build you wish to use). You can also start a new build from this page by clicking the "Run workflow" button.
6. After clicking the desired workflow run, you should be presented with a section at the bottom of the page called "Artifacts". This section contains the results of your build, in a .uf2 file.
6. Download the .uf2 file
7. Flash the firmware to both halves of your Go60 according to the user documentation.
8. Optionally, perform a Configuration Factory Reset on both halves.
9. Turn on RGB underglow using RGB_TOG (Magic + Y).
10. Cycle through RGB effects with RGB_EFF (Magic + H until the bottom modifier keys light up.


## 🎨 Defining RGB Scheme

RGB layers are defined in the Custom Device-tree of the keymap between the lines:

==== PER-KEY-RGB <section begins> ====
...
==== PER-KEY-RGB <section ends> =====

• The bindings parameter visually represents the LED layout
• ___ means the LED is OFF
• Colors: predefined names from zmk rgb_colors.h or any RGB hex code (e.g., 0x40E0D0 for turquoise)


## 🌈  RGB Features

HID Indicator Colors:
• &ug_nl COLOR_OFF COLOR_ON → NumLock
• &ug_cl COLOR_OFF COLOR_ON → CapsLock
• &ug_sl COLOR_OFF COLOR_ON → ScrollLock
• COLOR_OFF = indicator off
• COLOR_ON = indicator on

Battery Level Indicators:
• &ug_b2 BELOW ABOVE → <20%
• &ug_b4 BELOW ABOVE → <40%
• &ug_b6 BELOW ABOVE → <60%
• &ug_b8 BELOW ABOVE → <80%
• BELOW shows when battery is below threshold
• ABOVE shows when battery is above threshold

Fade-out Feature:
• fade-delay makes RGB layers fade out after a number of seconds
• -1 = layer stays on continuously
• Fade speed adjustable with RGB_SPI and RGB_SPD keys on Magic layer

## 💡 Extra Notes

• Active RGB layer always matches the highest active keymap layer
• RGB underglow uses battery; avoid permanent base-layer RGB for longer battery life
• Below 20% battery → RGB automatically turns off