# GCP Pricing Calculator — GCore Mapping 
**GCore total:** $5,273.22 USD

> **Region mapping (GCore → GCP nearest):**
> - Luxembourg → `europe-west6` (Zurich) or `europe-west3` (Frankfurt)
> - Warsaw → `europe-central2` (Warsaw) ✓ exact GCP region
> - Helsinki → `europe-north1` (Hamina, Finland)

---

## 1. Compute Engine — Large VM (Bare Metal Replacement)

> GCore had a committed bare metal server (2× AMD EPYC 9454, 512 GB RAM). The closest GCP cloud analog is a **custom N2 instance** with the same vCPU and memory spec.

| GCP Calculator Field | Value | Notes |
|---|---|---|
| **Machine type** | `n2-custom-96-524288` | 96 vCPU / 512 GB RAM — exact spec match |
| **Region** | `europe-west6` (Zurich) | GCore: Luxembourg-3 |
| **Hours/month** | **744** | Full April (31-day month) |
| **Boot disk** | `pd-ssd` | Size to match workload needs |
| **Commitment** | 1-year CUD recommended | GCore invoice was on a committed rate |

---

## 2. Compute Engine — VM Instances

> All instances are Linux unless noted. Use **Custom machine type** where no standard type matches exactly.

| GCP Calculator Entry | GCP Machine Type | vCPU | RAM (GB) | Region | Hours/month | OS |
|---|---|---|---|---|---|---|
| Instance 1 | `e2-custom-4-8192` | 4 | 8 | `europe-north1` (Helsinki) | **720** | Linux |
| Instance 2 | `e2-highcpu-8` | 8 | 8 | `europe-west6` (Luxembourg) | **1,194.55** | Linux |
| Instance 3 ×16 | `n2-custom-8-16384` | 8 | 16 | `europe-west6` (Luxembourg) | **720** each / **11,520** total | Linux |
| Instance 4 | `e2-custom-4-8192` | 4 | 8 | `europe-west6` (Luxembourg) | **720** | Linux |
| Instance 5 | `e2-custom-1-2048` | 1 | 2 | `europe-west6` (Luxembourg) | **1,166.52** | Linux |
| Instance 6 | `e2-highcpu-4` | 4 | 4 | `europe-west6` (Luxembourg) | **720** | Linux |
| Instance 7 | `e2-highcpu-2` | 2 | 2 | `europe-west6` (Luxembourg) | **485.22** | Linux |
| Instance 8 | `n2-highcpu-8` | 8 | 8 | `europe-north1` (Helsinki) | **720** | **Windows Server** |
| Instance 9 | `e2-custom-1-2048` | 1 | 2 | `europe-west6` (Luxembourg) | **1,440** | Linux |
| Instance 10 | `e2-custom-2-4096` | 2 | 4 | `europe-west6` (Luxembourg) | **1,695.57** | Linux |
| Instance 11 | `e2-custom-2-4096` | 2 | 4 | `europe-west6` (Luxembourg) | **720** | Linux |

**Instance 3:** Enter as **16 instances** of `n2-custom-8-16384`, 720 h/each in the calculator.

---

## 3. Compute Engine — Persistent Disk Storage

> GCP unit: **GB/month**. GCore unit GBM (GB-month) maps directly 1:1.

### High-IOPS SSD → `pd-ssd` (SSD Persistent Disk)

| Region | GCP Region | GB/month |
|---|---|---|
| Luxembourg-2 | `europe-west6` | **10.85** |
| Helsinki-1 | `europe-north1` | **134.22** |
| Luxembourg-3 | `europe-west6` | **1,632.14** |
| **Total High-IOPS SSD** | | **1,777.21 GB/mo** |

### Standard → `pd-standard` (Standard Persistent Disk)

| Region | GCP Region | GB/month |
|---|---|---|
| Warsaw-1 | `europe-central2` | **80.53** |
| Luxembourg-2 | `europe-west6` | **20.73** |
| **Total Standard** | | **101.26 GB/mo** |

### SSD Low Latency → `pd-balanced` (Balanced Persistent Disk)

| Region | GCP Region | GB/month |
|---|---|---|
| Luxembourg-2 | `europe-west6` | **32.21** |
| **Total Balanced** | | **32.21 GB/mo** |

---

## 4. Cloud Load Balancing

| GCP Calculator Field | Value | Notes |
|---|---|---|
| **Type** | Network Load Balancer (or HTTP(S) LB) | GCore: lb1-1-2 (1 vCPU / 2 GB RAM) |
| **Region** | `europe-west6` (Luxembourg) | GCore: Luxembourg-3 |
| **Hours/month** | **720** | |
| **Forwarding rules** | 1 | |

