FROM python:3.13-slim

RUN apt-get update && apt-get upgrade -y
RUN pip3 install --upgrade pip

RUN addgroup --gid 1000 user && adduser --uid 1000 --gid 1000 user
USER user
ENV PATH="/home/user/.local/bin:${PATH}"

RUN pip3 install torch torchvision --extra-index-url https://download.pytorch.org/whl/cpu
RUN pip3 install iopaint
RUN iopaint install-plugins-packages

EXPOSE 8080

CMD ["bash"]
