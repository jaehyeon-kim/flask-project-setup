FROM python:3.7

ENV PYTHONUNBUFFERED 1

ADD Pipfile /tmp/Pipfile
WORKDIR /tmp
RUN pip install pipenv \
  && pipenv lock -r > requirements.txt \
  && pip install -r requirements.txt

RUN mkdir /opt/code
WORKDIR /opt/code