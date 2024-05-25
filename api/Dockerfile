FROM python:3.12.2-alpine

ARG FLASK_APP="app.py"
ARG FLASK_ENV="development"
ENV FLASK_APP=$FLASK_APP
ENV FLASK_ENV=$FLASK_ENV

WORKDIR /api
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .
CMD [ "python3","-m","flask","run","--host=0.0.0.0" ]