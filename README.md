# xdocker
A flexible system to run several work environments or desktop apps inside containers, based on archlinux

## Why?

I needed a way to run desktop applications and "self-contained work environments" (eg. for hardware projects), and wanted it flexible and seamless.
Some solutions already exists (x11docker, dx11...) but they didn't fit my needs, so i made xdocker.
Initially there was 2 systems, one for desktop applications, and one for hardware stuff, but they eventually merged into xdocker (the desktop part).

## Usual warning

* This was made for my own specific needs, so some patches to the script and configs may be needed
* This is based on archlinux images, and some options assume archlinux paths
* As usual, contributions are welcome :)

## Howto

* Build the xbase image (and tag it as `xbase`)
* * `docker build --no-cache -t xbase --build-arg user=$USER -f ./Dockerfile.xbase .`
* You can run it just by running xdocker (without any parameter)
* Build any image you want based on the xbase image, with the tag as `xdocker-$appname`
* Create a config file in `$XDG_CONFIG_HOME/xdocker/$appname` if you need options (see below)
* Create a config file `$XDG_CONFIG_HOME/xdocker/xdocker.rc` if you need custom options
* If needed, create .desktop files running `xdocker $appname` for desktop applications
* Or just run `xdocker $appname`

## Options

The options are bash scripts (so it is possible to, say, run a dmenu asking for variations, and set options conditionally) that set several variables:

* `OPTS_XORG` to pass the host Xorg to the container
* `OPTS_PULSE` to pass pulseaudio to the container
* `OPTS_DL` to pass `$HOME/Downloads` to the container
* `OPTS_CONFIG` to pass `$XDG_CONFIG_HOME` (.config) to the container
* `OPTS_DATA` to pass `$XDG_DATA_HOME` (.local) to the container
* `OPTS_DOCS` to pass `$HOME/Documents` to the container
* `OPTS_MOUNTS` to pass /mnt and /media to the container
* `OPTS_GPG` to pass GPG to the container
* `OPTS_PASS` to pass passwordstore to the container
* `DOCKER_ARGS` to pass custom docker flags
* `APP_CMD` to change the CMD and/or pass custom parameters

## Custom options

The custom options are set in the xdocker.rc file, and are in the form of `OPTION_NAME=(docker options)` (an example of that is in examples/), these options can be use the same way as the built-in ones
