FROM python:3.10-slim

RUN apt-get update && apt-get upgrade -y
RUN pip3 install --upgrade pip

# In order to use GPU, install cuda version of pytorch first.
# pip3 install torch==2.1.2 torchvision==0.16.2 --index-url https://download.pytorch.org/whl/cu118
# AMD GPU users, please utilize the following command, only works on linux, as pytorch is not yet supported on Windows with ROCm.
# pip3 install torch==2.1.2 torchvision==0.16.2 --index-url https://download.pytorch.org/whl/rocm5.6

RUN pip3 install iopaint
RUN iopaint install-plugins-packages

EXPOSE 8080

CMD ["bash"]
