# ActivityWatch setup for time tracking

* install main release .deb

    * https://github.com/ActivityWatch/activitywatch/releases

* remove xdg autostart

    ```
    sudo rm -rf /etc/xdg/autostart/aw-qt.desktop
    ```

## Additional stuff for wayland

* install gnome extension manager

    ```
    sudo apt install gnome-shell-extension-manager
    ```

* open extension manager and install focused window extension

    * Browse -> Search -> Focused Window D-Bus

* manipulate extension manifest to be compatible with installed gnome version

    * Check gnome version

    ```
    gnome-shell --version
    ```

    * Manipulate extension manifest

    ```
    vi .local/share/gnome-shell/extensions/focused-window-dbus@flexagoon.com/metadata.json
    ```

    * Logout/login; open extension manager to verify that the extension is active

* install aw-awatcher for afk & window tracking

    * https://github.com/2e3s/awatcher/releases

    * use `aw-awatcher_*.deb`, only the watcher, not the bundle

* check that aw-server and aw-awatcher is working

    ```
    /opt/activitywatch/aw-server/aw-server --verbose
    /usr/bin/aw-awatcher -vvv
    ```

## tmux

* install tmux plugin
    ```
    https://github.com/akohlbecker/aw-watcher-tmux?tab=readme-ov-file#install-the-aw-watcher-tmux-plugin
    ```

## Setup autostart
    
    * Create, test, and enable activitywatch service

    ```
    sudo cp activitywatch.service /etc/systemd/system/
    sudo service activitywatch start
    journalctl -u activitywatch
    sudo service activitywatch stop
    sudo systemctl enable activitywatch
    ```

    * Create desktop autostart for `aw-watcher`

    ```
    sudo cp aw-watcher.desktop /etc/xdg/autostart/
    ```

