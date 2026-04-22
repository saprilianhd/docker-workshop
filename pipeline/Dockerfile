# Start with slim Python 3.12 image
FROM python:3.12.1-slim

# Copy uv binary from official uv image (multi-stage build pattern)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# Set working directory
WORKDIR /code

# Copy dependency files first (better layer caching)
COPY pyproject.toml uv.locked .python-version ./
# Install dependencies from lock file (ensures reproducible builds)
RUN uv sync --locked

# Copy application code
COPY pipeline.py .

# Set entry point
ENTRYPOINT ["uv", "run", "python", "pipeline.py"]