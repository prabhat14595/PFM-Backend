# Use an official Python runtime as a parent image
FROM python:3.10-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container at /app
COPY requirements.txt /app/

# Install any dependencies
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Copy the current directory contents into the container at /app
COPY . /app/

# Ensure the Django manage.py script is executable
RUN chmod +x /app/manage.py

# Expose port 8000 for Django
EXPOSE 8000

# Start a bash shell by default, can be overridden by docker-compose command
# CMD ["bash"]
# Define the command to run the Django application
CMD ["python", "/app/manage.py", "runserver", "0.0.0.0:8000"]
