<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Instant Failover with CloudFront Origin Groups

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-disaster-recovery-failover)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_n4p8r2t6)

---

## Introducing Today's Project!

This project demonstrates how to build automatic, near-instant failover between regions using Amazon CloudFront origin groups. The goal is to ensure users experience minimal disruption during a regional outage while traffic is transparently routed to a healthy backup region.

CloudFront is used because it operates at the edge and can detect origin failures quickly. When combined with multi-region App Runner services, it provides a simple and effective disaster recovery mechanism without requiring custom routing logic.

### Key services and concepts

This project uses Amazon CloudFront and AWS App Runner. The key concepts include origin groups, health checks, failover criteria, and edge-based traffic routing.

Together, these services allow traffic to be served from a primary region under normal conditions and automatically redirected to a secondary region when the primary becomes unavailable.

### Challenges and wins

The project took approximately ninety minutes to complete. The most challenging part was configuring CloudWatch alarms correctly so that failover events would generate accurate and timely alerts.

The most rewarding outcome was observing CloudFront automatically switch to the backup origin during a simulated outage and then return traffic to the primary origin once it was restored. This confirmed that both failover and failback were working as designed.

---

## Setting Up Multi-Region Prerequisites

This project requires App Runner services running in at least two AWS regions. Each service hosts the same application but operates independently within its region.

These services are required so CloudFront has multiple origins to route traffic to. Without regional duplication, true failover would not be possible.

---

## Creating a CloudFront Distribution

A CloudFront distribution is created using the App Runner service URLs as origins. One App Runner service is designated as the primary origin and the other as the backup.

Once created, CloudFront provides a single global URL that users access, abstracting away the underlying regional infrastructure.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_n4p8r2t6)

---

## Configuring Origin Groups for Failover

In this step, an origin group is configured to define how CloudFront should fail over between regions. The primary and secondary App Runner services are grouped together, and CloudFront is instructed to route traffic based on origin health.

Health checks and failover criteria ensure that CloudFront automatically switches to the backup origin if the primary becomes unhealthy, without requiring manual intervention.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_e7f3g9h1)

### Failover criteria configuration

The origin group is configured with the primary App Runner service as the first priority and the secondary service as the fallback. Health checks monitor the primary origin for errors and availability.

This setup ensures CloudFront reacts quickly to failures and maintains availability by routing traffic only to healthy origins.

### Testing the CloudFront URL

The CloudFront URL is tested under normal conditions and loads successfully. This confirms that traffic is routed to the primary origin as expected when both regions are healthy.

---

## Testing Automatic Failover

Automatic failover is tested by pausing the App Runner service in the primary region to simulate an outage. CloudFront detects the failure and reroutes traffic to the backup region.

This validates that the system can tolerate regional failures without user-visible downtime.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_x3y7z1a5)

### Simulating primary origin failure

When the primary App Runner service is paused, the response served through CloudFront changes to content coming from the backup region. This confirms that CloudFront has successfully failed over to the secondary origin.

---

## Verifying Automatic Failback

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_f6g1h5i9)

### Restoring the primary origin

Once the primary service resumes, CloudFront routes traffic back to it without manual changes. This confirms that automatic failback works correctly and that normal operation is restored as soon as the primary region is healthy.

---

## Building Production Alerting with CloudWatch

Alerting is added using CloudWatch and SNS to ensure failover events are visible to operators. While CloudFront handles failover automatically, alerts are needed to investigate root causes and assess impact.

This ensures operational awareness rather than silent recovery.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_sm2j7n4r)

### Configuring CloudWatch alarms

A CloudWatch alarm is created on the CloudFront 4xx error rate with a defined threshold and evaluation period. When the threshold is exceeded, an SNS notification is sent to notify on-call engineers.

This allows teams to respond quickly to failures even though traffic continues to flow.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-failover_sm4g5l6w)

### Verifying alerting works

The alarm is tested by pausing the primary App Runner service. After the evaluation period, an alert is received indicating a failover event.

This confirms that monitoring and alerting are correctly integrated with the failover system.

---

## Wrapping Up

This project demonstrates how to implement edge-based failover using CloudFront origin groups to protect multi-region applications from regional outages. It shows that high availability can be achieved without complex routing logic or custom failover systems.

A logical next step is learning how to apply similar disaster recovery patterns to stateful components such as databases through replication and controlled failover strategies.

---

---
