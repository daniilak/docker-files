FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install  -y python3 python3-pip wget

RUN pip3 install flask flask_cors flask_restful marshmallow PyYAML urllib3 requests
RUN apt-get remove -y $BUILD_DEPS && rm -rf /var/lib/apt/lists/*

ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONUNBUFFERED=1

COPY . /app

WORKDIR /app

RUN python3 app/yaml/swagger-yaml-to-html.py < app/yaml/api.yaml > app/yaml/doc.html

CMD python3 app/app.py
