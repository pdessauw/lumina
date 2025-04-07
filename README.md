# Lumina - Setup your LLM locally

## Disclaimer

This tool has been tested on a Nvidia GPU. Instructions *will* differ for other GPU 
brands.

## Pre-requisites

The following software and files should be available on the target machine:
* [Docker](https://docs.docker.com/engine/install/),
* [Nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html),
* Your favorite LLM ([Hugging Face](https://huggingface.co/) is a good place to start)

## Installation

### Environment file 

Update environment variables located in `deploy.env`. It is advised to create a copy of 
this file to facilitate debugging and future deployments.

| Variable        | Description                                        |
|-----------------|----------------------------------------------------|
| SGLANG_IMAGE    | Image identifier for SGLang                        |
| MODEL_DIRPATH   | Path to the local folder where the LLMs are stored |
| MODEL_FNAME     | Name of the model directory / file                 |
| OPENWEBUI_IMAGE | Image identifier for OpenWebUI                     |
| NGINX_IMAGE     | Image identifier for Nginx                         |
| HTTP_PORT       | HTTP port for Nginx                                |
| HTTPS_PORT      | HTTPS port for Nginx                               |

### SSL certificates

Place the SSL certificates in the *nginx/ssl* folder. To create self-signed certificates,
run:
```bash
openssl req \
  -newkey rsa:2048 \
  -nodes -subj "/CN="localhost \
  -keyout nginx/openwebui.key \
  -x509 -days 365 \
  -out nginx/openwebui.crt
```

Please note that the default names (*openwebui.crt* and *openwebui.key*) are linked to 
the nginx configuration in *nginx/conf.d*. If you change the default names, remember to
propagate the change in the nginx configuration as well!

### Deploy the stack

```shell
DEPLOY_ENV="deploy.env"  # Replace by the name of the env file.
docker compose --env-file ${DEPLOY_ENV} up -d
```

### Access the chatbot

Within a few minutes of deployment, the chatbot will be ready at 
`https://localhost:${HTTPS_PORT}`. The variable `HTTPS_PORT` is defined in the env file.
