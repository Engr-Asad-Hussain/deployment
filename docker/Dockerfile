FROM python:3.10
LABEL author='Asad Hussain'
LABEL application='Deployment Sample 1.0'

WORKDIR /app

COPY requirements.txt /app/requirements.txt
RUN pip install -r /app/requirements.txt
COPY run.py /app
COPY app /app/app

ENV ENVIRONMENT=production
ENV DEBUG=False
ENV ENABLE_LOGGER=True
ENV LOGGER_LEVEL=20

ENV DATABASE=sample
ENV DB_USERNAME=sample
ENV DB_PASSWORD=sample
ENV DB_HOST=localhost
ENV DB_PORT=3306

EXPOSE 5000
ENTRYPOINT [ "python" ]
CMD [ "/app/app/app.py" ]
