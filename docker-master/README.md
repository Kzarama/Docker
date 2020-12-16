# Curso de Docker

Make the communication between two containers, one with mongo and other with js.
Build the docker image

```bash
docker build -t app .
```

Run the container of example

```bash
docker run --rm -p 3000:3000 docker-master
```

---

Run with bind mounts for the automatic changes in the code

```bash
docker run --rm -p 3000:3000 -v JS_PATH:JS_CONTAINER_PATH NAMES
```

---

Create the network

```bash
docker network create --attachable mongo_js_network
```

Run the mongo container

```bash
docker run -d --name db mongo
```

Connect the container of mongo at the network

```bash
docker network connect mongo_js_network db
```

Run and connect the app of js at the network (--env = environment variable)

```bash
docker run -d --name app -p 3000:3000 --env MONGO_URL=mongodb://db:27017/test docker-master
```

See the details of the network

```bash
docker network inspect mongo_js_network
```

---

Run the docker-compose file

```bash
docker-compose up
```

Stop the docker-compose and delete the services and networks

```bash
docker-compose down
```
