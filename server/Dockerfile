FROM python:3.12.0-slim-bookworm

# Environment variables to avoid .pyc files and enable unbuffered output
ENV PYTHONBUFFERED 1
ENV PYTHONWRITEBYTECODE 1
ENV APP=/app

# Set working directory
WORKDIR $APP

# Copy and install dependencies
COPY requirements.txt $APP
RUN pip install --upgrade pip && pip install -r requirements.txt

# Copy project files
COPY . $APP

# Expose port 8000
EXPOSE 8000

# Give execution permission to entrypoint.sh
RUN chmod +x /app/entrypoint.sh

# Run entrypoint script first, then start Gunicorn
ENTRYPOINT ["/bin/bash", "/app/entrypoint.sh"]
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]
