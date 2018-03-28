## Installing CUDA

### Recommended Method

1. Download the `runfile (local)` from the CUDA website.
2. `ctrl + alt + f1` to switch to a tty.
3. Kill the X server with `sudo service lightdm stop`.
4. Make the cuda runfile executable `chmod +x <filename>.run`.
5. Run the file to install the toolkit: `sudo sh runfile`.
5. Follow the instructions to install CUDA. Make sure you **don't** install the CUDA OpenGL libraries when prompted unless you really need them (You can hit `q` to see the EULA accept prompt).
6. Restart the X server `sudo service lightdm restart`.
7. `ctrl + alt + f7` to switch back to GUI.
8. Add the following lines to your shell's "run commands" file (i.e. .bashrc for bash):

    ```
    export PATH=/usr/local/cuda/bin:$PATH
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
    ```

8. Restart the computer to make sure everything works.

### Alternative Method


### Weird Issues

- If the TTY1 does not show on hitting `ctrl+alt+f1` or if it shows a black screen, then simply set this `GRUB_CMDLINE_LINUX_DEFAULT="quiet splash usbcore.autosuspend=-1 nomodeset"` in the `/etc/default/grub` file. Make sure to run `sudo update-grub`.

- An issue that is being since since January 2018 on Ubuntu systems is that if you update your system to have the latest linux kernel headers (e.g. `4.4.0-116-generic`), then your Nvidia driver stops working, causing your system to either go into low graphics mode with reduced functionality, or not show the desktop at all.
The fix for this is to download version `390.42` of the Nvidia driver and install that. Note that on Nvidia's drivers website, you'll need to set your OS to Linux 64-bit (instead of Linux 64-bit Ubuntu 16.04 which is broken at the time of this writing) to get the link to the driver. 
To install, the process is:
    
    - Hit `Ctrl+Alt+F1`.
    - Stop the GUI daemon with `sudo service lightdm stop`.
    - Begin the driver installation `sudo sh NVIDIA-Linux-x86_64-390.42.run`.
    - Say yes to overwriting the previous driver.
    - If the installer complains about a GCC compiler mismatch (4.9 vs 5.x), run:
        ```
        sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 50
        sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 100
        ```
        This will set the compiler version to the latest 5.x series of GCC. In case the installer complains about another GCC version, you should be able to figure this out, else get someone else to help you.
    - When you get to the DKMS support screen, you should select `No`. Even though DKMS is desirable, for some unknown reason enabling DKMS support breaks the installation. Hopefully this is fixed in a future version.
    - The driver should be installed at this point. Run `nvidia-smi` to confirm and `sudo service lightdm start` to get back to your desktop.
    - You may need to reboot with `sudo reboot` but this is unlikely.


- Login loop: If you get an issue after the CUDA driver installation where you get kicked out each time you login, this is due to having installed the CUDA OpenGL libraries when installing the CUDA drivers. This is a known bug and you may need to google to see its current status.

- Sometimes disabling nouveau can help if your installation fails. To do so, 
    1. Go to a TTY and disable your X server (`sudo service lightdm stop`).
    2. Create the driver blacklist conf file: `sudo vi /etc/modprobe.d/blacklist-nouveau.conf`
    3. Add the following lines:

        ```
        blacklist nouveau
        options nouveau modeset=0
        ```
    4. Regenerate the kernel initramfs:
        `$ sudo update-initramfs -u`



## Install cuDNN

To install cuDNN, go to the [Nvidia CuDNN page](https://developer.nvidia.com/cudnn), register yourself and download the linux library (e.g. cuDNN v5.1 Library for Linux) for the appropriate CUDA version.

Now follow the below instructions:

1. Find the location of your CUDA install `which nvcc`.
2. Unzip the cuDNN tarball you downloaded above.
3. `cd` into the extracted folder.
4. Run the following commands:

        $ sudo cp -P include/cudnn.h /usr/local/cuda-8.0/include  # assuming you got /usr/local/cuda-8.0 from step 1
        $ sudo cp -P lib64/libcudnn* /usr/lib/x86_64-linux-gnu/
        $ sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*

You should now be able to run `make` or `cmake` and see the cuDNN installation being picked up.


## Hacks

- To get a history of processes on the GPU, run `sudo fuser -v /dev/nvidia*`. Useful for finding processes that aren't listed in `nvidia-smi` but are still occupying the GPU.