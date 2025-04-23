FROM python:3.6
RUN mkdir /code
WORKDIR /code  
COPY . /code
RUN pip install --no-cache-dir -r requirements.txt  
ENV REDIS_HOST=redis-stack-server
ENV REDIS_PORT=6379
ENV REDIS_CHANNEL=log_channel
EXPOSE 3000
CMD ["python", "/code/main.py"]