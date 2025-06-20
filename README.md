
# Martijn van der Made

https://github.com/mvandermade/made-funicular-postzegel-reporter-kotlin/blob/main/docker-compose.yml
https://github.com/mvandermade/made-duper-kubernetes/tree/main/kubernetes_playground/postzegel-reporter/app
https://github.com/mvandermade/made-duper-kubernetes/blob/main/kubernetes_playground/postzegel-reporter/local_dev/made.sh
https://github.com/mvandermade/made-duper-kubernetes/blob/main/kubernetes_playground/postzegel-backend/local_dev/made.sh
https://github.com/mvandermade/made-funicular-postzegel

Address: https://postzegel.tryin.top/

* First time:
  ```shell
  create-host-volume mmade-postzegel  # on server
  ```
  
* Each time:
  ```shell
  helmf mmade-postzegel mmade/postzegel/
  ```
