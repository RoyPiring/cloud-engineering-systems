<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build Multi-Region Apps on AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-disaster-recovery-multiregion)

**Author:** Roy Piring Jr  
**Email:** rpiringhawaii@gmail.com

---

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-multiregion_s1d6r9t4)

---

## Introducing Today's Project!

This project shows how to deploy the same application in multiple AWS regions to improve availability and reduce the impact of regional outages. The app is deployed using AWS App Runner with GitHub-based deployments so updates are automatic and consistent.

The main goal is to demonstrate practical disaster recovery. By running the application in more than one region, a single regional failure does not take the service offline.

### Key services and concepts

AWS App Runner is used to run the application, GitHub is used to manage code and trigger deployments, and Express.js provides a simple web framework. The project focuses on AWS regions, automated deployments, and multi-region design as a reliability strategy.

The key idea is that regions are isolated by design. Each region must be deployed and managed independently for true resilience.

### Challenges and wins

The main challenge was understanding that App Runner and GitHub integrations are region-specific. Each region requires its own setup even when using the same code.

The win was confirming the application was running at the same time in two regions. This validated the multi-region design and showed how redundancy improves reliability.

---

## Creating a Node.js Express App

A simple Express application is created and pushed to GitHub. This app is intentionally minimal so the focus stays on deployment behavior rather than application logic.

The first deployment targets the us-east-1 region using AWS App Runner. Once deployed, the application is verified through the public HTTPS endpoint.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-multiregion_s1b8m3p9)

### Pushing code to GitHub

A simple Express application is created and pushed to GitHub. This app is intentionally minimal so the focus stays on deployment behavior rather than application logic.

The first deployment targets the us-east-1 region using AWS App Runner. Once deployed, the application is verified through the public HTTPS endpoint.

---

## Deploying to AWS App Runner (us-east-1)

The deployment in us-east-1 is validated by loading the App Runner URL and confirming the application responds correctly.

App Runner handles HTTPS, scaling, and infrastructure automatically, which keeps the focus on architecture instead of server management.

---

## Expanding to a Second Region (us-west-2)

The same application is deployed to a second region, us-west-2. Because AWS resources are regional, this requires creating a separate App Runner service.

Running the app in a second region ensures it remains available even if one region goes down.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-multiregion_s2c5n2r8)

### Creating a region-specific GitHub connection

Creating a region-specific GitHub connection

A separate GitHub connection is created for the second region. App Runner integrations do not share state across regions, so each region must be configured independently.

This separation is what makes real regional failover possible.

### Benefits of multi-region architecture

Both regional endpoints are tested and confirmed to work. Each region runs independently while serving the same application.

This improves availability, increases resilience, and allows traffic to be served closer to users.

---

## Adding Region-Aware Responses

The application is updated to display the AWS region it is running in. This makes it easy to see which region handled a request.

The change is pushed to GitHub and automatically deployed to both regions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-multiregion_s3c7n1p4)

### Using environment variables for region detection

The application reads the AWS_REGION environment variable provided by App Runner and includes it in the response.

This confirms that each deployment is correctly configured and makes testing and troubleshooting easier.

### Why region visibility matters

Being able to see the active region is important during outages or testing. It allows quick confirmation of which region is serving traffic.

This is especially useful when validating failover behavior.

---

## Measuring Real-World Latency

Latency is measured to compare response times between regions. Lower latency improves user experience and is one of the main reasons for multi-region deployment.

Measuring latency helps justify regional placement decisions.

![Image](http://learn.nextwork.org/refreshed_maroon_timid_jujube/uploads/ai-disaster-recovery-multiregion_sm4r8t2w)

### Building a latency test page

Response time is measured by recording timestamps at the start and end of each request. The difference shows how long the server took to respond.

This provides a simple and clear latency comparison.

### Latency results and insights

The region closer to the client shows lower latency. The farther region has higher response time due to distance and network routing.

This confirms the performance benefit of serving users from nearby regions.

---

## Project Reflection

This project demonstrates that multi-region deployments improve availability and performance without heavy operational complexity when using managed services.

The key takeaway is that regional redundancy can be implemented quickly and provides real reliability benefits. A future improvement would be managing deployments with infrastructure-as-code for greater consistency.

---

---
