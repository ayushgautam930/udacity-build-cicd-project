FROM python:3.10-slim-bookworm

RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    g++ \
    libpcre3 \
    libpcre3-dev \
    libssl-dev \
    libffi-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pip install pipenv

RUN adduser --uid 1000 --disabled-password --gecos "" app

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile* /app/

RUN cd /app && pipenv install --system --deploy

COPY . /app

WORKDIR /app

USER app

CMD ["uwsgi", "--http", "0.0.0.0:5000", "--module", "app:app"]