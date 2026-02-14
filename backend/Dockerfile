FROM python:3.12-alpine

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

WORKDIR /app

COPY app.py .

EXPOSE 8080

USER appuser

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD wget -qO- http://localhost:8080/ || exit 1

CMD ["python", "app.py"]
