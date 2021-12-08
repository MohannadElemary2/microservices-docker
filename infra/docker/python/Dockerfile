FROM python:3

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /code

COPY ./backend/notification/ /code/

RUN pip install -r requirements.txt

WORKDIR /code