# DESCRIPTION:  Anaconda container with some libraries & dependencies
# AUTHORS:      Alexis Mathon <mathonal@gmail.com>
# USAGE:
#   #BUILD command
#   docker build -t delka/conda_gen .
#   docker-compose run --rm conda_gen
#
#   #Run Alias 
#   defaut volume and workdir is under $HOME/work/project_code
#   change volume with parameter in alias
#   condagen(){
#   local curworkdir="$HOME/work/playermp3/project_code"
#   local contname="condagen"

#   del_stopped $contname #helper function to remove any exited container of that name

#   xhost +local:root; \
#   docker run -it \
#       -p 8888:8888 \
#       -v $curworkdir:$curworkdir \
#       -w $curworkdir \
#       -v /etc/localtime:/etc/localtime:ro \
#       --device /dev/snd \
#       --device /dev/dri \
#       -e DISPLAY=unix:0.0 -v="/tmp/.X11-unix:/tmp/.X11-unix:rw" --privileged \
#       --name $contname \
#       delka/conda_gen 
# }
#
# NOTES : 
# 1 - Page about creation and activation of user env in container build :
# https://pythonspeed.com/articles/activate-conda-dockerfile/
# (aim was to create a distinct env from base BUT pygame install does not work in new env, forced to update base ...)
#
# 2 - this construct will, in default config, test presence of numpy lib to check if requirements installed correctly
# (Since errors in requirements wont prevent image building)
#
# 3- use Volume/workdir during DOCKER RUN command to point to your own code
#
FROM continuumio/miniconda3
# List of necessary_libs to link image and sound (when docker run): 
# libgl1-mesa-dri, libgl1-mesa-glx 
# libmtdev1
# for pygame : libsdl2 libsdl2-gfx libsdl2-image libsdl2-mixer libsdl2-net libsdl2-ttf
RUN apt-get update && apt-get install -y \
    libgl1-mesa-dri \
    libgl1-mesa-glx \
    libmtdev1 \
    libsdl2-dev \
    libsdl2-image-dev \
    libsdl2-mixer-dev \
    libsdl2-ttf-dev
# ====================================
# INSTALLING CONDA WORKING ENVIRONMENT
# ====================================
WORKDIR /usr/src
# Make RUN commands use `bash --login`:
SHELL ["/bin/bash", "--login", "-c"]
# user env : updating base env
COPY requirements.txt .
# shell to execute all runs in conda base env  
SHELL ["conda", "run", "-n", "base", "/bin/bash", "-c"]
# install user libs
RUN pip install -r requirements.txt
# check on some libs
RUN python -c "import numpy"
#Tkinter : unable to install via pip
RUN conda install -c anaconda tk
RUN python -c "import tkinter"
# ====================================
# The code to run when container is started:
# will execute test version on main.py copied in /usr/src/app if no other volume or Wk
COPY main.py .
ENTRYPOINT ["conda", "run", "-n", "base", "python", "main.py"]
#ENTRYPOINT ["/bin/bash"]
