# DESCRIPTION: Run Audacity in a container
# AUTHORS: Jessie Frazelle <jess@linux.com>
# USAGE:
# docker build . -t jess/audacity
#
# docker run -d \
#		-v /etc/localtime:/etc/localtime:ro \
#		-v /tmp/.X11-unix:/tmp/.X11-unix \
#       -v $HOME/Music:$HOME/Music \
#		-e "DISPLAY=unix${DISPLAY}" \
#		-e QT_DEVICE_PIXEL_RATIO \
#		--device /dev/snd \
#		--group-add audio \
#		--name audacity \
#		jess/audacity
#
FROM debian:sid-slim
LABEL maintainer "Jessie Frazelle <jess@linux.com>"

RUN apt-get update && apt-get install -y \
	audacity \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "audacity" ]
