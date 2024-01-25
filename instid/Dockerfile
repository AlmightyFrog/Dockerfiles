FROM python:3.10

RUN useradd user

RUN apt update && apt install -y git-lfs

RUN mkdir /app /data
RUN chown user:user /app /data
USER user

WORKDIR /app
RUN git lfs install
RUN git clone https://github.com/aitrepreneur/INSTID .

RUN pip install torch torchvision torchaudio xformers --index-url https://download.pytorch.org/whl/cul18

RUN pip install -r requirements.txt

RUN python app.py

EXPOSE 7860
VOLUME ["/data"]
CMD ["python", "app.py"]
