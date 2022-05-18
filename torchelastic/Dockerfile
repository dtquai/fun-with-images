# Filename: Dockerfile
ARG BASE_IMAGE=pytorch/pytorch:1.9.0-cuda11.1-cudnn8-runtime
FROM $BASE_IMAGE

RUN pip install awscli --upgrade
RUN pip install classy-vision
RUN pip uninstall -y torch
RUN pip install --pre torch -f https://download.pytorch.org/whl/nightly/cu111/torch_nightly.html

WORKDIR /workspace

# download imagenet tiny for data
RUN apt-get -q update && apt-get -q install -y wget unzip
RUN wget -q <PATH_TO_MDL>

COPY . ./appdir
RUN chmod -R u+x ./appdir/bin
RUN appdir/bin/install_etcd -d appdir/bin
ENV PATH=/workspace/appdir/bin:${PATH}
RUN project

USER root
ENTRYPOINT ["python", "-m", "torch.distributed.run"]
CMD ["--help"]
