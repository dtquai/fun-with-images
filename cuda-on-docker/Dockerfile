# Filename: Dockerfile
FROM nvidia/cuda:11.5.1-cudnn8-runtime-ubuntu20.04

RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y curl
RUN apt-get install unzip
RUN apt-get -y install python3
RUN apt-get -y install python3-pip

WORKDIR /var/app

COPY . .

RUN pip3 install --no-cache-dir -r requirements.txt

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

EXPOSE 80
CMD ["gunicorn", "-b", "0.0.0.0:80","app:app","--workers","1","-k","uvicorn.workers.UvicornWorker"]
