![Internship Schedule](./screenshot-1.png)


# F9 Internship Notes

*Day 1, Date 10-08-2026:*
Completed tasks:

- Company overview and walkthrough of the structured task plan from the Team Lead.
- Created a repo to log daily tasks and agendas.
- Covered IAM basics and created a demo IAM user.
- Covered Git basics and installed Git locally.
- Installed IDE (Antigravity), got familiar with core Git commands.

Terminologies covered: GitHub, IAM, AWS root account, Git.

*Day 2, Date 11-08-2026:*
Completed tasks:

- Launched an EC2 instance.
- Created demo directories to practice core Linux commands.
- Logged all commands run during the session into session.logs for the final presentation.

Terminologies covered: keypair, SSH, chmod, EC2, security groups, grep, find, sed, awk.

*Day 3, Date 12-08-2026:*
Completed tasks:

- Continued prior day's objective: user/group permissions and access control on the EC2 instance.
- Got familiar with GitHub workflows and commands.
- Created a demo repo to test commands, recording and pushing each step as it was performed.

Terminologies covered: whoami, groups, id, owner/group/others, chown, git clone, init, status, add, commit, log, switch, branch.
Summary: user → group → directory ownership → directory permission → file ownership → file permissions.

*Day 4, Date 13-08-2026:*
Completed tasks:

- Launched a second EC2 instance to reinforce the prior day's setup.
- Installed and enabled Apache2, hosting an HTTP server; modified index.html at the default document root (/var/www/html).
- Reused the existing security group and key pair, updating the SG to allow inbound HTTP (port 80).
- Confirmed both websites returned the expected output.
- Covered S3 fundamentals: buckets, objects, file uploads, lifecycle rules, permissions, and endpoints.
- Uploaded a demo static site (including index.html) to an S3 bucket and verified it via the bucket endpoint.
- Compared hosting a website on EC2 versus S3.
- Pushed the local demo site to GitHub, cloned it from the EC2 terminal, and moved the files into /var/www/html to serve them from the public address.

Terminologies covered: EC2, keypairs, security groups, S3 bucket, objects, permissions, systemctl, Apache2, ports.

*Day 5, Date 14-08-2025:*
Completed tasks:

- Covered VPC fundamentals.
- Created a custom VPC separate from the default VPC.
- Explored subnet configuration, CIDR blocks, and route tables — the networking concepts that control which traffic is allowed or restricted by IP range.

Terminologies covered: VPC, subnets, CIDR block, route table.

*Day 6, Date 15-08-2025:*
Completed tasks:

- Reused the existing Apache setup to validate the EC2 instance.
- Covered core shell concepts alongside it.
- Configured the security group to allow port 22 (SSH) access.
- Understood NACLs versus security groups — inbound/outbound rules and explicit deny behavior.
- Experimented with NACL and SG rules by enabling/disabling ports for a Python static site running on port 5000.

Terminologies covered: shell, security groups, NACL, inbound/outbound rules, deny rules.

*Day 7, Date 16-08-2025:*
Completed tasks:

- Set up a reverse proxy with Nginx sitting in front of Apache.
- Reconfigured Apache to listen on port 8080, localhost only, avoiding a port conflict with Nginx on port 80.
- Used Nginx to enable HTTPS with a self-signed certificate and key pair, opening port 443 for encrypted traffic.
- Verified the full chain — confirmed Apache was still the server ultimately serving traffic, routed through Nginx.

Terminologies covered: reverse proxy, Nginx, Apache, HTTPS, self-signed certificate, config files.

*Day 8, Date 17-08-2026:*
Completed tasks:

- Got familiar with CloudWatch metrics and logs — metrics (CPU utilization, network, etc.) for alerting and monitoring; logs for understanding *why* a metric moved, most useful for troubleshooting.
- Observed EC2 metrics before and after a manual CPU spike (via a small Python stress script).
- Created a custom CloudWatch Agent namespace; attached an IAM role with two CW Agent policies; configured the SSM Agent to support it.
- Built a dashboard and added widgets for the collected metrics.
- Ran a stress test and watched the dashboard respond in real time alongside repeated site refreshes.

Terminologies covered: CloudWatch metrics, CloudWatch Logs, CloudWatch Agent, IAM role, SSM Agent, dashboard.

*Day 9, Date 18-08-2026:*
Completed tasks:

- Implemented an alarm that automatically sends an email with a custom message once a threshold is breached, based on the CPUUtilization metric.
- Received the alert, had the instance auto-stop per the alarm's configured action, and diagnosed the cause.
- Deliberately broke the site by revoking index.html's read permissions via chmod — reproduced the "Access Denied" error.
- Removed the inbound HTTP rule and confirmed the resulting "connection timed out" behavior at the terminal.
- Practiced common troubleshooting technique combining terminal diagnostics with log monitoring.

Terminologies covered: CloudWatch alarm, SNS, chmod, access denied, connection timeout.

*Day 10, Date 19-08-2025:*
Completed tasks:

- Built a presentation consolidating progress logged so far.
- Reviewed and refreshed all concepts covered to date.

Terminologies covered: documentation, monthly review.

*Day 11, Date 20-08-2025:*
Completed tasks:

- Got familiar with ALB concepts — listeners, target groups, health checks, routing algorithm.
- Implemented an ALB in front of three Apache web servers, with the listener on port 80 forwarding to target groups, each hosting a different site.
- Understood the ALB workflow: Listener → Target Groups → EC2 instances.
- Accessed the site through the ALB's provided domain URL.
- Monitored ALB and target group metrics in CloudWatch; adjusted traffic flow around health checks.
- Refreshing the site alternated between the three sites — observed round-robin routing in action.
- Stopped Apache on one instance and watched it get flagged unhealthy.
- Enabled sticky sessions, keeping one instance bound to a user across multiple refreshes.

