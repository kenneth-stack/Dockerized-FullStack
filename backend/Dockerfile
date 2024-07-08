# Use the official Python image from the Docker Hub
FROM python:3.12-slim

# Set environment variables to avoid prompts during Poetry installation
ENV POETRY_HOME="/opt/poetry" \
    POETRY_NO_INTERACTION=1

# Set the working directory in the container
WORKDIR /app

# Install Poetry
RUN pip install --upgrade pip && pip install poetry

# Copy only the necessary files for dependency installation
COPY pyproject.toml poetry.lock ./

# Create a virtual environment and install dependencies using Poetry
RUN python -m venv /opt/venv && \
    . /opt/venv/bin/activate && \
    poetry config virtualenvs.path /opt/venv && \
    poetry install ----no-root

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

# Activate the virtual environment and start the prestart script and then the FastAPI server
CMD ["bash", "-c", ". /opt/venv/bin/activate && /app/prestart.sh && uvicorn app.main:app --host 0.0.0.0 --port 8000"]
