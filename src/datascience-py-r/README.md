# Data Science with Python and R

## Summary

*Data science and Jupyter Notebooks development with Python and R. Installs dependencies from your requirements.txt file, and the Python, R, and Jupyter VS Code extensions.*

| Metadata | Value |  
|----------|-------|
| *Categories* | Core, Languages |
| *Image type* | Dockerfile |
| *Published image* | ghcr.io/microsoft/... |
| *Published image architecture(s)* | x86-64 |
| *Container host OS support* | Linux, macOS, Windows |
| *Container OS* | Ubuntu |
| *Languages, platforms* | Python, R, Jupyter |

## Using this image

### Configuration

You can directly reference pre-built versions of `.devcontainer/Dockerfile` by using the `image` property in `.devcontainer/devcontainer.json`.

Refer to [this guide](https://containers.dev/guide/dockerfile) for more details.

#### Installing or updating Python utilities

This container installs all Python development utilities using [pipx](https://pipxproject.github.io/pipx/) to avoid impacting the global Python environment. You can use this same utility add additional utilities in an isolated environment. For example:

```bash
pipx install prospector
```

Note that if you change the version of Python from the default, you'll need to run a few commands to update the utilities and `pipx`. More on that next.

#### Installing a different version of Python

You can install different versions of Python by changing the Python feature version in the `devcontainer.json` file.

You can install different versions of Python than the one in this image by running the following from a terminal (as covered in the [user FAQ](https://docs.anaconda.com/anaconda/user-guide/faq) for Anaconda):

```bash
conda install python=3.6
pip install --no-cache-dir pipx
pipx uninstall pipx
pipx reinstall-all
```

See the [pipx documentation](https://pipxproject.github.io/pipx/docs/) for additional information.

#### [Optional] Using the forwardPorts property

By default, frameworks like Flask only listens to localhost inside the container. As a result, we recommend using the `forwardPorts` property (available in v0.98.0+) to make these ports available locally.

```json
"forwardPorts": [5000]
```

The `appPort` property [publishes](https://docs.docker.com/config/containers/container-networking/#published-ports) rather than forwards the port, so applications need to listen to `*` or `0.0.0.0` for the application to be accessible externally. This conflicts with the defaults of some Python frameworks, but fortunately the `forwardPorts` property does not have this limitation.

### [Optional] Adding the contents of reqeuirements.txt to the image

This image will automatically install dependencies from the `requirements.txt` file in the parent folder when the container is built. You can change this behavior by altering the `postCreateCommand` in the `devcontainer.json`.

## License

Copyright (c) Microsoft Corporation. All rights reserved.

Licensed under the MIT License. See [LICENSE](https://github.com/devcontainers/images/blob/main/LICENSE)