# Infrastructure

## AWS Zones
Identify your zones here

From `rds-p/rds`:
"us-east-2a", "us-east-2b", "us-east-2c"

From `rds-s/rds.tf`:
"us-west-1b"

## Servers and Clusters

### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Web Server | serves up the Flask app | t3.micro | 1 instance | deployed |
| K8s cluster | mainly used for monitoring | t3.medium | 1 node | deployed |
| cluster db instance | stores cluster data | db.t2.small	 | 1 db instance | deployed |




### Descriptions
More detailed descriptions of each asset identified above.

The web server is the main application. We also serve up Prometheus metrics from this box. It is located in `us-east-2a`.

The Kubernetes cluster is used to do application monitoring. There is one node which is a t3.medium instance found in `us-east-2b`.

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

* Duplicate the web server in `us-west-1`, ensuring it has 3 instances instead of just one
* Duplicate the Kubernetes cluster in `us-west-1`, ensuring that there are at least two nodes instead of just one
* Duplicate the VPC in `us-west-1`, with IPs in multiple AZs within that region
* Duplicate the ALB in `us-west-1`.

## Steps:
Use a cloud load balancer. This way you can have multiple instances behind 1 IP in a region. During a failover scenario, I would fail over the single DNS entry at the DNS provider to point to the DR site. This is much more reliable than pointing to a single instance of a web server.

Make sure that the primary database is replicated and set up for automatic-failover to the secondary.