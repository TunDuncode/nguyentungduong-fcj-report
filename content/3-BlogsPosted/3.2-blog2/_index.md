---
title: "3.2 Preventing Server Downtime and Keeping Systems Reliable on AWS"
weight: 2
chapter: false
---

## Introduction

No server is guaranteed to operate without interruption, even when deployed on AWS. Sudden traffic spikes, CPU or memory overload, software errors, and infrastructure failures can all disrupt services. Therefore, we should plan for failure prevention and recovery from the very beginning of system design.

## Recommended Solutions on AWS

- **Amazon CloudWatch:** Monitor performance and configure alerts through Amazon SNS to detect early signs of problems.
- **Elastic Load Balancing (ELB):** Distribute incoming traffic across healthy servers instead of concentrating the load on a single server.
- **EC2 Auto Scaling:** Automatically adjust the number of servers based on demand and replace unhealthy instances according to health checks.
- **Multi-AZ:** Deploy servers across multiple Availability Zones within the same Region to reduce the impact of a failure in one zone.
- **AWS Backup:** Back up data regularly and test recovery procedures to minimize data loss.

![EC2 Auto Scaling architecture with an Application Load Balancer](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png)

*Figure 1. Load balancing and EC2 deployment across multiple Availability Zones. Source: [AWS Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/tutorial-ec2-auto-scaling-load-balancer.html).*

For example, when an EC2 instance fails, the load balancer can route new requests to the remaining healthy servers. Auto Scaling can replace the failed instance when appropriate health checks are configured. The remaining servers need enough capacity to serve users, and data must also have suitable redundancy.

![EC2 instance scale-out process](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/scale-out-diagram.png)

*Figure 2. Bringing a new EC2 instance into service during scale-out. Source: [AWS Documentation](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-lifecycle.html).*

## Choosing the Right Scaling Approach

| Criteria | Vertical Scaling | Horizontal Scaling |
| --- | --- | --- |
| Method | Increase CPU and RAM | Increase the number of servers |
| Implementation | Simpler | More complex |
| Fault tolerance | Limited with a single server | Better with redundancy |
| Scalability | Limited by server capacity | More flexible |

Small systems can start with a suitably sized server, monitoring, and backups. For critical services that require continuous availability, prioritize multiple servers, load balancing, and Multi-AZ deployment when the budget allows.

## Recommendations

In my opinion, rather than trying to build a server that never fails, we should build a system that can continue operating or recover quickly when failure occurs. Monitor proactively, test fault tolerance, and choose redundancy solutions that match actual needs. There is no need to deploy too many services from the start, but we should not wait until a system fails before preparing a response plan.

## Linkmyblog

https://www.facebook.com/groups/awsstudygroupfcj/permalink/2341484523283173/?rdid=ybztwhA7Gy935T5y#

## References

- [Amazon EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/)
- [AWS – Set up a scaled and load-balanced application](https://docs.aws.amazon.com/autoscaling/ec2/userguide/tutorial-ec2-auto-scaling-load-balancer.html)
- [AWS Well-Architected – Reliability Pillar](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html)

#AWS #AWSFCAJ #EC2 #AutoScaling #HighAvailability
