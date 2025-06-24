FROM ghcr.io/astral-sh/uv:0.1.39-python3.12

WORKDIR /app

COPY pyproject.toml uv.lock ./

RUN uv pip sync --system

COPY app.py .

EXPOSE 8002

CMD ["uv", "run", "--host", "0.0.0.0", "--port", "8002", "app.py"]