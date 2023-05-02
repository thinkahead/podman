# podman

## Commands
Install Vagrant from https://www.vagrantup.com/downloads with Binary install. You may need to upgrade ```vagrant plugin update```

```
cd /Users/karve/Downloads/6x6orchestration/podman
vagrant up
# vagrant destroy
```

## Modify the VirtualBox to forward port 8080 to host
```
VBoxManage controlvm podman natpf1 "jupyter,tcp,,8080,,8080"
```

## Wordpress deployment with 2 containers in a pod
```
podman play kube wordpress-deployment.yaml
podman pod stop wordpress-pod-0
podman pod start wordpress-pod-0
podman pod ps --filter label=app=wordpress -q | xargs podman pod rm -f
```

## Wordpress pods
```
podman play kube wordpress-pod.yaml
podman container ps -ap
podman pod ps
podman pod ps --filter label=app=wordpress
podman run -it --name runtop --pod wordpress docker.io/library/alpine:latest top
podman container rm runtop
podman pod stop wordpress
podman pod start wordpress
podman pod rm wordpress -f
```

## Running a Notebook using Jupyter
```
podman play kube notebook.yaml
podman container logs test-notebook-pod-0-test-notebook-container
```

## Running a nginx deployment with replicas
The YAML specifies three replicas, so Podman created three pods, each with one container.
```
podman play kube nginx-deployment.yaml
podman pod ps --filter label=app=nginx
```

## References
https://www.redhat.com/sysadmin/replace-docker-podman-macos

https://www.redhat.com/sysadmin/compose-podman-pods

https://www.redhat.com/sysadmin/podman-play-kube

https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#create_a_pod

https://github.com/rhjhunt/container-workshop

https://itnext.io/podman-and-skopeo-on-macos-1b3b9cf21e60
https://developers.redhat.com/blog/2020/02/12/podman-for-macos-sort-of#

## Larger disk size
```
#Cannot umount /home. Once inside I switched to root and closed my own session like this:
vagrant ssh
cd /
exec sudo su
umount /home

fdisk /dev/sda
Delete partition 5 and recreate it with full size
w
btrfs filesystem resize max /
reboot

vagrant ssh
```
