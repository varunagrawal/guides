## Installing CUDA

### Recommended Method

1. Download the `runfile (local)` from the CUDA website.
2. `ctrl + alt + f1` to switch to a tty.
3. Kill the X server with `sudo service lightdm stop`.
4. Run the runfile as `chmod +x runfile && sh runfile`.
5. Follow the instructions to install CUDA. Make sure you **don't** install the CUDA OpenGL libraries when prompted unless you really need them.
6. Restart the X server `sudo service lightdm restart`.
7. `ctrl + alt + f7` to switch back to GUI.

### Alternative Method


### Weird Issues

- If the TTY1 does not show on hitting `ctrl+alt+f1` or if it shows a black screen, then simply set this `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.autosuspend=-1 nomodeset"` in the `/etc/default/grub` file.

- Login loop: If you get an issue after the CUDA driver installation where you get kicked out each time you login, this is due to having installed the CUDA OpenGL libraries when installing the CUDA drivers. This is a known bug and you may need to google to see its current status.