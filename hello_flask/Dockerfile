# Stage 1: Build stage
FROM python:3.8-slim as Build

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

COPY . .

RUN pip install --no-cache-dir flask mysqlclient

# Stage 2: Runtime stage
FROM python:3.8-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    default-libmysqlclient-dev \
    && rm -rf /var/lib/apt/lists/*

COPY --from=Build /app /app
COPY --from=Build /usr/local/lib/python3.8/site-packages /usr/local/lib/python3.8/site-packages
COPY --from=Build /usr/local/bin /usr/local/bin

EXPOSE 5005

CMD ["python", "app.py"]
