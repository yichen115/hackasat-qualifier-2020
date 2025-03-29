FROM python:3.7-slim AS python_env

WORKDIR /src
RUN sed -i 's|deb.debian.org|mirrors.aliyun.com|g' /etc/apt/sources.list.d/debian.sources ;\
    apt update ;\
    apt install -y --no-install-recommends python3-virtualenv python-dev-is-python3 build-essential
    
ENV VIRTUAL_ENV="/opt/venv"
ENV PATH="/opt/venv/bin:$PATH"

RUN python -m venv $VIRTUAL_ENV ;\
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple ;\
    pip install --upgrade pip ;\
    pip install --no-cache-dir pwntools 

FROM python:3.7-slim
ENV PATH="/opt/venv/bin:$PATH"
ENV VIRTUAL_ENV="/opt/venv"
COPY --from=python_env /opt/venv /opt/venv

WORKDIR /solver
COPY *.py /solver/

CMD python solve.py
