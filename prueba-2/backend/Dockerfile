FROM python:3.8-slim-buster

WORKDIR /app

ENV SECRET_KEY=12345

RUN apt-get update && apt-get install -y \
    gcc \
    g++ \
    build-essential \
    libpq-dev \
    postgresql-client \
    libmariadb-dev \
    gcc \
    python-dev \
    graphviz \
    libgraphviz-dev \
    pkg-config \
    graphviz-dev \
    libpq-dev \
    #python3.8-dev \
    libpq-dev \
    #python3-dev \
    #libpython3-dev \
    python3-wheel

ADD requirements.txt requirements.txt

RUN python3.8 -m pip install -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]