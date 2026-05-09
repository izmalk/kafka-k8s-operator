---
myst:
  html_meta:
    description: "Enable TLS encryption for Charmed Apache Kafka K8s to secure data in transit using self-signed certificates and Juju relations."
---

<!-- test:spread
priority: -100
kill-timeout: 40m
-->

(tutorial-enable-encryption)=
# 5. Enable encryption

This is a part of the [Charmed Apache Kafka K8s Tutorial](index.md).

[TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) is used to encrypt data exchanged
between two applications; it secures data transmitted over the network.
Typically, enabling TLS within a highly available database, and between a highly available database
and client/server applications, requires domain-specific knowledge and a high level of expertise.
Fortunately, the domain-specific knowledge has been encoded into Charmed Apache Kafka K8s.
This means (re-)configuring TLS on Charmed Apache Kafka K8s is readily available and requires
minimal effort on your end.

Juju relations are particularly useful for enabling TLS.
For example, you can integrate Charmed Apache Kafka K8s to the
[Self-signed Certificates Charm](https://charmhub.io/self-signed-certificates)
using the [tls-certificates](https://charmhub.io/integrations/tls-certificates) interface.
The `tls-certificates` relation centralises TLS certificate management,
handling certificate provisioning, requests, and renewal.
This approach allows you to use different certificate providers,
including self-signed certificates or external services such as Let's Encrypt.

```{note}
In this tutorial, we will distribute
[self-signed certificates](https://en.wikipedia.org/wiki/Self-signed_certificate)
to all charms (Charmed Apache Kafka K8s and client applications) that are signed using
a root self-signed CA that is also trusted by all applications. 
This setup is only for testing and demonstrating purposes and self-signed certificates
are not recommended in a production cluster.
For more information about which charm may better suit your use-case, please see the
[Security with X.509 certificates](https://charmhub.io/topics/security-with-x-509-certificates) page.
```

## Configure TLS

Before enabling TLS on Charmed Apache Kafka K8s we must first deploy the `self-signed-certificates`
charm:

```shell
juju deploy self-signed-certificates --config ca-common-name="Tutorial CA"
```

<!-- test:await-idle --timeout 1200 --allow-blocked data-integrator -->

Wait for the charm to settle into an `active`/`idle` state, as shown by `juju status`.

To enable TLS on Charmed Apache Kafka K8s, integrate with `self-signed-certificates` charm:

```shell
juju integrate kafka-k8s:certificates self-signed-certificates
```

<!-- test:await-idle --timeout 1200 --allow-blocked data-integrator -->

<!-- test:assert
juju status --format json | jq -e '.applications["self-signed-certificates"]["application-status"].current == "active"'
-->

After the charms settle into `active`/`idle` states, the Apache Kafka listeners
should now have been swapped to the default encrypted port `9093`.

```{caution}
When no other application is integrated to Charmed Apache Kafka K8s,
the cluster is secured-by-default and external listeners (bound to port `9092`) are disabled,
thus preventing any external incoming connection. 
```

Let's integrate the `data-integrator` application to the Apache Kafka K8s cluster:

```shell
juju integrate data-integrator kafka-k8s
```

<!-- test:await-idle --timeout 1200 -->

## Enable TLS encrypted connection

Once TLS is configured on the cluster side, client applications should be configured as well
to connect to the correct port and trust the self-signed CA provided by
the `self-signed-certificates` charm.

Let's deploy our [Apache Kafka Test App](https://charmhub.io/kafka-test-app) again:

```shell
juju deploy kafka-test-app --channel edge
```

Then, enable encryption on the `kafka-test-app` by integrating with
the `self-signed-certificates` charm:

```shell
juju integrate kafka-test-app self-signed-certificates
```

<!-- test:await-idle --timeout 600 --allow-blocked kafka-test-app -->

We can then set up the `kafka-test-app` to produce messages with the usual configuration
(note that the process here is the same as with the unencrypted workflow):

```shell
juju config kafka-test-app topic_name=HOT-TOPIC role=producer num_messages=20
```

Finally, relate with the `kafka-k8s` cluster:

```shell
juju integrate kafka-k8s kafka-test-app
```

<!-- test:await-idle --timeout 600 -->

Wait for `active`/`idle` status in `juju status` and check that the messages are pushed into
the Charmed Apache Kafka K8s cluster by inspecting the logs:

```shell
juju exec --application kafka-test-app "tail /tmp/*.log"
```

Refer to the latest logs produced and also check that in the logs the connection
is indeed established with the encrypted port `9093`.

## Remove external TLS certificate

To remove the external TLS and return to the locally generated one,
remove relation with certificates provider:

```shell
juju remove-relation kafka-k8s self-signed-certificates
```

<!-- test:await-idle --timeout 600 --allow-blocked data-integrator -->

The Charmed Apache Kafka K8s application is not using TLS anymore for client connections.

## Clean up

Before proceeding further, let's remove the `kafka-test-app` application:

```shell
juju remove-relation kafka-test-app kafka-k8s
juju remove-relation kafka-test-app self-signed-certificates
juju remove-application kafka-test-app --destroy-storage --no-prompt
```

<!-- test:await-idle --timeout 600 --allow-blocked data-integrator -->
