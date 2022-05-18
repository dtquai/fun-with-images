# Filename: Dockerfile
FROM nvidia/cuda:11.5.1-cudnn8-devel-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive

# RUN for base utilities
RUN apt-get update && \
         apt-get install -y build-essential && \
         apt-get install -y cmake && \
         apt-get install -y git && \
         apt-get install -y curl && \
         apt-get install -y wget && \
         apt-get install -y ca-certificates && \
     rm -rf /var/lib/apt/lists/*

# Create a working directory
RUN mkdir /app
WORKDIR /app

# RUN for LTS miniconda, PyTorch & other frameworks/libs
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && chmod +x ~/miniconda.sh && \
     ~/miniconda.sh -b -p /opt/conda && rm ~/miniconda.sh && \
     /opt/conda/bin/conda install -y python=3.8 numpy scikit-learn scipy ipython pillow && \
     /opt/conda/bin/conda config --append channels conda-forge && \
     /opt/conda/bin/conda install -y -c pytorch torchvision torchaudio filelock ray-default ray-rllib ray-tune ray-serve && \
     /opt/conda/bin/conda clean -ya

# Define ENV
ENV PATH=$CONDA_DIR/bin:$PATH