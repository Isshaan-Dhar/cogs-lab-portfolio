# Post-Incident Report (PIR)
**Incident ID:** INC-2026-0601-001
**Date:** 2026-06-01
**Severity:** P1
**Status:** Resolved

## Incident Summary
The Nginx gateway service terminated unexpectedly, causing a total loss of connectivity for all users. The issue was detected via Uptime Kuma monitoring alerts and resolved by manually forcing a service restart of the Nginx daemon.

## Timeline
| Time (IST) | Event |
|---|---|
| 12:30 | Uptime Kuma Nginx monitor flipped to RED (Down) after 3 failed retries. |
| 12:31 | GitHub P1 ticket created; Incident response initiated. |
| 12:32 | Customer acknowledgement notice posted to ticket. |
| 12:32 | Investigation phase: Prometheus queried. Confirmed no CPU/Memory spike prior to crash. |
| 12:33 | Internal investigation note added to ticket. |
| 12:34 | 15-Minute update posted to customer. |
| 12:34 | Fix applied: `sudo systemctl start nginx` executed on the gateway VM. |
| 12:34 | Uptime Kuma Nginx monitor flipped to GREEN (Up); service recovery verified. |
| 12:36 | Resolution notice posted to ticket. |
| 12:37 | Ticket closed (Status: Resolved). |

## Root Cause
The `nginx` systemd service halted abruptly. Telemetry from Node Exporter confirmed no resource exhaustion (CPU/Memory) occurred prior to the halt, indicating an isolated daemon crash rather than a VM-level failure.

## Impact Assessment
* **Users affected:** All
* **Duration:** 22 minutes (12:40 to 13:02)
* **Business impact:** Total gateway downtime preventing any internal user access during the outage window.

## Resolution Steps
1. Verified service state via `systemctl status nginx` (confirmed inactive).
2. Checked Prometheus for resource exhaustion (confirmed normal).
3. Issued `sudo systemctl start nginx` to force recovery.
4. Verified recovery via Uptime Kuma HTTP 200 OK responses.

## Prevention Actions
- [ ] Implement automatic systemd restart policies (`Restart=always` in `nginx.service`) to automatically recover from isolated daemon crashes.
  * **Owner:** Support Engineering
  * **Due:** 2026-06-05

## Open Items
- [ ] Pull syslog/journalctl logs for the specific minute of the crash to identify the exact fault code or config error that triggered the termination.
