# AWS-VPC-Architecture

## Project Summary 
This example demonstrates how to create a VPC that you can use for servers in a
production environment.
To improve resiliency, you deploy the servers in two Availability Zones, by using
an Auto Scaling group and an Application Load Balancer. For additional security,
you deploy the servers in private subnets. The servers receive requests through
the load balancer. The servers can connect to the internet by using a NAT
gateway. To improve resiliency, you deploy the NAT gateway in both Availability
Zones.

## Prerequisites:
Before you get started, make sure you have the following prerequisites set:

- An Aws account

## Project Scope
### 1.  Install and Configure
```
helm init
```

[Local Desktop - Install Azure CLI and Azure AKS CLI](https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/blob/master/01-Create-AKS-Cluster/README.md#step-06-local-desktop---install-azure-cli-and-azure-aks-cli)

[Running the sample](https://github.com/stacksimplify/azure-aks-kubernetes-masterclass/blob/master/14-Ingress-SSL-with-LetsEncrypt/README.md)
