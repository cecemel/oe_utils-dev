FROM python:3.5

RUN apt-get update
RUN apt-get install -y libgeos-c1 libgeos-3.4.2

WORKDIR "/app"
ARG GITUSER="USERNAME_NEEDED"
ARG GITPW="PASSWORD_NEEDED"

COPY requirements.txt /app/
COPY requirements-dev.txt /app/

RUN pip install -r requirements.txt
RUN pip install -r requirements-dev.txt

COPY . /app

WORKDIR "/app"