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