# podman

## Commands
Install Vagrant from https://www.vagrantup.com/downloads with Binary install. YOu may need to upgrade ```vagrant plugin update```

```
cd /Users/karve/Downloads/6x6orchestration/podman
vagrant up
```

Modify the VirtualBox to forward port 8080 to host
```
VBoxManage controlvm podman natpf1 "jupyter,tcp,,8080,,8080"
```
```
podman play kube wordpress-deployment.yaml
podman pod stop wordpress-pod-0
podman pod start wordpress-pod-0
podman pod ps --filter label=app=wordpress -q | xargs podman pod rm -f

podman play kube wordpress-pod.yaml
podman container ps -ap
podman pod ps
podman pod ps --filter label=app=wordpress
podman run -it --name runtop --pod wordpress docker.io/library/alpine:latest top
podman container rm runtop
podman pod stop wordpress
podman pod start wordpress
podman pod rm wordpress -f

vagrant destroy
```

Running a Notebook using Jupyter
```
podman play kube notebook.yaml
podman container logs test-notebook-pod-0-test-notebook-container
```

## References
https://www.redhat.com/sysadmin/replace-docker-podman-macos

https://www.redhat.com/sysadmin/compose-podman-pods

https://www.redhat.com/sysadmin/podman-play-kube

https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#create_a_pod
