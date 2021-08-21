# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# Para utilizar com GPU
# ARG BASE_CONTAINER=tensorflow/tensorflow:latest-gpu-jupyter

# Para utilizar com CPU
ARG BASE_CONTAINER=tensorflow/tensorflow:latest-jupyter

FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

#RUN apt-get update && apt-get install wget && groupadd -g 1000 aula && useradd -d /home/aula -m aula -u 1000 -g 1000
RUN apt-get update && apt-get install -y vim tmux
RUN python3 -m pip install --upgrade pip

COPY requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

# CPU
RUN pip install torch==1.9.0+cpu torchvision==0.10.0+cpu torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
# GPU 11
# RUN pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
# GPU 10
# RUN pip install torch torchvision torchaudio

RUN jupyter nbextension install --py jupyter_tabnine
RUN jupyter nbextension enable --py jupyter_tabnine
RUN jupyter serverextension enable --py jupyter_tabnine
RUN jupyter serverextension enable voila --sys-prefix


# ENV PATH=$PATH:/home/aula/.local/bin

# # RUN chown -R 1000:1000 /home/aula/.local/share/jupyter/*

# RUN mkdir /tf/work
# RUN chown -R 1000:1000 /tf

RUN ipython profile create
RUN echo 'c.IPCompleter.use_jedi = False' >> ~/.ipython/profile_default/ipython_kernel_config.py
RUN echo 'c.NotebookApp.password = "argon2:$argon2id$v=19$m=10240,t=10,p=8$3+hFcCaQAUEL9JoAk9p/1g$qTdzoibh1bZJjmya5407TA"' >> ~/.ipython/profile_default/ipython_kernel_config.py

## Integração com o Metatrader
# RUN pip install MetaTrader5
# RUN pip install pytz

WORKDIR /
