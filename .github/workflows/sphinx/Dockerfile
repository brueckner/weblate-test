FROM sphinxdoc/sphinx

COPY ../requirements.txt /docs
COPY ../source /docs
COPY ../locales /docs/locales
RUN pip3 install -r requirements.txt

# Copies your code file from your action repository to the filesystem path `/` of the container
COPY entrypoint.sh /entrypoint.sh

# Executes `entrypoint.sh` when the Docker container starts up
ENTRYPOINT ["/entrypoint.sh"]
