# DESCRIPTION:  VLC media player container with its dependencies
# AUTHORS:      Jessie Frazelle <jess@linux.com>
# MODIFIER: Alexis Mathon <mathonal@gmail.com>
# USAGE:
#   #BUILD command
#   docker build -tag jess/vlc .
#
#   #Run Alias (defaut volume and workdir is under $HOME/Music/ )
#   docker run -d \
#       -v $HOME/Music/:$HOME/Music/ \
#       -w $HOME/Music/ \
#       -v /etc/localtime:/etc/localtime:ro \
#       --device /dev/snd \
#       --device /dev/dri \
#       -v /tmp/.X11-unix:/tmp/.X11-unix \
#       -e DISPLAY=unix$DISPLAY \
#       --name vlc \
#       jess/vlc
#
# Note : dockerfile nor modified from Jess image, just Run commands
# https://github.com/jessfraz/dockerfiles/blob/master/vlc/Dockerfile
#
FROM debian:bullseye-slim
LABEL maintainer "Jessie Frazelle <jess@linux.com>"

RUN apt-get update && apt-get install -y \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	vlc \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV HOME /home/vlc
RUN useradd --create-home --home-dir $HOME vlc \
	&& chown -R vlc:vlc $HOME \
	&& usermod -a -G audio,video vlc

WORKDIR $HOME
USER vlc

ENTRYPOINT [ "vlc" ]
