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

## tmux-attached

* install aw-watcher-tmux-attached
    ```
    pip3 install aw-watcher-tmux-attached
    ```

## Setup autostart
    
* Create, test, and enable services

    ```
    mkdir -p $HOME/.local/share/systemd/user
    cp *.service $HOME/.local/share/systemd/user

    systemctl --user start activitywatch
    journalctl --user -u activitywatch
    systemctl --user enable activitywatch

    systemctl --user start aw-awatcher
    journalctl --user -u aw-awatcher
    systemctl --user enable aw-awatcher

    systemctl --user start aw-tmux-attached
    journalctl --user -u aw-tmux-attached
    systemctl --user enable aw-tmux-attached
    ```
