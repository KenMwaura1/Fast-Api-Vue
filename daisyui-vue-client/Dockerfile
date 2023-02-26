# pull official base image
FROM node:18.0.0-alpine AS base

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# copy requirements file
COPY ./package.json /usr/src/app/package.json

# install dependencies
RUN set -eux \
	&& apk add --no-cache --virtual .build-deps build-base \
	libressl-dev libffi-dev gcc musl-dev python3-dev \
	postgresql-dev \
	&& npm install --upgrade npm \
	&& npm install -g yarn\
	&& yarn add -r /usr/src/app/package.json \
	&& rm -rf /root/.cache/pip

# copy project
COPY . /usr/src/app/