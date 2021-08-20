# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
# Para utilizar com GPU
#ARG BASE_CONTAINER=tensorflow/tensorflow:latest-gpu-jupyter

# Para utilizar com CPU
ARG BASE_CONTAINER=tensorflow/tensorflow:latest-jupyter

FROM $BASE_CONTAINER

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

RUN apt-get update && apt-get install wget && groupadd -g 1000 aula && useradd -d /home/aula -m aula -u 1000 -g 1000
ENV PATH=$PATH:/home/aula/.local/bin
RUN python3 -m pip install --upgrade pip
USER aula
RUN pip install jupyterlab==3
RUN pip install pyforest
RUN pip install python-Levenshtein
RUN pip install fuzzywuzzy
RUN pip install --user tf-agents
RUN pip install --user dm-reverb
RUN pip install -q tensorflow-recommenders
RUN pip install -q --upgrade tensorflow-datasets
RUN pip install tf-agents
RUN pip install Pillow
RUN pip install tensorboard
RUN pip install SpeechRecognition
RUN pip install pandas_datareader
RUN pip install sklearn
RUN pip install scikit-learn
RUN pip install scikit-image
RUN pip install wandb
RUN pip install h5py
RUN pip install gym
RUN pip install keras
RUN pip install torch==1.9.0+cpu torchvision==0.10.0+cpu torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html
RUN pip install voila
RUN pip install RISE
RUN pip install pydotplus
RUN pip install graphviz
RUN pip install seaborn
RUN pip install simpful 
RUN pip install matplotlib
RUN pip install pycodestyle

USER root
RUN pip install jupyter-tabnine
RUN jupyter nbextension install --py jupyter_tabnine
RUN jupyter nbextension enable --py jupyter_tabnine
RUN jupyter serverextension enable --py jupyter_tabnine
RUN pip install python-language-server

RUN chown -R 1000:1000 /home/aula/.local/share/jupyter/*

RUN mkdir /tf/work
RUN chown -R 1000:1000 /tf
USER aula

RUN ipython profile create
RUN echo 'c.IPCompleter.use_jedi = False' >> ~/.ipython/profile_default/ipython_kernel_config.py
## Integração com o Metatrader
# RUN pip install MetaTrader5
# RUN pip install pytz

WORKDIR /
