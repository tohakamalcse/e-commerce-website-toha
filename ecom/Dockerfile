# Use official Python image
FROM python:3.10-slim

# Set working directory inside container
WORKDIR /app

# Install system dependencies for PostgreSQL and build tools
RUN apt-get update && apt-get install -y gcc libpq-dev && rm -rf /var/lib/apt/lists/*

# Copy only requirements first to leverage Docker cache
COPY requirements.txt .

# Upgrade pip and install dependencies
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

# Copy the entire Django project (current folder) into container
COPY . .

# Expose Django port
EXPOSE 8000

# Run Django app with Gunicorn
CMD ["gunicorn", "ecom.wsgi:application", "--bind", "0.0.0.0:8000"]
