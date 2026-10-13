# Evidence index

Images supplied with the lab folder. They document a working run; the values shown are point-in-time lab state.

| File | Shows |
| --- | --- |
| `evidence/receiver-port-setup.png` | Receiver configured to listen on TCP 9997 |
| `evidence/receiver-port-enabled.png` | Port 9997 saved and enabled |
| `evidence/index-created.png` | `armor-soc` index in Splunk |
| `evidence/forwarder-running-and-connected.png` | Forwarder running and active output to `192.168.56.1:9997` |
| `evidence/attacker-ssh-session.png` | SSH session from attacker to target |
| `evidence/target-audit-events.png` | Target audit log entries including failed and successful SSH events |
| `evidence/splunk-audit-events.png` | Events indexed as `linux:audit` with source and host metadata |
| `evidence/ssh-alert-search.png` | Search SPL and grouped results |
| `evidence/ssh-alert-enabled.png` | Alert listed as enabled |
| `evidence/event-count-by-type.png` | Audit-event counts by type |
| `evidence/event-count-by-account-address-result.png` | Counts by address, account, and result |
| `evidence/forwarded-logs-in-splunk-1.png`, `evidence/forwarded-logs-in-splunk-2.png` | Additional forwarded log views |
| `evidence/ssh-event-timeline.png` | Time-ordered SSH authentication events from `192.168.56.103` |
| `evidence/index-created-duplicate.png` | Additional copy of the index screenshot from nested source folder |

Images can show local usernames, hostnames, IP addresses, and desktop details. Review before public upload.

