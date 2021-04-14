# pull official base image
#FROM python:3.8.1-slim-buster
FROM python:3

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install system dependencies
RUN apt-get update && apt-get install -y netcat

#RUN apt-get install -y postgresql-client

#RUN apt-get -y install postgresql

#RUN apt-get install postgresql-dev gcc python3-dev musl-dev

RUN apt-get -y install python-scipy

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt /usr/src/app/requirements.txt
RUN pip install -r requirements.txt

# copy project
COPY . /usr/src/app/

RUN echo $(ls -1 /usr/src/app/)

# using the local flask server
#CMD [ "python", "/usr/src/app/run_server.py" ]
CMD ["gunicorn"  , "-b", "0.0.0.0:8081", "dive.server.core:app"]

# run entrypoint.sh
#ENTRYPOINT ["/usr/src/app/entrypoint.sh"]