FROM nvidia/cuda:12.4.0-cudnn8-devel-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    git wget curl ca-certificates vim build-essential \
    python3 python3-pip python3-venv \
    libglib2.0-0 libsm6 libxrender1 libxext6 libgl1 && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /workspace

COPY requirements.txt /tmp/
RUN pip install --no-cache-dir \
    --index-url https://download.pytorch.org/whl/cu124 \  
    --extra-index-url https://pypi.tuna.tsinghua.edu.cn/simple \  
    -r /tmp/requirements.txt

COPY . /workspace

ENV HF_HOME=/workspace/.cache/huggingface \
    TRANSFORMERS_CACHE=/workspace/.cache/huggingface \
    TORCH_HOME=/workspace/.cache/torch \
    PYTHONPATH=/workspace

ENTRYPOINT ["/bin/bash"]