---

## 5. VPC Network — External IP Addresses

> GCP charges per hour for static external IPs in use and when reserved but unused.

### Public IP addresses (→ Static External IP)

| Location | GCP Region | Hours/month |
|---|---|---|
| Warsaw-1 | `europe-central2` | **720** |
| Luxembourg-3 | `europe-west6` | **4,539.57** |
| Luxembourg-2 | `europe-west6` | **485.23** |
| Helsinki-1 | `europe-north1` | **1,440** |
| **Total Public IP hours** | | **7,184.80 h** |

### Floating IP addresses (→ Static/Ephemeral External IP)

| Location | GCP Region | Hours/month |
|---|---|---|
| Luxembourg-2 | `europe-west6` | **1,886.52** |
| Luxembourg-3 | `europe-west6` | **3,390.55** |
| **Total Floating IP hours** | | **5,277.07 h** |

---

## 6. VPC Network — Egress / Data Transfer

| GCP Calculator Field | Value | Notes |
|---|---|---|
| **Traffic type** | Internet egress (Premium Tier) | GCore: "Egress traffic Bare Metal" |
| **Region** | `europe-west6` (Luxembourg) | GCore: Luxembourg-3 |
| **Data transferred** | **2,333.78 GB** | |

---

## 7. Cloud Logging

| GCP Calculator Field | Value | Notes |
|---|---|---|
| **Log ingestion** | **439.78 GB/month** | GCore: "Logging as a Service - Gb Luxembourg-2" |
| **Region** | `europe-west6` | |
| **Note** | First 50 GB/mo is free; billed volume = ~389.78 GB | GCP pricing: $0.50/GB after free tier |

---

## Quick-Reference Summary Table

| GCP Service | Resource | Quantity | Unit |
|---|---|---|---|
| Compute Engine VM | n2-custom-96-524288 (Luxembourg, BM replacement) | 744 | hours |
| Compute Engine VM | e2-custom-4-8192 (Helsinki) | 720 | hours |
| Compute Engine VM | e2-highcpu-8 (Luxembourg) | 1,194.55 | hours |
| Compute Engine VM ×16 | n2-custom-8-16384 (Luxembourg) | 720 each / 11,520 total | hours |
| Compute Engine VM | e2-custom-4-8192 (Luxembourg) | 720 | hours |
| Compute Engine VM | e2-custom-1-2048 (Luxembourg) | 1,166.52 | hours |
| Compute Engine VM | e2-highcpu-4 (Luxembourg) | 720 | hours |
| Compute Engine VM | e2-highcpu-2 (Luxembourg) | 485.22 | hours |
| Compute Engine VM | n2-highcpu-8 + Windows (Helsinki) | 720 | hours |
| Compute Engine VM | e2-custom-1-2048 (Luxembourg) | 1,440 | hours |
| Compute Engine VM | e2-custom-2-4096 (Luxembourg) | 1,695.57 | hours |
| Compute Engine VM | e2-custom-2-4096 (Luxembourg) | 720 | hours |
| Persistent Disk SSD (pd-ssd) | Luxembourg-2 | 10.85 | GB/mo |
| Persistent Disk SSD (pd-ssd) | Helsinki-1 | 134.22 | GB/mo |
| Persistent Disk SSD (pd-ssd) | Luxembourg-3 | 1,632.14 | GB/mo |
| Persistent Disk Standard (pd-standard) | Warsaw-1 | 80.53 | GB/mo |
| Persistent Disk Standard (pd-standard) | Luxembourg-2 | 20.73 | GB/mo |
| Persistent Disk Balanced (pd-balanced) | Luxembourg-2 | 32.21 | GB/mo |
| Cloud Load Balancing | 1 NLB, Luxembourg | 720 | hours |
| External IP (Static) | Warsaw-1 | 720 | hours |
| External IP (Static) | Luxembourg-3 | 4,539.57 | hours |
| External IP (Static) | Luxembourg-2 | 485.23 | hours |
| External IP (Static) | Helsinki-1 | 1,440 | hours |
| External IP (Floating/Ephemeral) | Luxembourg-2 | 1,886.52 | hours |
| External IP (Floating/Ephemeral) | Luxembourg-3 | 3,390.55 | hours |
| Internet Egress (Premium) | Luxembourg-3 | 2,333.78 | GB |
| Cloud Logging ingestion | Luxembourg-2 | 439.78 | GB/mo |
