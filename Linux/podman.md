---
tags: [docker, podman, oci, container, build]
---
### "SHELL is not supported for OCI image format" when building with podman
Need to add `--format docker`
```bash
podman build --format docker -t my-docker-container .
```

### Login to docker.io to push containers to docker hub
```bash
podman login docker.io
```

### Allow container to use Host network (UNSAFE FOR PRODUCTION)
Important part is `--network=host`, this line itself will open a docker container at your current directory and has neovim, node, rust, libssl-dev and my plugins preinstalled
```bash
podman run -it --rm -v $PWD/:/workdir --network=host gianpdev/neovim-rust-docker
```

### Setting volume on containers in windows
`//d` is the drive letter and folders are separated by `/` instead of `\`
```bash
podman run -it --rm -v //d/dev/folder:/workdir neovim_rust_docker
```
