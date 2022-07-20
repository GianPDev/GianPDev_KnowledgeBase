---
tags: [docker, podman, oci, container, build]
---
### "SHELL is not supported for OCI image format" when building with podman
Need to add `--format docker`
```bash
podman build --format docker -t my-docker-container .
```