Terminologies covered: ALB, listener, target group, health check, round-robin, sticky sessions.

*Day 12, Date 21-08-2025:*
Completed tasks:

- Learned AMIs (golden images) as reusable blueprints capturing OS and software configuration.
- Built a Launch Template defining the instance recipe: AMI, instance type, key pair, security group.
- Created an Auto Scaling Group (desired=2, min=1, max=3) spread across 2 Availability Zones.
- Enabled ELB health checks so the ASG responds to app-level failures, not just instance crashes.
- Watched the ASG auto-launch 2 identical instances with zero manual intervention.
- Triggered self-healing: stopped Apache on one instance → ASG detected the unhealthy status, terminated it, and launched a replacement within 2–3 minutes.
- Tested a CPU-based scaling policy (50% threshold) — a stress test triggered an auto-launched 3rd instance, which scaled back down once load cleared.
- Key concept: an ASG assumes identical clones — replacement is automatic, not manual.

Terminologies covered: AMI, Launch Template, Auto Scaling Group, ELB health check, self-healing, scaling policy.git 

*Day 13, Date 22-08-2025:*
Completed tasks:

- Created a DB subnet group and dedicated RDS security group, allowing port 3306 only from the EC2 security group.
- Launched RDS MySQL instance (Single-AZ), connected via mysql client from EC2 terminal.
- Created a test database and table, inserted sample data for later validation.
- Understood Multi-AZ (sync replication, automatic failover, standby not queryable) vs Read Replica (async, read-only, manual promotion).

Terminologies covered: RDS, DB subnet group, Multi-AZ, Read Replica, endpoint.

*Day 14, Date 23-08-2025:*
Completed tasks:

- Took a manual snapshot as baseline, inserted new data afterward to test restore accuracy.
- Restored snapshot to a new instance, confirmed only pre-snapshot data was present. Learned restore always creates a new instance, never an in-place revert.
- Extended exploration: enabled real Multi-AZ and tested failover, measuring brief downtime with a continuous query loop.
- Created a Read Replica, observed replication lag, then promoted it to a standalone writable instance.
- Performed point-in-time recovery (PITR) to a custom timestamp and validated the exact data cutoff.
- Copied a snapshot cross-region for disaster recovery practice.

Terminologies covered: manual/automated snapshot, restore, PITR, replication lag, promotion, cross-region copy.

*Day 15, Date 24-08-2025:*
Completed tasks:

- Audited own IAM user via Access Advisor, found over-permissioned AdministratorAccess grant.
- Wrote a custom least-privilege JSON policy scoped to EC2, RDS, CloudWatch, S3.
- Created a test IAM user with the scoped policy, verified restricted actions failed with AccessDenied.

Terminologies covered: least privilege, IAM policy, Access Advisor, AccessDenied.

*Day 16, Date 25-08-2025:*
Completed tasks:

- Enabled MFA on root account and personal IAM user via authenticator app.
- Checked for and removed root access keys.
- Created a WAF Web ACL with AWS Managed Core Rule Set, associated it with the ALB.
- Tested mock SQL injection and XSS requests, confirmed WAF blocked them (403), verified in WAF request logs.

Terminologies covered: MFA, root access keys, WAF, Web ACL, Managed Rules.

*Day 17, Date 26-08-2025:*
Completed tasks:

- Explored Cost Explorer, grouped monthly spend by service.
- Checked for unattached EBS volumes and unused Elastic IPs, cleaned up what wasn't needed.
- Reviewed and trimmed old RDS snapshots.
- Set up a billing budget alert.

Terminologies covered: Cost Explorer, EBS volumes, Elastic IP, budget alert.

*Day 18, Date 27-08-2025:*
Completed tasks:

- Reviewed AWS's own Savings Plans recommendations based on usage history.
- Compared On-Demand vs Reserved Instance pricing without purchasing.
- Modeled real cost difference for a year of usage via AWS Pricing Calculator.

Terminologies covered: Savings Plans, Reserved Instances, On-Demand, Spot Instances.

*Day 19, Date 28-08-2025:*
Completed tasks:

- Installed Docker Engine on Ubuntu EC2 via official Docker repository.
- Verified with hello-world container, added user to docker group to run without sudo.
- Explored docker info and docker images.

Terminologies covered: Docker daemon, Docker CLI, Docker Hub, containers vs VMs.

*Day 20, Date 29-08-2025:*
Completed tasks:

- Wrote a Dockerfile for the static site project (FROM nginx:alpine, COPY, EXPOSE).
- Built the image, ran it as a container with port mapping (-p 8080:80).
- Inspected the running container via docker logs and docker exec.
- Learned volume mounts (-v) for live file editing without rebuilding.
- Practiced scp to pull website files from another EC2 instance/account.

Terminologies covered: Dockerfile, image, container, docker build/run, port mapping, volume mount, scp.

*Day 21, Date 30-08-2025:*
Completed tasks:

- Wrote a docker-compose.yml defining three services: web (nginx static site), db (MySQL), adminer (DB admin UI).
- Brought up the stack with docker compose up -d, verified all containers running.
- Connected to MySQL via Adminer using service name "db" as hostname, confirming built-in container networking.
- Tested named volume persistence across a down/up cycle.
- Compared self-hosted containerized MySQL against managed RDS from Week 2.

Terminologies covered: Docker Compose, services, named volumes, depends_on, container networking.

