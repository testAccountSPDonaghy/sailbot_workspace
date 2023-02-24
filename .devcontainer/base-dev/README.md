# Base and Dev Images

## Features

- The base image builds off the the [`pre-base`](../pre-base/pre-base.Dockerfile) image and adds additional dependencies
- The dev image build off the base image and:
    - Installs software that is nice to have for development
    - Adds a non-root user
    - Initializes the ROS log and bash history volumes
        - Docker volumes are used to persist data generated by and used by containers
    - Updates the bash configuration file, `~/.bashrc`

## How to build

For example, the steps required to add a development dependency:

1. In [`base-dev.Dockerfile`](base-dev.Dockerfile), add the dependency and push your changes
2. In the [Build Images workflow](https://github.com/UBCSailbot/sailbot_workspace/actions/workflows/build-images.yml),
   select "Run workflow"
3. In "Use workflow from", select the branch that your changes are in
4. Update "Base and dev image tag" with a short description of the changes; for example, `add-vim`
5. Click "Run workflow"
6. In [`.devcontainer/Dockerfile`](../Dockerfile), update the dev image tag with the short description above
7. Once the workflow successfully completes:
    1. Run the "Dev Containers: Rebuild Container" VS Code command to use the newly built image in your Dev Container
    2. Push your changes so that the CI runs with the newly built image