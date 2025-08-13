# Task 4: Setup and Use a Firewall on Kali Linux

## Objective
Configure and test basic firewall rules to allow or block traffic, and understand how a firewall filters network traffic.

## Tools
- UFW (Uncomplicated Firewall)
- Telnet (for testing blocked ports)
- SSH (for testing allowed ports)

---

## Steps Performed

### 1. Install and Enable UFW
```bash
sudo apt update && sudo apt install ufw -y
sudo ufw enable
````

**Outcome:**

* UFW firewall installed and activated.
* Default status: `active`, logging `low`, incoming connections denied, outgoing allowed.

---

### 2. Check Current Firewall Status

```bash
sudo ufw status verbose
```

**Outcome:** Shows firewall status and default policies:

```
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip
```

---

### 3. Block Port 23 (Telnet)

```bash
sudo ufw deny 23/tcp
```

**Outcome:**

* Incoming connections on port 23 are blocked.
* Firewall rule added: `23/tcp DENY IN`.

---

### 4. Test the Blocked Port

```bash
telnet 127.0.0.1 23
```

**Outcome:**

* Connection refused → confirms that port 23 is successfully blocked.
* Note: `127.0.0.1` is the local machine; no sensitive info is exposed.

---

### 5. Allow SSH (Port 22)

```bash
sudo ufw allow 22/tcp
```

**Outcome:**

* Incoming SSH connections allowed.
* Example SSH test (safe placeholder):

```bash
ssh <username>@127.0.0.1
```

* Connection succeeds locally; ensures remote access is possible if needed.

---

### 6. List Current Rules

```bash
sudo ufw status numbered
```

**Outcome:** Shows all active firewall rules with numbers:

```
[ 1] 22/tcp ALLOW IN
[ 2] 23/tcp DENY IN
```

---

### 7. Restore Firewall to Original State

**Option 1: Delete only test rule**

```bash
sudo ufw delete 2
sudo ufw status verbose
```

**Option 2: Reset completely to default**

```bash
sudo ufw reset
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw enable
sudo ufw status verbose
```

**Outcome:** Firewall restored to safe defaults. Only SSH allowed, no leftover rules from testing.

---

## How Firewall Filters Traffic

* UFW filters packets based on **source IP, destination IP, port, and protocol**.
* Inbound and outbound rules allow or block traffic.
* Rules are evaluated in order; the first matching rule is applied.
* Example: blocking Telnet prevented unauthorized inbound connections while allowing SSH.

---

## Conclusion

* Firewall successfully configured and tested.
* Incoming Telnet traffic blocked, SSH allowed.
* System restored to default safe state after testing.
* Demonstrated understanding of basic firewall management and network traffic filtering.

---


