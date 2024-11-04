# Nitrokey's User Documentation

- [Initial Setup](#Initial-Setup)
- [Building the docs](#Building-the-docs)
- [Local testing webserver](#Local-testing-webserver)
- [Local Weblate instance](#Local-Weblate-instance)

## Initial Setup

Clone the repo and switch to the `develop` branch.
```bash
git clone git@github.com:Nitrokey/nitrokey-documentation.git
cd nitrokey-documentation
git checkout develop
```

Set up local environment variables.
```bash
cp .env.example .env
nano .env

# Change these .env variables accordingly:
#
# Mandatory:
#
# WEBLATE_URL:      this can your local instance of weblate (https://hub.docker.com/r/weblate/weblate) 
#                   or the URL of the test-server's weblate instance
# WEBLATE_API_KEY:  from WEBLATE_URL at: /accounts/profile/#api
# SPHINX_PATH:      the full path to where this repository has been checked out at
# LOGFILE_PATH:     can be the same as SPHINX_PATH

# Optional:
#
# PRIORITY_LANGUAGES:   modify to your needs
# OTHER_LANGUAGES:      will be used for full builds
```

Use `docker-compose.override.yml.example` if you run into permission-troubles with docker. Copy the file and remove the `.example`-suffix, then add your user and group ids. This will force all files created by docker to be created by that user and group.

To get your user's id and group (on linux or mac), type:
```bash
# this will get you a numeric user_id:group_id
echo "$(id -u):$(id -g)"
```

Next, build the container image.
```bash
bash build-container-image.sh
```

## Building the docs

```bash
# Build PRIORITY_LANGUAGES
bash build-docs.sh

# Build a specific language
bash build-docs.sh de

# Build all languages
bash build-docs.sh --all-languages
```

## Local testing webserver
You may serve the docs using any local webserver you want, or use this command to start a local nginx server with docker on port 8080.
```bash
bash serve-docs.sh
```

The docs will be accessible at:             
http://localhost:8080/en/

## Local Weblate instance
The easiest way to run weblate locally is using the official docker image: https://hub.docker.com/r/weblate/weblate

Once set up, create a project called `Nitrokey Documentation` and import a backup zip-file from:       
https://translate.nitrokey.com/backups/nitrokey-documentation/

Before trying to import this pretty big zip file, you need to override some container variables:

In the weblate repo's `docker-compose.override.yml`, add:
```yml
CLIENT_MAX_BODY_SIZE: 5000M
```
