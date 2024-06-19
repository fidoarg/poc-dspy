# Use the official Python 3.10 image from the Docker Hub
FROM python:3.10-slim

# Define environment variables for Poetry
ENV POETRY_VERSION=1.8.2
ENV POETRY_HOME=/opt/poetry

# Add Poetry to the PATH
ENV PATH="$POETRY_HOME/bin:$PATH"

# Install dependencies
RUN apt-get update && \
    apt-get install -y curl build-essential libssl-dev libffi-dev python3-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Poetry using curl and specify the version
RUN curl -sSL https://install.python-poetry.org | POETRY_VERSION=$POETRY_VERSION python3 -

# Verify Poetry installation
RUN poetry --version

# Configure Poetry to not create virtual environments
RUN poetry config virtualenvs.create false

# Set the working directory
WORKDIR /app

# Copy the project files to the working directory
COPY . .

# Install project dependencies
RUN poetry install --with=explore --no-interaction --no-root

# Expose the port the app runs on
EXPOSE 8888

# Define the command to run the application
CMD ["poetry", "run", "jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--notebook-dir=/app"]
