FROM python:2.7


EXPOSE 9000

RUN apt-get update && apt-get install -y --no-install-recommends libldap2-dev libsasl2-dev && rm -rf /var/lib/apt/lists/*
RUN pip install --no-cache-dir python-ldap

COPY backend-sample-app.py /usr/src/

CMD ["python", "/usr/src/backend-sample-app.py"]