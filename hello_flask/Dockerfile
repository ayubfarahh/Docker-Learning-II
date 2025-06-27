#Stage 1: Build Stage
FROM python:3.8-slim as Build

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Copy project files into container
COPY . .

RUN pip install --no-cache-dir flask mysqlclient

#STAGE 2: Production stage

FROM python:3.8-slim

WORKDIR /app

COPY --from=Build /app /app

EXPOSE 5005

CMD ["python", "app.py"]