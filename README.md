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
| OPENWEBUI_PORT  | OpenWebUI web interface port                       |

### Deploy the stack

```shell
DEPLOY_ENV="deploy.env"  # Replace by the name of the env file.
docker compose --env-file ${DEPLOY_ENV} up -d
```

### Access the chatbot

Within a few minutes of deployment, the chatbot will be ready at 
`http://localhost:${OPENWEBUI_PORT}`. The variable `OPENWEBUI_PORT` is defined in the env
file.
