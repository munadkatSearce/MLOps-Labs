# FROM pytorch/torchserve:latest-gpu
FROM python:3.9

USER root

RUN apt-get update

RUN apt-get install ffmpeg libsm6 libxext6  -y

RUN apt-get --assume-yes install wget

RUN apt-get -y install git 

# RUN apt-get install -y python3.7

RUN wget -nv https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz && \
        mkdir /root/tools && \
        tar xvzf google-cloud-sdk.tar.gz -C /root/tools && \
        rm google-cloud-sdk.tar.gz && \
        /root/tools/google-cloud-sdk/install.sh --usage-reporting=false \
        --path-update=false --bash-completion=false \
        --disable-installation-options && \
        rm -rf /root/.config/* && \
        ln -s /root/.config /config && \
        rm -rf /root/tools/google-cloud-sdk/.install/.backup

ENV PATH $PATH:/root/tools/google-cloud-sdk/bin

RUN mkdir app
WORKDIR /app
COPY . /app

RUN pip install -r requirements.txt

CMD ["python", "train.py"]

