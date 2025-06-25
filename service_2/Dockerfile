FROM python:3.12-slim AS builder

RUN pip install uv

WORKDIR /app

COPY requirements.txt* ./

RUN if [ -f requirements.txt ]; then uv pip install --system -r requirements.txt; else pip install flask; fi

COPY . .

FROM python:3.12-slim

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages
COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /app .

EXPOSE 8002

CMD ["python", "app.py"]