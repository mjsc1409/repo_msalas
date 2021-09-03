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
