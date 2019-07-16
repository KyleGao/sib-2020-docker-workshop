FROM python:3.7.3-slim-stretch

# To build it outside of docker-compose, in the toplevel directory of the repository,
# run:
#
# $ docker build -f Docker/cathapi/Dockerfile -t cathapi .
#
# where
# - "-t cathapi" just defines a name/ tag
#

# Get API code inside the image
RUN /bin/mkdir /cathapi
ENV SRC_DIR="/cathapi"
COPY ./ $SRC_DIR

WORKDIR $SRC_DIR
# Install system dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ncbi-blast+  \
    mafft        \
    gcc          \
    libc-dev     \
    libpq-dev && \
    /bin/rm -rf /var/lib/apt/lists/* && \
# Install Python dependencies
    /usr/local/bin/pip install --no-cache-dir -r requirements.txt
# Create the secret key
RUN /bin/date | /usr/bin/md5sum > secret_key.txt
# Run the tests
#RUN /usr/local/bin/pytest

COPY Docker/cathapi/entrypoint.sh $SRC_DIR
