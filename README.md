
# Postzegel!

The Helm chart for https://github.com/mvandermade/made-funicular-postzegel

Some links:

https://github.com/mvandermade/made-funicular-postzegel-reporter-kotlin/blob/main/docker-compose.yml
https://github.com/mvandermade/made-duper-kubernetes/tree/main/kubernetes_playground/postzegel-reporter/app
https://github.com/mvandermade/made-duper-kubernetes/blob/main/kubernetes_playground/postzegel-reporter/local_dev/made.sh
https://github.com/mvandermade/made-duper-kubernetes/blob/main/kubernetes_playground/postzegel-backend/local_dev/made.sh
https://github.com/mvandermade/made-funicular-postzegel

Address: https://postzegel.tryin.top/

* First time create a node volume
  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: mmade-postzegel-pv
  spec:
    capacity:
      # space limit, not reserved
      storage: 4Gi
    volumeMode: Filesystem
    accessModes:
      - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    hostPath:
      path: $DIR
  ```

* And tag the node to schedule all pods on the one that has the volume
  ```shell
  kubectl label node "NODENAME" has-local-volume-mmade-postzegel="1"
  ```
  
* Each time:
  ```shell
  helm upgrade --install --create-namespace -n mmade-postzegel mmade-postzegel mmade/postzegel/
  ```
