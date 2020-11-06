# DESCRIPTION: Run gimp in a container
# AUTHORS: Jessie Frazelle <jess@linux.com>
# MODIFIER: Alexis Mathon <mathonal@gmail.com>
# USAGE:
# docker build . -t jess/gimp
#
# docker run -d \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	-v $HOME/Pictures:/root/Pictures \
#	--name gimp \
#	jess/gimp
#
# note : same image as jess image
# https://github.com/jessfraz/dockerfiles/blob/master/gimp/Dockerfile
#
# there is a problem with icones at launch
# go to edit >> prefrences >> icons themes >> select legacy
#
FROM debian:bullseye-slim
LABEL maintainer "Jessie Frazelle <jess@linux.com>"

RUN apt-get update && apt-get install -y \
	gimp \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "gimp" ]
