# Build Container Image GitHub Action

The `action.yaml` file is a configuration for a GitHub Action aimed at building and pushing a container image to a container registry. This GitHub Action is designed to automate the process of building and deploying Docker images, which includes several important steps such as checking out the source code, setting up the Node.js environment, installing dependencies, building static assets, setting up Docker Buildx, caching Docker layers, logging into the container registry, and finally building and pushing the Docker image to the registry.

## General Information

- **name**: The name of this GitHub Action, which is "Build Container Image".
- **description**: A brief description of the purpose of this action, which is "Build and Push to Registry".

## Inputs

### Registry Config

- **registry_name**: The name of the container registry to be used. The default is `ghcr.io`.
- **registry_username**: The username for authenticating to the container registry.
- **registry_password**: The password for authenticating to the container registry.
- **push**: Determines whether the container image will be pushed to the registry. The default is `true`.

### Docker Config

- **context**: The Docker build context. The default is the current directory (`.`).
- **dockerfile**: The name of the Dockerfile to be used. The default is `Dockerfile`.
- **image_name**: The name of the image to be built.
- **image_tag**: The tag of the image to be built. The default is `latest`.
- **target**: The multistage Docker target to be used. The default is an empty string.

### Composer Config

- **composer_github_auth**: The GitHub token used to allow Composer to install private packages.

### Env Config

- **copy_env**: Determines whether the `.env.example` file will be copied to `.env`. The default is `true`.

## Steps

1. **Checkout**: Uses `actions/checkout@v4` to check out the source code from the repository.
2. **Setup Node.js**: Uses `actions/setup-node@v2` to set up the Node.js environment version 14.
3. **Install Dependencies**: Runs `npm install` to install the project's dependencies.
4. **Build Static Assets**: Runs commands to build static assets, including copying the `.env.example` file to `.env` if needed, and running `npm run prod`.
5. **Setup Docker Buildx**: Uses `docker/setup-buildx-action@v1` to set up Docker Buildx.
6. **Cache Docker Layers**: Uses `actions/cache@v4` to cache Docker layers.
7. **Login to Registry**: Uses `docker/login-action@v1` to log in to the container registry using the `registry_name`, `registry_username`, and `registry_password` inputs.
8. **Build and Push**: Uses `docker/build-push-action@v2` to build and push the Docker image to the registry using the various inputs defined earlier.

Overall, the `action.yaml` file orchestrates a series of steps required to automatically build and push Docker images using GitHub Actions, facilitating the Continuous Integration and Continuous Deployment (CI/CD) process in our project.