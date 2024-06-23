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
EXPOSE 80

# Start a bash shell by default, can be overridden by docker-compose command
# CMD ["bash"]
# Define the command to run the Django application
# CMD ["python", "/app/manage.py", "runserver", "0.0.0.0:8000"]

# Install Apache HTTP server
RUN apt-get update && apt-get install -y apache2

# Configure Apache to proxy requests to Django
COPY apache/django.conf /etc/apache2/sites-available/
RUN a2enmod proxy proxy_http
RUN a2ensite django.conf
RUN service apache2 restart

# Start Apache HTTP server
CMD ["apache2ctl", "-D", "FOREGROUND"]
