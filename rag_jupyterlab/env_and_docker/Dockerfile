ARG CUDA_ver=12.1.1
ARG cudnn_ver=8
ARG ubuntu_ver=22.04

FROM nvidia/cuda:${CUDA_ver}-cudnn${cudnn_ver}-runtime-ubuntu${ubuntu_ver}

# linuxの環境設定
RUN apt-get update \
    # imageのサイズを小さくするためにキャッシュ削除
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# 基本ツールと、python、pipのインストール
RUN apt-get update
RUN apt-get install -y \
        git wget curl python3 python3-pip

# psycopg2 用に依存パッケージ追加
RUN apt-get update && apt-get install -y gcc libpq-dev

RUN pip install --upgrade pip

# requirements.txtをコピーする
COPY requirements.txt ${PWD}
# pythonのパッケージをインストール
RUN pip install -r ./requirements.txt

WORKDIR /workspace
