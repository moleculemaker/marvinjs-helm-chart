# marvinjs-helm-chart
Helm chart for running MarvinJS Webservices in a Kubernetes cluster


## References
* Docker Compose recipe: [ChemAxon/marvinjs-docker-example](https://github.com/ChemAxon/marvinjs-docker-example/blob/master/official_image/mjs-with-official-license-server.yml)

### License File
If you have a license file (instead of a license key), mount it into the container at runtime:
```
/home/cxnapp/.chemaxon/licenses/license.cxl
```

Create a secret from the file using the following:
```bash
kubectl create secret generic marvinjs-license --from-file=license.cxl
```

And specify this secret name as the value for `controller.license.secretFile`.


## PSA: Always check Pod `AGE` after deploying
You may need to delete the running Pod to trigger a new Pod to be created with the new config.


## Local
If you are running Docker + Kubernetes locally on your laptop, you can use the following to run marvinjs on your local cluster

To change the existing application in your local cluster, you can use the following command:
```bash
$ helm upgrade --install marvinjs -n staging . -f values.local.yaml
```

This will overwrite the configuration of the instance in your local cluster.

You should then be able to access the following URL:
* MarvinJS Demo Canvas: marvinjs.proxy.localhost/demo.html

This example is currently configured to use the NGINX Ingress Controller, but you can adjust values.local.yaml to change the ingress class.


## Staging
To change the existing application in the `staging` namespace, you can use the following command:
```bash
$ helm upgrade --install marvinjs -n staging . -f values.staging.yaml
```

This will overwrite the configuration of the current staging instance.

Swagger UI is available to test the MarvinJS API individually (if desired):
* MarvinJS: marvinjs.staging.mmli1.ncsa.illinois.edu/api/swagger-ui/index.html


## Prod
TBD - prod should look almost identical to `staging`, and will be deployed automatically by ArgoCD once the necessary pieces are in place. Prod will have the same URLs as above, just without the `.staging` in each


## TODOs
* Create ArgoCD apps for staging + prod
