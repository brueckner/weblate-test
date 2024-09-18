FROM sphinxdoc/sphinx

WORKDIR /docs
COPY ../../requirements.txt /docs
COPY ../../locales /docs/locales
COPY ../../source /docs
# COPY ../../entrypoint.sh /entrypoint.sh

# RUN pip3 install -r requirements.txt

# # Executes `entrypoint.sh` when the Docker container starts up
# ENTRYPOINT ["/entrypoint.sh"]
