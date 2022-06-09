# Kubernetes FinOps Label Schema

Just as [there are recommended labels for workloads running within a Kubernetes environment](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels/), there is a need for FinOps based labels to assist in allocating the cost for Kubernetes workloads.

## Labels

| Key                      | Description                 | Example                   | Type   | Maturity  |
| :----------------------- | :-------------------------- | :------------------------ | :----: | :-------: |
| `finops.org/application` | Application Name            | `acme fitness`            | string | 1 - Crawl |
| `finops.org/product`     | Product Name                | `acme fitness store`      | string | 2 - Walk  |
| `finops.org/service`     | Service                     | `store shopping cart`     | string | 3 - Run   |
| `finops.org/component`   | Component                   | `database`                | string | 3 - Run   |
| `finops.org/department`  | Department                  | `retail`                  | string | 2 - Walk  |
| `finops.org/cost-center` | Cost Center                 | `acme-1001`               | string | 1 - Crawl |
| `finops.org/team`        | Team                        | `road-runner`             | string | 1 - Crawl |
| `finops.org/environment` | Environment                 | `production`              | string | 2 - Walk  |
| `finops.org/tech-stack`  | Technology Stack by Purpose | `application`             | string | 3 - Run   |
| `finops.org/customer`    | Customer Name               | `acme`                    | string | 2 - Walk  |

## Examples

To illustrate different ways to use these labels the following examples have varying complexity.

### A Simple Stateless Service

Consider the case for a simple stateless service deployed using `Deployment` and `Service` objects. The following two snippets represent how FinOps labels could be used in their simplest form.

The `Deployment` is used to oversee the pods running the application itself.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    finops.org/application: acme fitness
    finops.org/cost-center: acme-1001
    finops.org/team: road-runner
    finops.org/environment: production
...
```

The `Service` is used to expose the application.
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    finops.org/application: acme fitness
    finops.org/cost-center: acme-1001
    finops.org/team: road-runner
    finops.org/service: store shopping cart
    finops.org/environment: production
...
```