# Helmfile

Helmfile is a tool to combine multiple Helm Charts and their respective installation commands.

## Preparation

* Before you begin with the actual exercise please make sure to follow these steps to work in your own environment:

  ```shell
  read -p "Please enter your name (without blanks e.g. johndoe): " YOURNAME
  export YOURNAME
  kubectl create ns ${YOURNAME}
  kubectl label namespace ${YOURNAME} deepdive-pgd=true
  kubectl config set-context --current --namespace=${YOURNAME}
  ```

* Clone this repository to your working station and change into the directory for the following exercises

---

* Helmfile project [on GitHub](https://github.com/helmfile/helmfile)

* Install the tool `helmfile` following its [documentation](https://github.com/helmfile/helmfile/tree/main#installation)

* Verify installation

  ```shell
  $ helmfile --version
  helmfile version x.xxx.x
  ```

---

## Task

Install two separate Helm Charts in combination using helmfile.
Inspect each Helm Chart first and then proceed with the installation.

* Inspect `nginx` and `phpfpm` chart with their templates and values.
* Inspect the `helmfile.yaml`
  * Note the `needs` section.

* Note: In this example two local charts are combined.
  * What combinations are possible?
    * local / local
    * local / remote
    * remote / remote

---

* Use helmfile to show diffs regarding the workshop cluster.
  * What are the differences?

  ```shell
  helmfile diff
  ```

* Install the Helm charts now
  ```shell
  helmfile -n $YOURNAME apply
  ```

* Verify the installation with these commands
  * `helm -n $YOURNAME list`
  * `helm -n $YOURNAME get manifest`

* Create a port-forward to reach the demo application
  * `kubectl -n $YOURNAME port-forward svc/nginx 8080:80`
  * Visit URL: http://localhost:8080
  * Result: a PHP info page is displayed

---

## Clean up

* Uninstall the helm releases
  * `helmfile -n $YOURNAME destroy`

---

## Conclusion

It stores all installation instructions in one single file which can be used for documentation and IaaC.

It creates another layer of abstraction.

Key features:
- combine Helm Charts from different places (local, registry)
- inject multiple values files
- create dependencies between the releases
