# Netcat (Ncat) for SOC Analysts

## Overview

This repository demonstrates practical Netcat usage from a Security Operations Center perspective.

Topics include:

- Banner grabbing
- TCP troubleshooting
- Firewall validation
- Service verification
- Network debugging

---

## Tool Overview

Netcat (Ncat) is a networking utility used to read and write data across TCP and UDP connections.

---

## Features

- Practical SOC examples
- Bash automation
- Python wrappers
- Troubleshooting guides
- Cheatsheets

---

## Prerequisites

- Linux
- Nmap/Ncat
- Bash
- Python 3

Install

```bash
sudo apt install netcat-openbsd
```

or

```bash
sudo apt install ncat
```

---

## Usage

Check port

```bash
nc -vz 192.168.1.5 443
```

Banner grabbing

```bash
nc 192.168.1.5 80
```

---

## Repository Structure

```text
docs/
scripts/
examples/
screenshots/
```

---

## Security Warning

⚠ Use only in systems you own or are authorized to test.

Unauthorized network testing may violate laws or organizational policies.

---

## References

Official documentation

Nmap Project

RFCs

---

