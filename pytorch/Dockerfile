ARG BASE=wxsicey/python:3.9.8-oe2503

FROM ${BASE}

ARG VERSION=2.6.0

RUN yum install -y python3-pip

RUN pip install --no-cache-dir --index-url https://download.pytorch.org/whl/cpu \
    torch==${VERSION}