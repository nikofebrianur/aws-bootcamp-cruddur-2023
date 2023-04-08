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
```

Then, run the flask app
```
python3 -m flask run --host=0.0.0.0 --port=4567
```
![Run flask app in dev](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-1/run%20docker%20at%20port%204567%20and%20unlock.png)

Remember to unset the env
```
unset FRONTEND_URL
unset BACKEND_URL
```

### Build the docker
Change the directory one level above first
```
cd ..
docker build -t backend-flask ./backend-flask
```
![Build Success](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-1/docker%20build%20flask%20app.png)

### Run the docker
```
docker run --rm -p 4567:4567 -it -e FRONTEND_URL='*' -e BACKEND_URL='*' backend-flask
```
You can check it run in /api/activites/home endpoint.
![Success run the docker](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/main/journal/assets/week-1/success%20run%20the%20docker%20flask%20app.png)

## HOMEWORK CHALLENGE
### Run docker in local use WSL2
First time use docker in WSL2. I have to search documentation and find the good one here [Docker Desktop WSL 2 backend on Windows](https://docs.docker.com/desktop/windows/wsl/)
And then, just follow the steps above and it run on local I guess...
![run the app locally using docker](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/week-1/journal/assets/week-1/LOCAL%20running%20docker%20locally%20use%20wsl2.png)

## Push image to Docker Hub
I wanna use new tag for the image before push it.
```
docker tag backend-flask:latest 12903478/backend-flask:v1
docker push 12903478/backend-flask:v1
```
![My images in local](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/week-1/journal/assets/week-1/docker%20images.png)
![New pushed image in Docker Hub](https://github.com/nikofebrianur/aws-bootcamp-cruddur-2023/blob/week-1/journal/assets/week-1/docker%20hub.png)
