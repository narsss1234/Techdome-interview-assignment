Author/Owner: narsss1234
# Techdome Interview Question

# Deploying Database - mongoDB

1. Created a folder name database and created a Dockerfile

```
FROM mongo:latest

ENV MONGO_INITDB_ROOT_USERNAME=admin
ENV MONGO_INITDB_ROOT_PASSWORD=password
ENV MONGO_INITDB_DATABASE=mern_app


EXPOSE 27017

CMD ["mongod"]
```

Using Docker hub documention or mongo db

Set variables fo the DB for username, password and the database name

# Deploying Backend

1. Checked and found in the server.js file, that there are process env variables that need to be passed in order to deploy the backend

2. Created a .env file

```
DB="mongodb+srv://*********@mongodb/mern_app"
PORT="3080"
```

3. Install the node dependencies

```
npm install
```

4. Run the node server

```
node server.js
```

5. The backend is now deployed, test it on

```
http://localhost:3080

and

http://localhost:3080/api
```
6. On the console, you will find the below messages

```
listening at port 3080
Connection established!
```

7. Once this is tested, created a Dockerfile for the backend

```
FROM node:alpine

WORKDIR /app

COPY . .

RUN npm install --force

EXPOSE 3080

CMD ["node","server.js"]
```

# Deploying frontend

1. Checked and found that a .env file is already preset here, where backend url can be provided

```
REACT_APP_BASE_URL="http://localhost:3080/api"

or

REACT_APP_BASE_URL="http://backend:3080/api"
```
2. Install the node dependencies

```
npm install
```

3. Run the frontend app

```
npm start
```

4. The app will be deployed on below url

```
http://localhost:3000
```

5. Created a dockerfile to containerize the application

```
FROM node:alpine

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm","start"]
```

# Create a docker compose

1. Strategy

```
Create a network to isolate the stack deployment

add dependencies in such a way that the stack is deployed in the below manner

1. Mongodb
2. Backend
3. Frontend

```
2. Once the stack is up

The backend and the frontend can be tested to see if the connection is established to mongodb and also to see if the frontend is working as expected.

# Minikube Deployment

1. Pushed the docker images to dockerhub

```
narsss1234/techdome-backend:latest

narsss1234/techdome-frontend:latest
```

2. Created Kuberenets manifest files

Created them seperately for deployment and a service

3. Launched minikube

4. First applied mongo deployment and service

5. Deployed backend deployment and service files

5. Backend can be tested by the below command

```
minikube service backend --url

test the url, for the same output as deployed locally
```

6. To check logs run below command

```
kubectl logs pod/backend*****
```

7. Deployed frontend deployment and service files

5. frontend can be tested by the below command

```
minikube service frontend --url

test the url, for the same output as deployed locally
```

6. To check logs run below command

```
kubectl logs pod/frontend*****
```

# Application is deployed, due to time contraints there were many security compromises made.