# pull official base image
FROM python:3.6-alpine3.9

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apk update \
    && apk add --virtual build-dependencies \
    build-base \
    gcc \
    wget \
    python-dev \
    git \
    && pip3 install -U pip
RUN apk add libc-dev gcc curl-dev libevent-dev python3-dev libressl-dev

RUN \
 apk add --no-cache postgresql-libs && \
 apk add --no-cache --virtual .build-deps gcc musl-dev postgresql-dev

# lint
RUN pip install --upgrade pip

# install python dependencies
COPY ./requirements.txt .
RUN \
 apk add --no-cache postgresql-libs && \
 apk add --no-cache --virtual .build-deps gcc musl-dev postgresql-dev && \
 python3 -m pip install -r requirements.txt --no-cache-dir && \
 apk --purge del .build-deps


# copy project
COPY . /usr/src/app/

# create user group and user
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

RUN chown -R appuser:appgroup /usr/src
RUN chown -R appuser:appgroup /home
# RUN chmod -R 755 /usr/src/app
RUN chmod -R 777 /var/log
USER appuser
RUN whoami

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]