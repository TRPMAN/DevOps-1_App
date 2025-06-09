# App Helm Chart

A production-grade Helm chart for deploying the application stack.

## Components

This Helm chart deploys the following components:

- Application frontend
- MySQL database with persistent storage
- Memcached for caching
- RabbitMQ for messaging
- Ingress for external access

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure
- Ingress controller (like NGINX Ingress Controller)

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
helm install my-release .
```

## Configuration

The following table lists the configurable parameters of the App chart and their default values.

| Parameter                        | Description                                      | Default                    |
|----------------------------------|--------------------------------------------------|----------------------------|
| `global.domain`                  | Domain name for the application                  | `app.agsfva.online`        |
| `app.replicaCount`               | Number of application replicas                   | `1`                        |
| `app.image.repository`           | Application image repository                     | `trpman/dockerpj1_app`     |
| `app.image.tag`                  | Application image tag                            | `latest`                   |
| `db.replicaCount`                | Number of database replicas                      | `1`                        |
| `db.image.repository`            | Database image repository                        | `trpman/dockerpj1_db`      |
| `db.persistence.enabled`         | Enable persistence for database                  | `true`                     |
| `db.persistence.size`            | Size of persistent volume claim                  | `3Gi`                      |
| `memcache.replicaCount`          | Number of memcached replicas                     | `1`                        |
| `rabbitmq.replicaCount`          | Number of RabbitMQ replicas                      | `1`                        |
| `ingress.enabled`                | Enable ingress                                   | `true`                     |
| `ingress.className`              | Ingress class name                               | `nginx`                    |

## Production Considerations

For production deployments, consider the following:

1. **Resource Limits**: Adjust CPU and memory limits based on your workload.
2. **Replicas**: Increase the number of replicas for high availability.
3. **Storage**: Use a production-grade storage class for database persistence.
4. **Secrets**: Use a secret management solution instead of storing secrets in values.yaml.
5. **Image Tags**: Use specific image tags instead of `latest`.
6. **Health Checks**: Add liveness and readiness probes for all components.
7. **Monitoring**: Integrate with monitoring solutions like Prometheus and Grafana.

## Upgrading the Chart

To upgrade the chart:

```bash
helm upgrade my-release .
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```