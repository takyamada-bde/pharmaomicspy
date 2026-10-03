FROM python:3.12
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

RUN groupadd -r appgroup && useradd -r -m -d /home/appuser -g appgroup appuser

WORKDIR /usr/src

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    UV_PROJECT_ENVIRONMENT=/opt/.venv \
    PATH="/opt/.venv/bin:$PATH"

COPY pyproject.toml uv.lock ./

RUN --mount=type=cache,target=/root/.cache/uv \
    uv sync --frozen --no-install-project --no-dev --no-cache --compile-bytecode

COPY --chown=appuser:appgroup . .

USER appuser

CMD ["/bin/bash"]
