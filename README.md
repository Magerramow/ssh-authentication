# SSH Authentication Monitoring Lab

## Objective
Analyze SSH authentication logs and understand the difference between failed and successful login attempts in Linux.

---

## Environment
- Kali Linux VM
- OpenSSH service
- journalctl for log analysis

---

## User Setup

### Create a new user
```bash
sudo adduser test1
```

### Assign sudo privileges
```bash
sudo usermod -aG sudo test1
```

### Verify group membership
```bash
groups test1
```

---

## Authentication Simulation

### Generate failed login attempts
```bash
ssh test1@localhost
```
(Enter incorrect password multiple times.)

### Generate successful login
```bash
ssh test1@localhost
```
(Enter the correct password.)

---

## Log Analysis

### View SSH logs
```bash
sudo journalctl -u ssh -b
```

### Filter failed login attempts
```bash
sudo journalctl -u ssh -b | grep "Failed password"
```

### Filter successful login attempts
```bash
sudo journalctl -u ssh -b | grep "Accepted password"
```

### Count failed attempts
```bash
sudo journalctl -u ssh -b | grep "Failed password" | wc -l
```

### Count successful attempts
```bash
sudo journalctl -u ssh -b | grep "Accepted password" | wc -l
```

---

## Key Observations

- Invalid users generate:
  `Failed password for invalid user`

- Existing users generate:
  `Failed password for <username>`

- Successful authentication generates:
  `Accepted password`

- Authentication attempts can be counted and monitored to detect suspicious patterns.

---

## Outcome

This lab helped me understand:

- Linux user management  
- Sudo privilege configuration  
- SSH authentication behavior  
- Basic log filtering using grep  
- Event counting using wc  
- Fundamental concepts relevant to SOC Level 1 log monitoring  

This project represents a beginner-level hands-on practice focused on practical log analysis and authentication monitoring.
