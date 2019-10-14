FROM python:3.7-slim-buster

RUN apt-get update && apt-get --no-install-recommends -y install python3.7-dev build-essential \
 && pip install gunicorn uvicorn \
 && apt-get -y purge --auto-remove -y python3.7-dev build-essential \
 && rm -rf /var/lib/apt/lists/*

COPY ./start.sh /start.sh
COPY ./gunicorn_conf.py /gunicorn_conf.py
COPY ./start-reload.sh /start-reload.sh

RUN chmod +x /start.sh \
  && chmod +x /start-reload.sh

COPY ./app /app
WORKDIR /app/

ENV PYTHONPATH=/app

EXPOSE 80

# Run the start script, it will check for an /app/prestart.sh script (e.g. for migrations)
# And then will start Gunicorn with Uvicorn
CMD ["/start.sh"]
