# artis3n/pgmodeler

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/artis3n/pgmodeler-container?style=flat-square)](https://github.com/users/artis3n/packages/container/pgmodeler)
[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/artis3n/pgmodeler-container/Test?style=flat-square)](https://github.com/artis3n/pgmodeler-container/actions)
![GitHub last commit](https://img.shields.io/github/last-commit/artis3n/pgmodeler-container?style=flat-square)
![GitHub](https://img.shields.io/github/license/artis3n/pgmodeler-container?style=flat-square)
![GitHub followers](https://img.shields.io/github/followers/artis3n?style=social)
![Twitter Follow](https://img.shields.io/twitter/follow/artis3n?style=social)

Docker image wrapping [pgmodeler/pgmodeler][pgmodeler repo]. Unlike other containers I've seen for this project, this container is **_secure by default_**. There is no `--privileged` or any capabilities passed to the container. There is a non-root user. You get the graphical interface for PGModeler and can save project files to a specified volume for persistence.

Download from GitHub Container Registry or Docker Hub:

```bash
docker pull ghcr.io/artis3n/pgmodeler:latest
docker pull artis3n/pgmodeler:latest
```

## Usage

Run the container:

```bash
xhost +local:
docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix ghcr.io/artis3n/pgmodeler:latest
xhost -local:
```

| :exclamation: To persist your project data, be sure to mount a directory to `/app/savedwork` |
| --- |

```bash
xhost +local:
docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /persistent/local/directory/for/project:/app/savedwork ghcr.io/artis3n/pgmodeler:latest
xhost -local:
```

Then, while working in PGModeler, be sure to save your project files to `/app/savedwork`. Done!

### OSX Hosts

For OSX hosts, you have to install a Linux-compatible X11 server. The most common option is [XQuartz][].

The steps are:

1. `brew cask install xquartz`
1. `open -a XQuartz`
    1. Ensure XQuartz is running whenever you want to run this image.
1. XQuartz preferences -> Security -> check "Allow connections from network clients"
1. Make sure `/usr/X11/bin` is in your PATH
1. Set your `DISPLAY` appropriately

```bash
# Check to make sure your WiFi device is en0. If not, replace en0 with the appropriate device.
IP=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
# 'echo $IP' should show your IP address, e.g. 192.168.1.X
export DISPLAY=$IP:0
```

Now you can run the container with the regular instructions:

```bash
xhost +local:
docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -v /persistent/local/directory/for/project:/app/savedwork ghcr.io/artis3n/pgmodeler:latest
xhost -local:
```

[pgmodeler repo]: https://github.com/pgmodeler/pgmodeler
[xquartz]: https://www.xquartz.org/
