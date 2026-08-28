---
myst:
  html_meta:
    description: "Complete documentation for Charmed Apache Kafka K8s - deploy, manage, and scale Apache Kafka clusters on Kubernetes."
---

(index)=

```{note}
This is a **Kubernetes** operator.
To deploy on IAAS/VM, see [Charmed Apache Kafka operator](https://documentation.ubuntu.com/charmed-kafka/4/).
```

# Charmed Apache Kafka K8s documentation

Charmed Apache Kafka K8s is an open-source software operator, packaged as a
[Juju charm](https://documentation.ubuntu.com/juju/latest/reference/charm/),
that simplifies the deployment, scaling, and management of Apache Kafka clusters
on Kubernetes.

[Apache Kafka](https://kafka.apache.org) is a free, open-source software project
by the Apache Software Foundation.

The charm helps ops teams and administrators automate Apache Kafka operations from
[Day 0 to Day 2](https://codilime.com/blog/day-0-day-1-day-2-the-software-lifecycle-in-the-cloud-age/)
with additional capabilities, such as: replication, TLS encryption, password rotation,
easy-to-use application integration, and monitoring.

## In this documentation

| | |
|--|--|
| **Tutorial** | [Introduction](tutorial-introduction) • [Step 1: Environment setup](tutorial-environment) |
| **Deployment** | [Deploy](how-to-deploy-index) • [Juju CLI](how-to-deploy-deploy-anywhere) • [Terraform](how-to-deploy-terraform) • [AKS](how-to-deploy-on-aks) • [EKS](how-to-deploy-on-eks) • [Requirements](reference-requirements) |
| **Operations** | [Connections management](how-to-client-connections) • [Unit management](how-to-manage-units) • [Monitoring](how-to-monitoring) • [File system paths](reference-file-system-paths) • [Broker listeners](reference-broker-listeners) • [Status reference](reference-statuses) • [External K8s connection](how-to-external-k8s-connection) |
| **Maintenance** | [Version upgrade](how-to-upgrade) • [Migration](how-to-cluster-migration) • [Replication](how-to-cluster-replication) • [MirrorMaker](explanation-mirrormaker2-0)  • [Backups](explanation-backups) |
| **Security** | [Overview](explanation-security) • [Enable encryption](how-to-tls-encryption) • [mTLS](how-to-create-mtls-client-credentials) • [Cryptography](explanation-cryptography) |
| **Extensions** | [Kafka Connect](how-to-use-kafka-connect) • [Schema registry](how-to-schemas-serialisation) • [Kafka UI](how-to-kafka-ui) |

## How the documentation is organised

This documentation uses the [Diátaxis documentation structure](https://diataxis.fr/):

- The [Tutorial](tutorial-introduction) walks you through deploying your first Charmed Apache Kafka K8s cluster from scratch, step by step.
- [How-to guides](how-to-index) help you solve specific operational tasks such as enabling TLS, connecting clients, or scaling brokers.
- [Reference](reference-index) lets you look up configuration options, status codes, file paths, and system requirements.
- [Explanation](explanation-index) helps you understand the design decisions behind security, replication, and integration architecture.

## Project and community

Charmed Apache Kafka K8s is a distribution of Apache Kafka. It’s an open-source project that welcomes community contributions, suggestions, fixes and constructive feedback.

- [Read our Code of Conduct](https://ubuntu.com/community/code-of-conduct)
- [Join the Discourse forum](https://discourse.charmhub.io/tag/kafka)
- [Contribute](https://github.com/canonical/kafka-k8s-operator/blob/main/CONTRIBUTING.md) and report [issues](https://github.com/canonical/kafka-k8s-operator/issues/new)
- Explore [Canonical's open-source data platform](https://canonical.com/data)
- [Contact us](reference-contact) for all further questions

## License and trademarks

[Apache Kafka](https://kafka.apache.org) is a free, open-source software project
by the Apache Software Foundation.
Apache®, Apache Kafka, Kafka®, and the Apache Kafka logo are either registered trademarks
or trademarks of the Apache Software Foundation in the United States and/or other countries.

The Charmed Apache Kafka K8s Operator is free software, distributed under the Apache Software License,
version 2.0. See [LICENSE](https://github.com/canonical/kafka-k8s-operator/blob/main/LICENSE) for more information.

```{toctree}
:titlesonly:
:maxdepth: 2
:hidden:

Home <self>
tutorial/index
how-to/index
reference/index
explanation/index
```
