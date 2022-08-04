---
tags: [docker, podman, oci, container, build]
---
### Replacing docker.sock in podman
Install podman-docker
```bash
sudo dnf install podman-docker
```
Run 'sock' in separate terminal (in `-t 0` to forever keep it on)
```bash
podman system service -t 0
```
Use this variable instead of the docker.sock
```bash
-v $XDG_RUNTIME_DIR/podman/podman.sock:/var/run/docker.sock
```
*Running this without `podman system service -t 0` will cause the error: `no such file or directory`*

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

### Install Podman with Nvidia on Fedora (tested on Fedora 36)
From: https://blog.shawonashraf.com/nvidia-podman-fedora-34

```bash
sudo rpm -Uvh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm; sudo rpm -Uvh http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm; sudo dnf update -y
```
Install correct drivers: https://rpmfusion.org/Howto/NVIDIA
Then reboot `sudo reboot`

Install podman if it isn't already installed:
```bash
sudo dnf install podman
```
Check CUDA version (mine was `CUDA Version: 11.7`):
```bash
nvidia-smi
```
Check for latest distribution here: https://nvidia.github.io/nvidia-container-runtime/

Set distribution value to the latest one
```bash
distribution=rhel9
```
Download and install repo:
```bash
curl -s -L https://nvidia.github.io/nvidia-container-runtime/$distribution/nvidia-container-runtime.repo | sudo tee /etc/yum.repos.d/nvidia-container-runtime.repo
```
Install nvidia container runtime
```bash
sudo dnf install nvidia-container-runtime
```
change no-cgroups to true: `no-cgroups = true`
```bash
sudo vi /etc/nvidia-container-runtime/config.toml
```

### Running a container with gpu:
```bash
podman run -it --rm --security-opt=label=disable nvidia/cuda:11.7.0-runtime-ubuntu20.04 nvidia-smi
```
*This should return the same info as running `nvidia-smi` on your own pc*
```bash
--security-opt=label=disable
```
*This is used to avoid selinux from blocking the gpu*

