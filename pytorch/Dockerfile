ARG BASE=wxsicey/python:3.9.1-oe2403lts

FROM ${BASE}

ARG VERSION=2.5.1

RUN yum install -y python3-pip

RUN pip install --no-cache-dir --index-url https://download.pytorch.org/whl/cpu \
    torch==${VERSION}