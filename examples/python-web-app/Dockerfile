# Use the official Ubuntu image as the base
FROM ubuntu:20.04

# Set the working directory
WORKDIR /app

# Copy the requirements file first to leverage Docker cache
COPY requirements.txt /app/

# Install Python, pip, and venv
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv

# Create a virtual environment
RUN python3 -m venv venv

# Install the Python packages in the virtual environment
RUN . venv/bin/activate && pip install --upgrade pip && pip install -r requirements.txt

# Copy the rest of the application code
COPY devops /app

# Set environment variables to use the virtual environment
ENV VIRTUAL_ENV=/app/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Set the entry point to use the virtual environment's Python
ENTRYPOINT ["python"]

# Set the default command to run your application
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
