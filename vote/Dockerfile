# Base stage with dependencies
FROM python:3.11-alpine AS base
WORKDIR /usr/local/app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Development stage (matching docker-compose target)
FROM base AS dev
COPY . .
RUN chown -R appuser:appgroup /usr/local/app
USER appuser
EXPOSE 80
CMD ["python", "app.py"]

# Final production stage
FROM dev AS final
CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]
