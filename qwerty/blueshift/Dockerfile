# image for running as a container
# make sure we create the blueshift root workspace structure as well.

FROM python:3.6-alpine
MAINTAINER Quantra Blueshift <blueshift-support@quantinsti.com>

ENV PYTHONPATH "${PYTHONPATH}:/blueshift"

COPY requirements.txt /home/blueshift/requirements.txt
COPY ./dist/blueshift-0.0.1.tar.gz /home/blueshift/blueshift-0.0.1.tar.gz
WORKDIR /home/blueshift

RUN apk update
RUN apk add make cmake gcc g++ gfortran libffi openssl linux-headers
RUN apk add libffi-dev openssl-dev build-base python3-dev py3-pip 
RUN pip install cython
RUN pip install numpy
RUN pip install setuptools-scm
RUN pip install -r requirements.txt
RUN pip install blueshift-0.0.1.tar.gz

RUN rm requirements.txt && rm blueshift-0.0.1.tar.gz
RUN addgroup -S blueshift && adduser -S blueshift -G blueshift

USER blueshift

RUN mkdir .blueshift
RUN blueshift config > .blueshift/.blueshift_config.json

CMD ["/bin/sh"]