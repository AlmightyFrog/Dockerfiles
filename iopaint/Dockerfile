FROM python:3.10-slim

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 install --upgrade pip && \
    addgroup --gid 1000 user && \
    adduser --uid 1000 --gid 1000 user

USER user
ENV PATH="/home/user/.local/bin:${PATH}"

RUN pip3 install torch==2.1.2 torchvision --extra-index-url https://download.pytorch.org/whl/cpu && \
    pip3 install iopaint && \
    iopaint install-plugins-packages

# ugly patch numpy dependency break
RUN pip3 install "numpy<2" 

EXPOSE 8080

CMD ["bash"]
