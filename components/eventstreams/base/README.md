Sample eventstreams instance and topic configured with Kafka Connect and a Connector to the queue defined here: [qm.yaml](../../mq/base/singleinstance-qm/qm.yaml)

Based on https://dalelane.co.uk/blog/?p=4615


Consume with:

kcat -C -b eventstreams-kafka-external-bootstrap-eventstreams.apps.6602d6121b0194001e821256.cloud.techzone.ibm.com:443 -t DOOR.BADGEIN -X security.protocol=SASL_SSL -X sasl.mechanism=SCRAM-SHA-512 -X sasl.username=<username> -X sasl.password=<password>  -X enable.ssl.certificate.verification=false -o end -u | jq
