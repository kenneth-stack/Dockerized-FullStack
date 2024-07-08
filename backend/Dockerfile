# Use the official Python image from the Docker Hub
FROM python:3.12-slim

# Set environment variables to avoid prompts during Poetry installation
ENV POETRY_HOME="/opt/poetry" \
    POETRY_VIRTUALENVS_CREATE=false \
    POETRY_NO_INTERACTION=1

# Set the working directory in the container
WORKDIR /app

# Install Poetry
RUN pip install poetry

# Copy only the necessary files for dependency installation
COPY pyproject.toml poetry.lock ./

# Install dependencies using Poetry
RUN poetry config virtualenvs.create false && poetry install --only main

# Copy the rest of the working directory contents into the container
COPY . /app

# Set PYTHONPATH to include the 'app' directory
ENV PYTHONPATH="/app"

# Make the prestart script executable
RUN chmod +x /app/prestart.sh

# Debug: List files in the /app directory to ensure all files are present
RUN ls -l /app

# Expose the backend port
EXPOSE 8000

# Start the prestart script and then the FastAPI server
CMD ["bash", "-c", "/app/prestart.sh && uvicorn app.main:app --host 0.0.0.0 --port 8000"]
