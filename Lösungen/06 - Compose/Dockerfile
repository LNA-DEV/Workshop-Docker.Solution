# Erstellen sie eine Dockerfile für app.py
# Notwendig: pip install -r requirements.txt
# Deswegen muss diese Datei im Container sein
# Exposen sie den Port 5000
# Ersetzen sie XXX mit einem sinnvollen Basis-Image

FROM python:3.10-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run", "--debug"]