# Definition

In [[Cloud Computing]], an **Availability Zone (AZ)** is a distinct, physically isolated location within a geographic [[Region]] that is designed to be resilient to local failures. If a [[Region]] is a city, then **Availability Zones** are individual, self-sufficient buildings within that city.

# Regions vs. Zones

1. **Geography:** A large area (e.g., North America).

2. **[[Region]]:** A specific geographic area (e.g., `us-east-1` in Northern Virginia).

3. **Availability Zone:** A subset of a Region (e.g., `us-east-1a`, `us-east-1b`).

>Each **Availability Zone** consists of one or more discrete **Data Centers**, each with redundant power, cooling, and networking.

# Key Characteristics of an AZ

## Physical Isolation

**Availability Zone** are separated by a meaningful physical distance to ensure that a localized disaster such as a fire, flood, or power grid failure affecting one AZ is unlikely to affect another.

## Low-Latency Connectivity

Despite being physically separate, all AZs within a single Region are connected via high-speed, private **fiber-optic networking**. This allows for **[[Synchronous Replication]]** of data, meaning you can copy data from AZ-1 to AZ-2 so fast that the user doesn't notice a delay.

## Independent Infrastructure

Each AZ has its own:

- Power connection (often from different utility providers).

- Backup generators and UPS (Uninterruptible Power Supply).

- Cooling equipment.

- Network gateways.

---

# High Availability Architecture

The primary purpose of AZs is to allow engineers to build **[[Fault Tolerant]]** systems.

---

## The "Multi-AZ" Strategy

>Instead of running your entire application in one AZ, you distribute it across two or more.

---

- **Scenario:** You run a website on two servers: one in `AZ-A` and one in `AZ-B`.

- **The Event:** A freak lightning strike knocks out the power for all of `AZ-A`.

- **The Result:** Because your application is "Multi-AZ," the traffic is automatically rerouted to the server in `AZ-B`. The end-user experiences zero downtime.


## Availability Zones vs. Edge Locations

- Availability Zones are for [[Compute]] and [[Storage]]. They are where your servers "live."

- **[[Edge Locations]]** are smaller sites used by [[CDN|CDNs]] (like [[CloudFront]]) to cache content closer to users to reduce latency. You cannot typically run a full [[database]] or a [[Virtual Machine|VM]] in an [[Edge Location]].

---

# Technical Trade-offs

## The Cost of "Chatty" Apps

While data transfer _into_ an AZ is usually free, cloud providers often charge a small fee for data moving **between** AZs. If your application is "chatty" (sending millions of small requests between a web server in AZ-1 and a database in AZ-2), you will see an increase in your [[Egress]] or Inter-AZ transfer bill.

## Consistency vs. Availability

In [[Distributed Systems]], replicating data across AZs introduces the **[[CAP Theorem]]** dilemma.

- **Synchronous Replication:** Safer (data is in both places before the "Save" is confirmed) but slower.
    
- **Asynchronous Replication:** Faster, but there is a tiny risk of data loss if the primary AZ fails before the copy is finished.
    

---

# AZ Name Map

Interestingly, `us-east-1a` for one user might not be the same physical building as `us-east-1a` for another user. 

Cloud providers randomize the mapping of AZ names to physical locations for each account to ensure even distribution of resources across their data centers. 

To sync locations between different accounts, engineers use **[[AZ IDs]]** (e.g., `use1-az1`).

# Related Notes

- [[High Availability vs Disaster Recovery]]

- [[Region]]

- [[Load Balancing]]

- [[SLA (Service Level Agreement)]]

- [[Fault Tolerance]]

# Tags

#cloud #infrastructure #highavailability #devops #architecture #reliability