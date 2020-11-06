# DESCRIPTION:  jupyter Notebook (AllSpark version) with some ALL PURPOSE python libraries + dependencies:
# (see details of libs in REQUIREMENTS.txt file)
#	 - data/machinelearning python
#	 - web scrapping & api
#	 - hadoop env api lib cloudera coms
#	 - flask webing 
#	 - azure sql apis
# 
# AUTHORS:      jupyter, Alexis Mathon <mathonal@gmail.com>
# USAGE:
#   #BUILD command
#   docker build -t delka/jupyterdata .
#
#   #Run Alias (replace the shared volume : $HOME/work/Jupyter_volume by your own folder)
# docker run -it --rm \
#     --name jupyter \
#     -p 8888:8888 -p 4040:4040 \
#     -v $HOME/work/Jupyter_volume:$HOME/work \
#     -w $HOME/work \
#     delka/jupyterdata
#
# if need to get in container (config files):
# docker exec -it -e GRAND_SUDO=yes jupyter /bin/bash
#
FROM jupyter/all-spark-notebook:latest
LABEL maintainer "Alexis Mathon <mathonal@gmail.com>"
USER root

# sasl pre-requisites for hadoop pylib
RUN apt-get update && apt-get install libsasl2-dev
# needed by pyodbc lib 
RUN apt-get install -y unixodbc-dev
#
# installation process for azuresql tools 
RUN apt-get install -y gnupg
RUN curl -s -N https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17 mssql-tools

# Jupiter config file
COPY jupyter_notebook_config.py /home/jovyan/.jupyter/jupyter_notebook_config.py

# needed python libs
COPY requirements.txt ./
RUN pip install --no-cache-dir --use-feature=2020-resolver -r requirements.txt

# NOTA ABOUT : --use-feature=2020-resolver
# ERROR: After October 2020 you may experience errors when installing or updating packages. This is because pip will change the way that it resolves dependency conflicts.
# We recommend you use --use-feature=2020-resolver to test your packages with the new resolver before it becomes the default.
# tensorflow 2.3.1 requires numpy<1.19.0,>=1.16.0, but you'll have numpy 1.19.1 which is incompatible.
