FROM tensorflow/tensorflow:latest-gpu

# metadata
LABEL maintainer="abelb@nvidia.com" version="0.1" description="Introduction to object detection using TensorFlow API"

# system libs configure
RUN apt-get update && apt-get install -y wget git protobuf-compiler python-pil python-lxml && apt-get clean && rm -rf /var/lib/apt/lists/*

# create working directory for content
RUN mkdir -p /dli && cd /dli && git clone https://github.com/abelatnvidia/tfodapi.git && cd -

# set the working directory for everything
WORKDIR /dli/tfodapi/lab

# get the coco annotations
RUN mkdir coco && cd coco && wget --quiet http://msvocds.blob.core.windows.net/annotations-1-0-3/instances_train-val2014.zip && unzip instances_train-val2014.zip  && cd ..

# get the TensorFlow Object Detection API
RUN git clone https://github.com/tensorflow/models.git

ARG  NOTEBOOK_CONFIG_FILE=/root/.jupyter/jupyter_notebook_config.py

# configure jupyter
RUN echo "c.NotebookApp.ip = '*' "             > ${NOTEBOOK_CONFIG_FILE} && \ 
    echo "c.NotebookApp.port = 8888"          >> ${NOTEBOOK_CONFIG_FILE} && \
    echo "c.NotebookApp.open_browser = False" >> ${NOTEBOOK_CONFIG_FILE} && \
    echo "c.NotebookApp.token = '' "          >> ${NOTEBOOK_CONFIG_FILE} && \
    echo "c.NotebookApp.password = '' "       >> ${NOTEBOOK_CONFIG_FILE}

# Jupyter port 
EXPOSE 8888
