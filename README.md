# tx-smtp-relay-helm
Helm chart for tx-smtp-relay

This image provides an SMTP relay host for emails from within a Kubernetes cluster.

Configure this container to use an upstream authenticated SMTP relay like SendGrid or your ISP's mail server, and provide an
open relay service to your cluster. This means you don't have to configure all of your containerised services with email auth secrets.

```
helm repo add tx-smtp-relay-helm https://djjudas21.github.io/tx-smtp-relay-helm/
helm repo update
helm upgrade --install -n tx-smtp-relay  [-f values.yaml] --create-namespace djjudas21/tx-smtp-relay
```

As a minimum, you will need to provide your own `values.yaml` with some SMTP config:

| Key               | Required | Use                                  | Example                         |
|-------------------|----------|--------------------------------------|---------------------------------|
| `smtp.host`       | Required | Hostname of SMTP server to relay to  | `[smtp.sendgrid.net]:587`       |
| `smtp.username`   | Required | Username for SMTP server to relay to | `apikey`                        |
| `smtp.password`   | Required | Password for SMTP server to relay to | `pAsSwOrD`                      |
| `smtp.myhostname` | Optional | Hostname of this relay SMTP server   | `tx-smtp-relay.example.com      |
| `smtp.mynetworks` | Optional | Networks to permit relaying from     | `['127.0.0.0/8', '10.0.0.0/8']` |
