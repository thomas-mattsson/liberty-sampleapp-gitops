
### Fork this repo and adapt it for your environment

First, fork this repo. Update the following files that refer to your repo url:

- [kustomization.yaml](./argocd/kustomization.yaml)
- [bootstrap.yaml](./argocd/bootstrap.yaml)

Update the dnsNames for certificates with the correct ingress subdomain

- [mq-cert-domain.yaml](./components/mq/variants/cloudprovider/odf/mq-cert-domain.yaml)
- [route-certificate-domain.yaml](./components/eventstreams/variants/cloudprovider/odf/route-certificate-domain.yaml)

Install ArgoCD and add applications

* Add openshift-gitops operator
* Apply the ArgoCD [bootstrap.yaml](./argocd/bootstrap.yaml) to the cluster

Config for installed components

* Create mqwebusersecret with password in mq namespace, example here: [mqwebuser-secret-example.yaml](./components/mq/base/native-ha-qm/mqwebuser-secret-example.yaml)

* Create eventstreams-scram-auth secret in liberty using the created password for the admin user in the event streams namespace. The sample application uses [MicroProfile Config](https://openliberty.io/docs/latest/external-configuration.html) 
