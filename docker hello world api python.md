# Dockerfile

```
FROM python:3

WORKDIR /usr/src/app

# create requirements
RUN echo "bottle==0.12.17" > requirements.txt

# create app.py

RUN echo "from bottle import route, run" >> app.py
RUN echo "@route('/hello')" >> app.py
RUN echo "def index():" >> app.py
RUN echo "    return 'World'" >> app.py
RUN echo "run(host='0.0.0.0', port=8080)" >> app.py

RUN pip install --no-cache-dir -r requirements.txt

CMD [ "python", "./app.py" ]
```

# build

```
docker build --rm -t hello-world-docker .
```

# run

```
docker run -d --name hello-world-container -p 9090:8080 -t hello-world-docker
```

# test


```
curl localhost:9090/hello

```
**output:** World

# push to registry

```
docker login <REGISTRY_HOST>:<REGISTRY_PORT>
docker tag <IMAGE_ID> <REGISTRY_HOST>:<REGISTRY_PORT>/<APPNAME>:<APPVERSION>
docker push <REGISTRY_HOST>:<REGISTRY_PORT>/<APPNAME>:<APPVERSION>
```
sample:

```
docker login repo.company.com:3456
docker tag 19fcc4aa71ba repo.company.com:3456/myapp:0.1
docker push repo.company.com:3456/myapp:0.1
```
