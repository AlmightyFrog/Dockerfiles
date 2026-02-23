FROM python:3.11-slim-bookworm

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        libgl1 \
        libglib2.0-0 \
        curl \
        ca-certificates \
        git \
        build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    addgroup --gid 1000 user && \
    adduser --uid 1000 --gid 1000 user

RUN curl -Ls https://astral.sh/uv/install.sh | sh && \
    ln -s /root/.local/bin/uv /usr/local/bin/uv

RUN uv pip install --system torch==2.10.0 torchvision --extra-index-url https://download.pytorch.org/whl/cpu && \
    uv pip install --system iopaint && \
    iopaint install-plugins-packages

USER user
ENV PATH="/home/user/.local/bin:/usr/local/bin:$PATH"

# ugly patch numpy dependency break
RUN pip3 install "numpy<2" 

EXPOSE 8080

CMD ["bash"]
