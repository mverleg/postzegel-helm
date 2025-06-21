
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
    storageClassName: standard
  ```

* Find out the NODENAME using `kubectl get node`

* And tag the node to schedule all pods on the one that has the volume
  ```shell
  kubectl label node "NODENAME" has-local-volume-mmade-postzegel="1"
  ```
  
* Each time:
  ```shell
  helm upgrade --install --create-namespace -n mmade-postzegel mmade-postzegel . --set postgres_pass='p455w0rd!'
  ```

* Check out result:
  ```shell 
  helm ls -n mmade-postzegel
  ```

* Removal
  ```shell
  helm uninstall -n mmade-postzegel mmade-postzegel
  ```
  ```shell
  kubectl delete pv mmade-postzegel-pv
  ```

* Reclaim PV after uninstalling helm
  ```shell
  kubectl patch pv mmade-postzegel-pv -p '{"spec":{"claimRef": null}}'
  ```