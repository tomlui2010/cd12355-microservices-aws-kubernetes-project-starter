FROM python:3.9-slim-buster

# Setup and activate virtual python environment 
ENV VIRTUAL_ENV=~/.venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Working Directory
WORKDIR /app

# Copy requirements.txt
COPY requirements.txt .

# Install packages from requirements.txt
# hadolint ignore=DL3013
RUN pip install --no-cache-dir --upgrade pip &&\
    pip install --trusted-host pypi.python.org --no-cache-dir -r requirements.txt

# Copy source code
COPY . .

# Set the Python path
ENV PYTHONPATH /app/

EXPOSE 5153

CMD ["flask", "run", "--host", "0.0.0.0"]
