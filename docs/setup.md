# Rebuild the lab

Adapt addresses, packages, and paths to your environment. Screenshots document a host-only lab on `192.168.56.0/24`, with receiver `192.168.56.1` and observed SSH source `192.168.56.103`.

## 1. Prepare the VMs

- Splunk Enterprise host with the web UI reachable from your workstation.
- Kali target with OpenSSH and auditd, plus Splunk Universal Forwarder.
- Separate Kali attacker for authorized tests against the target.
- Place VMs on an isolated or otherwise controlled network.

## 2. Configure Splunk

Create an event index named `armor-soc`. Enable a receiving port at TCP `9997` under **Settings → Forwarding and receiving → Receive data**. The supplied receiver stanzas are examples; review them and restrict network access to the lab.

## 3. Configure Universal Forwarder

Install the official Universal Forwarder package for the target OS. Screenshots show it under `/opt/splunkforwarder` and running. Copy `configs/universal-forwarder/inputs.conf` and `outputs.conf` to a local forwarder app or `$SPLUNK_HOME/etc/system/local/`. Update the receiver address and source path. Ensure auditd is generating the file and that the forwarder can read it.

Captured CLI actions:

```bash
sudo /opt/splunkforwarder/bin/splunk add forward-server <SPLUNK_RECEIVER_IP>:9997
sudo /opt/splunkforwarder/bin/splunk list forward-server
sudo /opt/splunkforwarder/bin/splunk status
```

Do not put credentials into scripts or Git.

## 4. Generate controlled SSH events

From the attacker VM, connect to the target and generate a few failed attempts followed by a successful login. Do not test hosts outside your lab.

## 5. Validate ingestion

In Splunk Search, choose a suitable time range and run:

```spl
index=armor-soc sourcetype=linux:audit
```

Confirm the index, sourcetype, host, and source. If events are missing, check forwarder status, receiver port, connectivity, file permissions, auditd, and time range.

## 6. Search and alert

Run the files under `searches/`. The captured alert title is **ARMOR-SOC - SSH Failed Followed by Successful Login** and its status is enabled. When recreating it, set an appropriate time range, schedule, trigger condition, and action. The captured query counts at least two failures and one success per remote IP, but does not ensure the success followed the failures. See [the detection notes](architecture.md#detection-flow).
