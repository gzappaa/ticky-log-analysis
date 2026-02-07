# Use Python 3.11 slim
FROM python:3.11-slim

# Set working directory inside container
WORKDIR /app

# Copy source code and scripts
COPY src/ src/
COPY scripts/ scripts/

# Create folders for CSVs and HTMLs
RUN mkdir -p /app/data /app/html

# Default command: run analysis and generate CSVs + HTMLs
CMD python3 src/ticky_check.py && \
    python3 scripts/csv_to_html.py data/error_message.csv html/errors.html && \
    python3 scripts/csv_to_html.py data/user_statistics.csv html/users.html
