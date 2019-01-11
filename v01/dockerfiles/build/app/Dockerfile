FROM python:slim
MAINTAINER optimum <info@optimum-web.com>

# ---------- app prerequisites ------------- #
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
curl locales gcc libpq5 git curl lsof libpq-dev libffi-dev supervisor unzip make procps

# Set the locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

WORKDIR /app
COPY requirements.txt /app/requirements.txt
COPY supervisord.conf /etc/supervisord.conf
COPY src/flask_app.tar.gz /app/flask_app.tar.gz
COPY src/Flask-1.0.2.tar.gz /app/Flask-1.0.2.tar.gz
RUN pip install -U Flask-1.0.2.tar.gz
RUN pip install git+https://github.com/Supervisor/supervisor

RUN pip install --upgrade pip
RUN pip install -r requirements.txt