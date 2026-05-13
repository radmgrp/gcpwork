# AWS to GCP Pricing Calculator Mapping (EZC_AWS)

**Region mapping:** AWS "Europe (Frankfurt)" -> GCP **europe-west3 (Frankfurt)**.

| # | AWS service | AWS configuration (from CSV) | GCP service (calculator entry) | GCP fields to fill |
|---|---|---|---|---|
| 1 | Amazon EKS | 1 cluster, 0 hybrid nodes | **Google Kubernetes Engine (GKE)** | **Standard cluster**, **1 cluster**, region **europe-west3**. This is the control plane fee only (node costs are in Compute Engine). |
| 2 | Amazon EC2 | 15x **c6i.2xlarge** Linux, on-demand, 100% | **Compute Engine** | **Custom N2** (8 vCPU, 16 GB RAM), **15 instances**, **730 hours/instance**, **On-demand**, region **europe-west3**. |
| 3 | Amazon EC2 | 5x **c6i.2xlarge** Linux, spot (58% discount) | **Compute Engine** | **Custom N2** (8 vCPU, 16 GB RAM), **5 instances**, **730 hours/instance**, **Spot VMs**, region **europe-west3**. |
| 4 | Amazon EBS (gp3) | 20 volumes, **50 GB each**, 3000 IOPS, 125 MB/s, snapshots 2x daily, 3 GB changed | **Hyperdisk Balanced** (or **pd-balanced** if hyperdisk not available) + **Snapshot storage** | **20 disks x 50 GB**, **IOPS 3000**, **Throughput 125 MB/s**, region **europe-west3**. Snapshots: **2/day**, **3 GB changed per snapshot**. |
| 5 | Amazon ECR | 50 GB stored, no data transfer | **Artifact Registry** | **Docker/OCI storage 50 GB**, region **europe-west3**. |
| 6 | Amazon RDS for MySQL | 1 node, **db.r6g.4xlarge**, Multi-AZ, 10 TB gp3, 20k IOPS, 500 MiB/s | **Cloud SQL for MySQL** | **Regional (HA)**, **Custom 16 vCPU / 128 GB**, **SSD 10 TB**, region **europe-west3**. If calculator supports it, set **provisioned IOPS 20,000** and **throughput 500 MiB/s**. |
| 7 | Amazon ElastiCache (Redis) | 6 nodes **cache.r6g.xlarge** | **Memorystore for Redis** | **Standard tier**, **6 instances**, **~26 GB per instance** (r6g.xlarge), region **europe-west3**. |
| 8 | S3 Standard | 2000 GB storage, 5,000,000 PUT/LIST, 5,000,000 GET | **Cloud Storage Standard** | **Storage 2,000 GB**, **Class A ops 5,000,000**, **Class B ops 5,000,000**, region **europe-west3**. |
| 9 | Data Transfer | 0 TB inbound/outbound | **Network Egress** | **0 GB** (no egress to price). |
| 10 | Amazon EFS | 200 GB | **Filestore** | **Filestore Basic (HDD)**, **200 GB**, **730 hours**, region **europe-west3**. |
| 11 | Application Load Balancer | 1 ALB | **Cloud Load Balancing** | **External HTTP(S) Load Balancer**, **1 load balancer**, **730 hours**, region **europe-west3**. (No data processed specified.) |
| 12 | Amazon Route 53 | 1 hosted zone, 10 records, 3 health checks | **Cloud DNS** + **Cloud Monitoring (Uptime checks)** | **1 managed zone**, **10 record sets**. Add **3 uptime checks** in Cloud Monitoring. |
| 13 | AWS WAF | 1 Web ACL, 5 rules | **Cloud Armor** | **1 security policy**, **5 rules**, region **europe-west3**. |
| 14 | Amazon CloudWatch | 50 metrics, 1 dashboard, 200 GB logs ingested, 200 GB logs scanned | **Cloud Monitoring** + **Cloud Logging** | **Metrics: 50**, **Dashboards: 1**, **Log ingestion: 200 GB**, **Log analytics/scanned: 200 GB**, region **europe-west3**. |
| 15 | Amazon Managed Service for Prometheus | 150,000 active series, 10 rules, 10 dashboard users, 2,400 queries/user/day | **Managed Service for Prometheus** | **Active time series 150,000**, **Rules 10**, **Query volume per user** as given, **Users 10**, **Collectors 1**. |
| 16 | Amazon Managed Grafana | 1 editor/admin, 5 viewers | **Managed Service for Grafana** | **1 editor/admin**, **5 viewers**. |
| 17 | AWS KMS | 5 CMKs, 2,000,000 symmetric requests | **Cloud KMS** | **5 keys**, **2,000,000 key operations**, region **europe-west3**. |
| 18 | AWS Secrets Manager | 5 secrets, 50 API calls | **Secret Manager** | **5 secrets**, **50 access operations**, region **europe-west3**. |
| 19 | Amazon GuardDuty | CloudTrail events 1000, VPC Flow Logs 200 GB, DNS logs 2 GB | **Security Command Center (Premium)** + **Cloud Logging** | **SCC Premium (1 project)**. Add **VPC Flow Logs ingestion 200 GB** and **DNS logs 2 GB** to Cloud Logging if not already included. |
| 20 | AWS Security Hub | 1 account, 30 checks, 3000 findings, 2 automation rules | **Security Command Center (Standard)** | **SCC Standard tier** (or equivalent), **1 project**, use findings/checks in SCC if calculator supports. |
| 21 | EFS Backup | 1000 GB backup data | **Filestore backup storage** | **Backup storage 1,000 GB**. |
| 22 | RDS Backup | 10,000 GB backup data | **Cloud SQL backup storage** | **Backup storage 10,000 GB**. |
| 23 | EBS Backup | 1,000 GB backup data | **Persistent Disk snapshot storage** | **Snapshot storage 1,000 GB**. |
| 24 | EBS (FOR_RDS_backup) | 1 volume, **20 TB**, 20k IOPS, 1250 MB/s, daily snapshot, 300 GB changed | **Hyperdisk Balanced** + **Snapshot storage** | **1 disk x 20 TB**, **IOPS 20,000**, **Throughput 1,250 MB/s**, region **europe-west3**. Snapshots: **daily**, **300 GB changed**. |
