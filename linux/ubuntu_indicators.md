## Useful Menu Bar Indicators for Ubuntu

- Multiload Indicator 

        sudo add-apt-repository ppa:indicator-multiload/stable-daily
        sudo apt-get update
        sudo apt-get install indicator-multiload

Open in Menu. Go to `preferences` to update color scheme.

- Calendar Indicator

        sudo add-apt-repository ppa:atareao/atareao
        sudo apt-get update
        sudo apt-get install calendar-indicator

Open calendar-indicator from the Menu

- FluxGui

        # Install dependencies
        sudo apt-get install git python-appindicator python-xdg python-pexpect python-gconf python-gtk2 python-glade2 libxxf86vm1

        # Download xflux-gui
        cd /tmp
        git clone "https://github.com/xflux-gui/xflux-gui.git"
        cd xflux-gui
        python download-xflux.py

        # EITHER install globally
        sudo python setup.py install
        # EXCLUSIVE OR, install in your home directory. The binary installs
        # into ~/.local/bin, so be sure to add that to your PATH if installing locally.
        python setup.py install --user

        # Run flux
        fluxgui &


- Pomodoro Technique Indicator

        sudo add-apt-repository ppa:atareao/atareao
        sudo apt-get update
        sudo apt-get install pomodoro-indicator

Open in Menu.

