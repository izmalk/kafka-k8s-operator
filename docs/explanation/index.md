(explanation-index)=
# Explanation

The pages in this section aim to provide additional context and deeper understanding of foundational topics and concepts relevant to Charmed Apache Kafka K8s.

## Security

Secure deployments of Charmed Apache Kafka K8s can be achieved through using recommended configurations, including setting up encryption and authentication.
For more details, see [Security topic overview](explanation-security) and [Cryptography usage explanation](explanation-cryptography) pages.

## Clustering

Read an [explanation](explanation-cluster-configuration) of why we need Apache ZooKeeper
to coordinate and sync metadata between active brokers.

Check the [MirrorMaker explanation](explanation-mirrormaker2-0) page for more context in to how MirrorMaker replicates and migrates Apache Kafka clusters.

## Backups

Read through [Backups explanation](explanation-backups) for information on why snapshots and backing up Apache Kafka's log data is typically not necessary, and is not supported with Charmed Apache Kafka K8s.

## Other topics

To read more about our usage of Apache Kafka and other relevant trademarks, see the [Trademarks](explanation-trademarks) explanation page.

```{toctree}
:titlesonly:
:maxdepth: 2
:hidden:

Security<security.md>
Cryptography<cryptography.md>
Cluster configuration<cluster-configuration.md>
Backups<backups.md>
Trademarks<trademarks.md>
MirrorMaker2.0<mirrormaker2-0.md>
```
