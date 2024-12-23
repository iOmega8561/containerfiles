# AirPlay Server
This image is based upon the official alpine container and packs an Open Source [AirPlay Server](https://github.com/FDH2/UxPlay)

Although it is definitely possible to run the mDNS server inside the container, the best case scenario is to bind-mount the host sockets to simplify the process of network discovery.

Assuming a user with uid=1000 and gid=1000, with podman's command-line this image can be run using the following command
```
podman run -it --rm \
    --network host \
    --userns=keep-id \
    -v $XDG_RUNTIME_DIR/pipewire-0:$XDG_RUNTIME_DIR/pipewire-0 \
    -v /run/dbus/system_bus_socket:/run/dbus/system_bus_socket \
    -v /tmp/.X11-unix:/tmp/.X11-unix:rslave \
    -e DISPLAY="$DISPLAY" \
    localhost/airplay-server:latest
```
