---
title: Kubernetes attach an ad-hoc pod to a PVC
tags:
    - kubernetes
    - k8s
    - containers
---

# Kubernetes attach an ad-hoc pod to a PVC

## Create pod
~~~ bash
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Pod
metadata:
  name: pvc-adhoc
spec:
  containers:
  - image: busybox
    name: pvc-adhoc
    command:
      - tail
    args:
      - -f
      - /dev/null
    volumeMounts:
    - mountPath: /pvc
      name: pvc
  volumes:
  - name: pvc
    persistentVolumeClaim:
      claimName: pvc
EOF
~~~

## Exec into pod & list volume contents
~~~ bash
kubectl exec -it pvc-adhoc -- sh

ls -la /pvc
~~~

## Delete pod
~~~ bash
kubectl delete pod pvc-adhoc
~~~
