# Multi-stage builds 적용해보기

## Original Code
\: GPU 사용 여부를 체크해볼 수 있는 간단한 API  
\: Image Size 8.09GB
```python title="main.py"
from fastapi import FastAPI
import torch

app=FastAPI()

@app.get("/")
def check():
    return {"Hi! It's my space!"}

@app.get("/gpu_check")
async def gpu_check():
    return {"GPU":torch.cuda.is_available()}
```
```Dockerfile title="Dockerfile"
FROM pytorch/pytorch:1.9.1-cuda11.1-cudnn8-runtime

WORKDIR /code

COPY ./app /code/app
COPY ./requirements.txt /code/requirements.txt

RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

ENV NUM="2000"

ENTRYPOINT ["uvicorn"]
CMD ["app.main:app", "--host", "0.0.0.0", "--port", "13583"]
```

---
## Multi-stage Builds
\: GPU 사용 여부를 체크해볼 수 있는 간단한 API  
\: CUDA image, conda 이용  
\: Image Size 5.5GB

```Dockerfile title="Dockerfile"
ARG CONDA_ENV=docker_p
ARG CONDA_DIR=/opt/conda
ARG APP_DIR=/code

FROM nvidia/cuda:11.3.0-cudnn8-devel-ubuntu20.04 AS builder

ARG CONDA_ENV
ARG CONDA_DIR

ENV DEBIAN_FRONTEND=noninteractive \
    PYTHON_VERSION=3.9 \
    PATH=$CONDA_DIR/bin:$PATH 

SHELL ["/bin/bash", "-c"]

COPY ./requirements.txt /requirements.txt

RUN export BUILD_TARGET_ARCH=$(uname -m) && \
    echo "$BUILD_TARGET_ARCH" && \
    apt-get update --fix-missing && \
    apt-get install -y --no-install-recommends wget unzip bzip2 build-essential ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    if [ ${BUILD_TARGET_ARCH} == "x86_64" ]; then \
        export CONDA_URL=https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh; \
    else echo "Unsupported Flatform"; \
    fi && \ 
    wget -q $CONDA_URL -O /root/miniconda.sh && \
    /bin/bash /root/miniconda.sh -b -p /opt/conda && \
    rm /root/miniconda.sh &&  \
    /opt/conda/condabin/conda clean -y -av && \
    /opt/conda/condabin/conda update -y conda && \
    /opt/conda/condabin/conda create -y -n ${CONDA_ENV} python==${PYTHON_VERSION} pip && \
    grep -v '^#' < requirements.txt | xargs -t -L 1 /opt/conda/envs/${CONDA_ENV}/bin/pip install --timeout 60 --no-cache-dir && \
    /opt/conda/envs/${CONDA_ENV}/bin/pip cache purge && \
    /opt/conda/condabin/conda clean -y -av 


FROM nvidia/cuda:11.3.0-runtime-ubuntu20.04 AS base

ARG CONDA_ENV
ARG CONDA_DIR

ENV PATH=$CONDA_DIR/bin:$PATH 
ENV PATH=/opt/conda/envs/$CONDA_ENV/bin:$PATH

RUN echo -e ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo -e "conda activate $CONDA_ENV" >> ~/.bashrc && \
    rm -vrf /var/lib/apt/lists/* /var/cache/apt/archives/* /tmp/* /root/.cache/* 

COPY --from=builder /opt /opt


FROM base AS source
ARG APP_DIR

WORKDIR /${APP_DIR}
COPY ./app /${APP_DIR}/app

ENTRYPOINT ["uvicorn"]
CMD ["app.main:app", "--host", "0.0.0.0", "--port", "13583"]

```



!!! quote
    - [My-github](https://github.com/YSHeee/practice-docker)
    - Voiceprint-api.sp_recog-Dockerfile
    - [Useful-Blog](https://medium.com/the-artificial-impostor/smaller-docker-image-using-multi-stage-build-cb462e349968)  
    - [Useful-Blog-Github](https://github.com/ceshine/Dockerfiles/blob/master/cuda/pytorch-apex/Dockerfile)  
    - [Useful-Blog2](https://gzupark.dev/blog/A-guide-to-make-the-reproducible-environment-using-the-Docker-for-deep-learning-researcher/)
    - [Useful-Blog3](https://qiita.com/ynaka81/items/c44209c6f862d938c2ff)