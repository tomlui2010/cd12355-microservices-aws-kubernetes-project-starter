# Use the official Python image with version 3.9 on a slim Debian Buster base
FROM python:3.9-slim-buster

# Set the working directory inside the container to /app
WORKDIR /app

# Copy the requirements.txt file to the working directory
COPY requirements.txt .

# Install the Python packages specified in requirements.txt
# --no-cache-dir ensures no cache is used, --upgrade updates pip to the latest version
# hadolint ignore=DL3013: This line ignores the linter warning about missing pip version
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --trusted-host pypi.python.org --no-cache-dir -r requirements.txt

# Copy the entire application source code to the working directory
COPY . .

# Set the PYTHONPATH environment variable to /app to ensure Python modules are found
ENV PYTHONPATH /app/

# Expose port 5153 to allow traffic to reach the application
EXPOSE 5153

# Define the command to run the Flask application, binding it to all network interfaces
# and specifying the port on which it should run
CMD ["flask", "run", "--host", "0.0.0.0", "--port", "5153"]