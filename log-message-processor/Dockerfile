FROM python:3.6
RUN mkdir /code
WORKDIR /code  
COPY . /code
RUN pip install --no-cache-dir -r requirements.txt  
EXPOSE 3000
CMD ["python", "/code/main.py"]