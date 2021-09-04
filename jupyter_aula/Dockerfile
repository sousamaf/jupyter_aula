# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# Para utilizar com GPU
## Base: https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/dockerfiles/dockerfiles/cpu-jupyter.Dockerfile
# ARG BASE_CONTAINER=tensorflow/tensorflow:latest-gpu-jupyter

# Para utilizar com CPU
# ARG BASE_CONTAINER=tensorflow/tensorflow:nightly-jupyter

# FROM $BASE_CONTAINER

ARG UBUNTU_VERSION=20.04

FROM ubuntu:${UBUNTU_VERSION} as base

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

RUN apt-get update && apt-get install -y curl

# See http://bugs.python.org/issue19846
ENV LANG C.UTF-8

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip

RUN python3 -m pip --no-cache-dir install --upgrade \
    "pip<20.3" \
    setuptools

# Some TF tools expect a "python" binary
RUN ln -s $(which python3) /usr/local/bin/python

# Options:
#   tensorflow
#   tensorflow-gpu
#   tf-nightly
#   tf-nightly-gpu
# Set --build-arg TF_PACKAGE_VERSION=1.11.0rc0 to install a specific version.
# Installs the latest version by default.
ARG TF_PACKAGE=tensorflow
ARG TF_PACKAGE_VERSION=2.6.0
RUN python3 -m pip install --no-cache-dir ${TF_PACKAGE}${TF_PACKAGE_VERSION:+==${TF_PACKAGE_VERSION}}

COPY bashrc /etc/bash.bashrc
RUN chmod a+rwx /etc/bash.bashrc

RUN python3 -m pip install --no-cache-dir jupyter matplotlib
# Pin ipykernel and nbformat; see https://github.com/ipython/ipykernel/issues/422
# Pin jedi; see https://github.com/ipython/ipython/issues/12740
RUN python3 -m pip install --no-cache-dir jupyter_http_over_ws ipykernel==5.1.1 nbformat==4.4.0 jedi==0.17.2
RUN jupyter serverextension enable --py jupyter_http_over_ws

RUN mkdir -p /tf/tensorflow-tutorials && chmod -R a+rwx /tf/
RUN mkdir /.local && chmod a+rwx /.local
RUN apt-get update && apt-get install -y --no-install-recommends wget git
WORKDIR /tf/tensorflow-tutorials
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/classification.ipynb
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/overfit_and_underfit.ipynb
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/regression.ipynb
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/save_and_load.ipynb
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/text_classification.ipynb
RUN wget https://raw.githubusercontent.com/tensorflow/docs/master/site/en/tutorials/keras/text_classification_with_hub.ipynb
COPY readme-for-jupyter.md README.md
RUN apt-get autoremove -y && apt-get remove -y wget
WORKDIR /tf
EXPOSE 8888


#RUN apt-get update && apt-get install wget && groupadd -g 1000 aula && useradd -d /home/aula -m aula -u 1000 -g 1000
RUN apt-get update && apt-get install -y openssh-client vim tmux
RUN rm -f /etc/localtime
RUN ln -sf /usr/share/zoneinfo/America/Araguaina /etc/localtime
# RUN apt -y install tzdata
RUN apt install python3-gi python3-gi-cairo gir1.2-gtk-3.0 -y
RUN apt install build-essential libcairo2-dev libjpeg-dev libgif-dev -y
RUN python3 -m pip install --upgrade pip
RUN apt install libpq-dev pkg-config -y

FROM base 

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

RUN python3 -m ipykernel.kernelspec

CMD ["bash", "-c", "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --no-browser --allow-root"]
