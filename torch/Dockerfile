ARG BASE_IMAGE=pytorch/pytorch

FROM ${BASE_IMAGE} as dev-base

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV DEBIAN_FRONTEND noninteractive\
    SHELL=/bin/bash
RUN apt-get update --yes && \
    # - apt-get upgrade is run to patch known vulnerabilities in apt-get packages as
    #   the ubuntu base image is rebuilt too seldom sometimes (less than once a month)
    apt-get upgrade --yes && \
    apt install --yes --no-install-recommends\
    git\
    wget\
    curl\
    git\
    bash\
    openssh-server &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN pip install jupyterlab
RUN pip install ipywidgets
RUN pip install jupyter-archive
RUN jupyter nbextension enable --py widgetsnbextension

RUN git clone https://github.com/JoePenna/Dreambooth-Stable-Diffusion
RUN uses_reg = False
RUN wget https://sexy.canine.wf/file/yiffy-ckpt/yiffy-e18.ckpt -O /workspace/Dreambooth-Stable-Diffusion/model.ckpt
RUN mkdir -p /workspace/Dreambooth-Stable-Diffusion/training_images
RUN git clone https://github.com/JoePenna/Dreambooth-Stable-Diffusion
RUN pip install omegaconf
RUN pip install einops
RUN pip install pytorch-lightning==1.6.5
RUN pip install test-tube
RUN pip install transformers
RUN pip install kornia
RUN pip install -e git+https://github.com/CompVis/taming-transformers.git@master#egg=taming-transformers
RUN pip install -e git+https://github.com/openai/CLIP.git@main#egg=clip
RUN pip install setuptools==59.5.0
RUN pip install pillow==9.0.1
RUN pip install torchmetrics==0.6.0
RUN pip install -e .
RUN pip install protobuf==3.20.1
RUN pip install gdown
RUN pip install -qq diffusers["training"]==0.3.0 transformers ftfy
RUN pip install -qq "ipywidgets>=7,<8"
RUN pip install huggingface_hub
RUN pip install ipywidgets==7.7.1

ADD start.sh /

RUN chmod +x /start.sh

CMD [ "/start.sh" ]

