# Base image là Python
FROM python:3.10-slim

# Đặt thư mục làm việc bên trong container
WORKDIR /app

# Sao chép file requirements.txt vào container
COPY requirements.txt /app/

# Cài đặt thư viện từ requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Sao chép mã nguồn ứng dụng vào container
COPY . /app

# Mở cổng ứng dụng Flask
EXPOSE 5000

# Chạy ứng dụng Flask
CMD ["python", "app.py"]
