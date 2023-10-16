FROM lutraconsulting/merginmaps-backend:2023.3.0

USER root

RUN apt-get update \
    && apt-get install -y \
        curl \
        gpg \
        lsb-release \
        postgresql \
        telnet \
    && rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://packages.redis.io/gpg | gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/redis.list
RUN apt-get update && apt-get install -y redis

ENV LOCAL_PROJECTS=/data

USER mergin

COPY config.py /app/config.py
COPY gunicorn-logging.conf /app/gunicorn-logging.conf
