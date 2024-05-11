# Use the official Python 3.8 image as the base image
FROM python:3.8

# Set the working directory in the container
WORKDIR /app

# Copy the dependencies file to the working directory
COPY requirements.txt .

# Install any dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Install gunicorn
RUN pip install gunicorn

# Copy the content of the local src directory to the working directory
COPY . /app

# Expose port 5000 to the outside world
EXPOSE 5000

# Command to run the application using Gunicorn
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "app:app"]
