# Introduction

Welcome to the Disaster Recovery Options in the Cloud! This document provides an overview of disaster recovery concepts and strategies, including Recovery Point Objective (RPO) and Recovery Time Objective (RTO), as well as different disaster recovery strategies available in the cloud.

## Resources
- **Blog I Read**: [Disaster Recovery Workloads on AWS](https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-options-in-the-cloud.html)
- **Video I See**: [Disaster Recovery Options](https://www.youtube.com/watch?v=_4hESnziWIE)

# Table of Contents

1. [Introduction](#introduction)
2. [Disaster Recovery Basics](#disaster-recovery-basics)
3. [Disaster Recovery Strategies](#disaster-recovery-strategies)
4. [Understanding RPO and RTO](#understanding-rpo-and-rto)

## Disaster Recovery Basics
- **Definition**: Planning for and responding to unexpected disasters with a backup strategy.
- **RPO (Recovery Point Objective)**: Determining acceptable data loss.
- **RTO (Recovery Time Objective)**: Time taken for full recovery after a disaster.

## Disaster Recovery Strategies
1. **Backup and Restore (Active/Passive)**
   - Involves taking data backups only.
   - Infrastructure backups are not taken.
   - Requires infrastructure creation and backup restoration in a disaster recovery situation.
   - Time-consuming process with lower costs.

2. **Pilot Light (Active/Passive)**
   - Infrastructure is created but kept in a stopped position while continuously taking data backups.
   - Database server is always on in smaller instances.
   - Higher cost compared to backup and restore.

3. **Warm Standby**
   - Both regions remain active but with lower capacity in the disaster recovery region.
   - Higher cost than the pilot light approach.

4. **Multi-Site Active/Active**
   - All components are in an active state in both regions.
   - Highest cost option.

## Understanding RPO and RTO

### RPO (Recovery Point Objective)
- **Definition**: RPO determines how much data loss is acceptable in case of a disaster.
- **Example**: If your RPO is 1 hour, it means you can afford to lose data created within the last hour. Beyond that, data loss may occur during recovery.

### RTO (Recovery Time Objective)
- **Definition**: RTO is the maximum acceptable time to restore systems and recover operations after a disaster.
- **Example**: If your RTO is 4 hours, it means you aim to have systems fully operational within 4 hours of a disaster occurring.
