### Fork this repo and adapt it for your environment

Make sure you have a default block storage class. 

First, fork this repo. Update the following files that refer to your repo url:

- [kustomization.yaml](./argocd/kustomization.yaml)
- [bootstrap.yaml](./argocd/bootstrap.yaml)

Update the dnsNames for certificates with the correct ingress subdomain:

- [mq-cert-domain.yaml](./components/mq/variants/cloudprovider/odf/mq-cert-domain.yaml)
- [route-certificate-domain.yaml](./components/eventstreams/variants/cloudprovider/odf/route-certificate-domain.yaml)

Install ArgoCD and add applications:

* Add openshift-gitops operator
* Apply the ArgoCD [bootstrap.yaml](./argocd/bootstrap.yaml) to the cluster

Config for installed components:

* The sample application uses [MicroProfile Config](https://openliberty.io/docs/latest/external-configuration.html). Create liberty-config secret in the liberty namespace. 

  Add these keys and values:

  `MP_MESSAGING_CONNECTOR_LIBERTY_KAFKA_BOOTSTRAP_SERVERS` with value `SASL_SSL://eventstreams-kafka-external-bootstrap-eventstreams.apps.<INGRESS>:443`

  `MP_MESSAGING_CONNECTOR_LIBERTY_KAFKA_SASL_JAAS_CONFIG` with value `org.apache.kafka.common.security.scram.ScramLoginModule required username="<USERNAME>" password="<PASSWORD>";`

  `CONNECTION_NAME_LIST` with value `native-ha-qm-ibm-mq-qm-mq.apps.<INGRESS>(443)` for using MQ via OpenShift route, or for the service `native-ha-qm-ibm-mq.mq.svc.cluster.local(1414`

* To access the MQ web UI, create a secret 'mqwebusersecret' with password in the mq namespace, example here: [mqwebuser-secret-example.yaml](./components/mq/base/native-ha-qm/mqwebuser-secret-example.yaml)
