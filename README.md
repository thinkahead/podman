# podman

## Commands
```
cd /Users/karve/Downloads/6x6orchestration/podman
vagrant up

podman play kube wordpress-deployment.yaml # 
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

## References
https://www.redhat.com/sysadmin/replace-docker-podman-macos

https://www.redhat.com/sysadmin/compose-podman-pods

https://www.redhat.com/sysadmin/podman-play-kube

https://developers.redhat.com/blog/2019/01/15/podman-managing-containers-pods#create_a_pod
