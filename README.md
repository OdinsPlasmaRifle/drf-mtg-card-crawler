# Django MtG Card Crawler

MtG card searcher for South African online stores. The following stores are supported:

- Luckshack
- Dracoti
- Top Deck
- Sad Robot
- HQ Gaming
- The Warren
- A.I. Fest
- Battle Wizards
- Underworld Connections

## Development

Setup a Python virtual environment first. Then run the following commands from within that environment.

Install the necessary python packages:

```shell
pip install -r requirements.txt
```

Add a `.env` file to the project root. Use the `.example.env` file as a template.

Next, spin up a docker container for the postgres database:

```shell
docker-compose up -d postgres
```

Run the migrations on the new database:

```shell
python ./src/manage.py migrate
```

Load the store fixtures:

```shell
python ./src/manage.py loaddata stores.json
```

Collect the static files:

```shell
python ./src/manage.py collectstatic
```

Finally, run the django server for testing:

```shell
python ./src/manage.py runserver
```

The django server will be served on: http://localhost:8000

## Production

This project can be run in production using docker.

Ensure that you run docker as a non-root user who is part of the `docker` group.

Also, update the `.env` file to have values appropriate for production usage.

To run the docker containers, enter the following commands:

```shell
docker-compose up -d --no-deps --build
```

This will spin up all the docker containers required.

You can then migrate the database:

```shell
docker exec drf-mtg-card-crawler_web_1 /bin/sh -c "python manage.py migrate"
```

Load the store fixtures:

```shell
docker exec drf-mtg-card-crawler_web_1 /bin/sh -c "python manage.py loaddata stores.json"
```

Collect the static files:

```shell
docker exec drf-mtg-card-crawler_web_1 /bin/sh -c "python manage.py collectstatic --no-input"
```
