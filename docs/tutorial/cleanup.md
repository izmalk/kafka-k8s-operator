---
myst:
  html_meta:
    description: "Clean up your Charmed Apache Kafka K8s deployment and remove Juju from your environment after completing the tutorial."
---

<!-- test:spread
priority: -400
kill-timeout: 30m
-->

(tutorial-cleanup)=
# 8. Cleanup your environment

This is a part of the [Charmed Apache Kafka K8s Tutorial](index.md).

(remove-kafka-and-juju)=
## Remove tutorial

```{caution}
Removing a Juju model may result in data loss for all applications in this model.
```

To remove Charmed Apache Kafka K8s and the `tutorial` model it is hosted on,
along with all other applications:

```shell
juju destroy-model tutorial --destroy-storage --force --no-prompt
```

<!-- test:wait --seconds 120 -->

This will remove all applications in the `tutorial` model (Charmed Apache Kafka K8s,
OpenSearch, PostgreSQL).
Your Juju controller and other models (if any) will remain intact for future use.

(remove-juju)=
## (Optional) Remove Juju and MicroK8s

If you don't need Juju anymore and want to free up additional resources on your machine,
you can remove the Juju controller and Juju itself.

```{caution}
When you remove Juju as shown below,
you lose access to any other applications you have hosted on Juju.
```

### Remove the Juju controller

Check the list of controllers:

<!-- test:skip -->
```shell
juju controllers
```

Remove the Juju controller created in this tutorial:

<!-- test:skip -->
```shell
juju destroy-controller overlord
```

### Remove Juju

To remove Juju altogether:

<!-- test:skip -->
```shell
sudo snap remove juju --purge
```

### Clean up MicroK8s

If you also want to remove MicroK8s and free up all resources:

<!-- test:skip -->
```shell
sudo snap remove microk8s --purge
```

```{warning}
Only remove MicroK8s if you're not using it for other purposes.
MicroK8s may be managing other workloads on your system.
```

## What's next?

In this tutorial, we've successfully deployed Apache Kafka, added/removed replicas, added/removed users to/from the cluster, and even enabled and disabled TLS.
You may now keep your Charmed Apache Kafka K8s deployment running or remove it entirely using the steps in [Remove Charmed Apache Kafka K8s and Juju](remove-kafka-and-juju).
If you're looking for what to do next you can:

- Try [Charmed Apache Kafka on VM](https://github.com/canonical/kafka-operator).
- Check out our other Charmed offerings from [Canonical's Data Platform team](https://canonical.com/data)
- Read about [High Availability Best Practices](https://canonical.com/blog/database-high-availability)
- [Report](https://github.com/canonical/kafka-k8s-operator/issues) any problems you encountered.
- [Give us your feedback](https://matrix.to/#/#charmhub-data-platform:ubuntu.com).
- [Contribute to the code base](https://github.com/canonical/kafka-k8s-operator)
