# Week 1 — App Containerization

## DOCKER TASK
For this week I followed all the steps from live streaming video, because I'm trying to understand the Docker stuff

### Make the Dockerfile
FROM python:3.10-slim-buster
WORKDIR /backend-flask
COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt
COPY . .
ENV FLASK_ENV=development
EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]

### Install the requirements
```
cd backend-flask
pip3 install -r requirements.txt 
```

### Run the docker in port 4567 (dev)
(In backend-flask folder)

First, export the environment
```
export FRONTEND_URL="*"
export BACKEND_URL="*"

Then, run the flask app
```
python3 -m flask run --host=0.0.0.0 --port=4567
```

Remember to unset the env
```
unset FRONTEND_URL
unset BACKEND_URL
```

### Build the docker
Change the directory one level above first
```
cd ..
docker build -t backend-flask ./backend_flask
```

### Run the docker
```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```
You can check it run in /api/activites/home endpoint.