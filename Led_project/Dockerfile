# Use an official Python runtime as a parent image
FROM python:3.9

# Set the working directory in the container
WORKDIR /app

# Install system dependencies for building rpi_ws281x
RUN apt-get update && \
    apt-get install -y \
    build-essential \
    python3-dev \
    libffi-dev \
    git \
    wget \
    curl \
    gcc \
    g++ \
    make

# Clone and build the ws281x library
RUN git clone https://github.com/rpi-ws281x/rpi-ws281x-python.git /rpi_ws281x && \
    cd /rpi_ws281x/library && \
    python setup.py build && \
    python setup.py install

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Expose the port the app runs on
EXPOSE 5000

# Define environment variable
ENV CFLAGS="-Wno-error"

# Run the command to start the app
CMD ["python", "app.py"]

