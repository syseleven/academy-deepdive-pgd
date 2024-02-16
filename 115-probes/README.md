# Probes

## Preparation

* Before you begin with the actual exercise please make sure to follow these steps to work in your own environment:

  ```shell
  # "Please enter your name (without blanks e.g. johndoe)"
  export YOURNAME=<johndoe>
  kubectl create ns ${YOURNAME}
  kubectl config set-context --current --namespace=${YOURNAME}
  ```

* Clone this repository to your working station and change into the directory for the following exercises

---

## Exercise

## Readiness and Liveness Probes

* Create an nginx deployment with `readinessProbe` and `livenessProbe` set.
* Verify if the pod is running.

  ```shell
  kubectl apply -f deploy-probes.yaml
  kubectl get po -l app=nginx-probes
  ```

* Verify the liveness probe is executed and successful

  ```shell
  kubectl logs -f -l app=nginx-probes
  ```

* Expected result:

  ```shell
  2024/02/16 08:29:16 [notice] 1#1: start worker process 34
  ::1 - - [16/Feb/2024:08:29:21 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/7.74.0" "-"
  ::1 - - [16/Feb/2024:08:29:26 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/7.74.0" "-"
  ::1 - - [16/Feb/2024:08:29:31 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/7.74.0" "-"
  ```

### Clean up

* Delete the deployment

  ```shell
  kubectl delete -f deploy-probes.yaml
  ```
