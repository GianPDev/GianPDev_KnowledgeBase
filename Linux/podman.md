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

### Communicate between containers
Create pod, with `--pod new:PODNAME` . Must add ports when pod is created via `-p 3000:3000` or `-p 5000-6000` for a range of ports
```bash
podman run -d -p 3000:3000 -p 5000:5000 -e "DEFAULT_LAUNCH_ARGS=[\"--window-size=1366,768\"]" --pod new:podchangedetection --restart unless-stopped --shm-size="2g" browserless/chrome:1.53-chrome-stable

podman run -d --pod podchangedetection --restart always -e PLAYWRIGHT_DRIVER_URL="ws://127.0.0.1:3000/?stealth=1&--disable-web-security=true" -v /home/$USER/changedetection/datastore:/datastore --name changedetection.io dgtlmoon/changedetection.io
```

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


### UNSOLVED centos 7 issues (rootless podman)
Main issue just might be that the repo version is 1.6.4-32 vs AlmaLinux 8's version is 4.1.1
### subid error
`ERRO[0000] cannot find mappings for user $USER: No subuid ranges found for user "$USER" in /etc/subuid`
```bash
sudo vi /etc/subuid
```
```bash
sudo vi /etc/subgid
```
```
$USER:10000:65536
```
```
$USER:10000:65536
```
```bash
podman system migrate
```
```bash
#sudo usermod --add-subuids 10000-65536 $USER
#sudo usermod --add-subgids 10000-65536 $USER

#sudo usermod doesn't work properly
```


### TODO systemd user slice session scope error
`Error: stat /sys/fs/cgroup/systemd/user.slice/user-1002.slice/session-14785.scope: permission denied`
```bash
id
#output
uid=1002($USER) gid=1002($USER) groups=1002($USER),10(wheel)
```
```bash
sysctl -a | grep namespaces
# output
user.max_ipc_namespaces = 2147483647
user.max_mnt_namespaces = 2147483647
user.max_net_namespaces = 2147483647
user.max_pid_namespaces = 2147483647
user.max_user_namespaces = 2147483647
user.max_uts_namespaces = 2147483647
# note that user.max_cgroup_namespaces is not here
```
```bash
df -h
# output
Filesystem         Size  Used Avail Use% Mounted on
/dev/ploop40336p1  3.9G  2.0G  1.8G  54% /
none               128M     0  128M   0% /sys/fs/cgroup
none               128M     0  128M   0% /dev
tmpfs              128M   84K  128M   1% /dev/shm
tmpfs              128M  128K  128M   1% /run
tmpfs               26M  8.0K   26M   1% /run/user/1002
# note that /sys/fs/cgroup is none
```
rebooting seems to have removed the error 
```
sudo reboot
```
move on to the next error

### Error unmounting when running container
Error:
```bash
ERRO[0031] error unmounting /home/$USER/.local/share/containers/storage/overlay/6de19278027571121d68fb2cc4240004eaf4cbec8b9e6985162484a3e79aa2ec/merged: invalid argument 
Error: error mounting storage for container 1e79aeeb6f9fd30cd4401876c7aec136e459fdc2cbe35c1c0407cf7d626544bc: error creating overlay mount to /home/$USER/.local/share/containers/storage/overlay/6de19278027571121d68fb2cc4240004eaf4cbec8b9e6985162484a3e79aa2ec/merged: using mount program /usr/bin/fuse-overlayfs: fuse: device not found, try 'modprobe fuse' first
fuse-overlayfs: cannot mount: No such file or directory
```
```bash
# tried
sudo yum install fuse-libs
# doesn't work, trying reboot
Still same error
```
enabled fuse in VPS provider's UI, rebooted both from terminal and VPS provider UI, still didn't mount.
```bash
# tried
modprobe fuse
```
Reinstalling VPS might be required.
Error went away after reinstall VPS with fuse enabled

### slirp4netns failed
```bash
Error: slirp4netns failed: "open(\"/dev/net/tun\"): No such file or directory\nWARNING: Support for sandboxing is experimental\nchild failed(1)\nWARNING: Support for sandboxing is experimental\n"
```
Apparently requires TUN/TAP driver to be enabled (which is also an option on the VPS provider's UI)

This seems to remove that slirp4netns failed
```bash
sudo setcap cap_net_admin=+pe $(which podman)
```
```bash
sudo setcap cap_net_admin=+pe $(which slirp4netns)
```

### cannot write setgroups file
`Error: could not get runtime: cannot write setgroups file: open /proc/468/setgroups: permission denied`

Cannot run `podman run -d --restart always -p 5000:5000 -v /home/$USER/changedetection/datastore:/datastore --network=host --name changedetection.io dgtlmoon/changedetection.io`
Which was working previously, same error as above
I ran this, which caused the issues
```bash
sudo setcap cap_net_admin=+pe $(which podman)
```
unset by:
```bash
sudo setcap -r $(which podman)
```
get cap status (output will be literally nothing if nothing is set)
```bash
getcap $(which podman)
```
```bash
getcap $(which slirp4netns)
```
getting [[podman#slirp4netns failed]] again

Note: tried sudo podman and it worked
reinstalled centos 7 again
ran:
```bash
sudo setcap cap_net_admin=+pe $(which slirp4netns)
#added to /etc/subuid /etc/subgid
$USER:10000:65536
sudo rm /dev/net/tun
sudo mknod /dev/net/tun c 10 200
sudo chmod 0666 /dev/net/tun
modprobe tun
sudo reboot
modprobe tun
sudo modprobe tun
```
Doesn't work. Spent too much time on this. Avoid renting VPS with only CentOS 7 installs allowed.