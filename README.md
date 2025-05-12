# linux-cis-hardening-ansible
This repository documents my step-by-step journey of hardening a Rocky Linux 9 server(1:1 to RHEL9) based on CIS Benchmarks.

## 🔒 Goals

- Understand and implement CIS security controls manually
- Use OpenSCAP to audit the system
- Automate security hardening using Ansible (work in progress)
- Learn practical Linux security operations

## 📁 Structure

- `manual-hardening.md` – Manual steps and config changes
- `ansible/` – Automation scripts (in progress)
- `scans/` – OpenSCAP scan reports (before & after)
- `docs/cis-checklist.md` – My personal notes from reading the CIS Benchmark

## 🛠 Technologies

- Rocky Linux 9
- OpenSCAP & SCAP Workbench
- Bash / Manual configuration
- Ansible (later stage)

## ✅ Status

- [x] OpenSCAP audit completed
- [ ] Top 10 CIS items manually hardened
- [ ] Ansible automation for SSH + Auditd
- [ ] Full automation with Ansible roles

## 📚 Learnings

This lab will help me understand:
- Core Linux security concepts 
- The structure and purpose of CIS Benchmarks
- Why automation is useful only when you first understand the system
