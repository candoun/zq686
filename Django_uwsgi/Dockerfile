FROM django:1.8.5-python2

WORKDIR /usr/src/app

#RUN pip install mysqlclient psycopg2 django==1.8.4
# freetds-dev just for pip install pymssql==2.1.3

RUN apt-get update && apt-get install -y \
		gcc g++ autoconf automake make \
		vim \
		telnet \
		freetds-dev \
		libpcre3 \
		libpcre3-dev \
	--no-install-recommends && rm -rf /var/lib/apt/lists/*
	
# RUN pip install --no-cache-dir cx_Oracle	
ENV CELERY_VERSION 3.1.19

RUN pip install celery=="$CELERY_VERSION"

COPY requirements.txt ./
RUN pip install --upgrade --no-cache-dir -r requirements.txt
RUN set -ex;\
    find /usr/local -depth \
	\( \
	    \( -type d -a \( -name test -o -name tests \) \) \
		-o \
	    \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
	\) -exec rm -rf '{}' +; \
    rm requirements.txt

COPY Django-1.8.4.tar.gz ./
RUN tar -zxvf Django-1.8.4.tar.gz && cd Django-1.8.4 && pwd && python setup.py install

CMD ["/bin/bash"]
