# Use the official Python image as a parent image
FROM python:3.10-slim

# Set the working directory
WORKDIR /workspaces

# Install any necessary dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    libffi-dev \
    python3-dev \
    && apt-get clean

# Install Python packages
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . .

# Set the default command to run when starting the container
CMD ["bash"]
