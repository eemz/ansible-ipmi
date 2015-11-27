# ansible-ipmi
An Ansible module to allow playbooks to communicate with remote devices using IPMI.

This module can issue commands to any device that implements IPMI, which includes most
data center switches and other hardware, including servers. Credentials and network
addresses are specified in a YAML (or JSON) file.

A typical credentials file would look like this:


```
---
  servers:
    - id: "rabbit01"
      ilo-ip: "10.5.12.55"
      ilo-user: "admin"
      ilo-password: "m355ag3q1"

    - id: "rabbit02"
      ilo-ip: "10.5.12.56"
      ilo-user: "admin"
      ilo-password: "m355ag3q2"

    - id: "switch1"
      ilo-ip: "10.65.19.1"
      ilo-user: "swadmin"
      ilo-password: "5y5adm1n"

    - id: "moonshot01"
      ilo-ip: "10.70.23.45"
      ilo-user: "mnadmin"
      ilo-password: "whatever"
      ilo-extras: "-B0 -b7 -T82 -t24"
```

The ilo-extras field is the only one that's not obvious... it exists to allow you
to specify extra addressing parameters that are required by some IPMI devices.
For example all HP Moonshot servers in a single enclosure share the same iLO IP
address and require extra addressing parameters to identify which specific one
you are talking to.
