# Generator for Kubernetes resources using Kustomize and Skaffold

This generator creates the resources to deploy a Spring Boot application and a MySQL Database.

You will need to install the following command line tools

* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [kustomize](https://kubernetes-sigs.github.io/kustomize/installation/)
* [skaffold](https://skaffold.dev/docs/install/)


## Generator Commands

The Tanzu Starter Service can run these generator commands on the server when creating a new project.  Alternatively, you can run the generator command using the Tanzu Starter Service CLI named `tss`.

**TODO: LINK TO DOWNLOAD CLIENT**

`k8s new` creates

* A `skaffold.yaml` file in the root directory
* A kustomize directory structure with an overlay named `local`.  The kustomize file is located in `kubernetes/overlays/local/kustomization.yaml`
* Adds the [Jib Maven Plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the Maven `pom.xml` under the profile `local`
* Adds an Spring Actuator dependency to the Maven `pom.xml` if it is not already present

`k8s update` creates
* A kustomize directory structure with an overlay named `local-services` for MySql if the project has a dependency on the `mysql-connector-java` library.

## Running the application and services

Once the generator commands have be executed you can run the application and services.

To run the application's dependent services, execute the command

* `skaffold run -p local-services`

To run the application, execute the command

* `skaffold run -p local`

If running on `minikube` you can retrieve the route for the application using `minikube service list`.  As you make changes to the application, execute the `skaffold run -p local` command to rebuild the container and update the application running in the Kubernetes cluster.

To delete the application's dependent services, execute the command

* `skaffold delete -p local-services`

To delete the application, execute the command

* `skaffold delete -p local`