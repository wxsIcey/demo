ARG BASE=openeuler/python:3.9.9-oe2409

FROM ${BASE}

ARG VERSION=2.7.0

RUN yum install -y python3-pip

RUN pip install --no-cache-dir --index-url https://download.pytorch.org/whl/cpu \
    torch==${VERSION}