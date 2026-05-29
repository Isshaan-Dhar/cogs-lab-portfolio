cat > PIR-2026-04-08-MFA-Bulk-Failure.md <<'EOF'
# Post-Incident Report (PIR)
**Incident ID:** INC-2026-0408-001
**Date:** 2026-04-08
**Severity:** P2
**Status:** Resolved

## Incident Summary
This morning, 25 users in the finance department couldn't log into the InstaSafe client because they weren't receiving their SMS OTPs. We checked and found out that the SMS route was being blocked by the telecom carrier. The issue was fixed by switching the customer's OTP traffic over to a backup sender ID, which allowed everyone to log in normally again.

## Timeline
| Time (IST) | Event |
|------------|-------|
| 09:15 | Customer reported MFA failure for 25 users |
| 09:18 | Ticket #1001 created — priority P2 |
| 09:20 | First response sent to customer |
| 09:35 | Kaleyra checked — REJECTED codes confirmed |
| 10:30 | Escalated to L2 |
| 11:30 | L2 identified: Kaleyra sender ID flagged |
| 11:40 | Backup sender ID activated |
| 11:45 | Customer confirmed OTP working |

## Root Cause
The main Kaleyra SMS sender ID used for this customer got flagged and blocked by the telecom carrier TRAI. This happened because another company sharing the same route broke the DND (Do Not Disturb) rules. Because of this, the carrier blocked the whole sender ID. So, all 25 legitimate OTP requests were instantly rejected by the telecom provider.

## Impact Assessment
- Users affected: 25
- Duration: 2 hours 30 minutes
- Business impact: The finance team experienced a total lockout, meaning that they couldnt access or carry out their work and duties.

## Resolution Steps
1. [Step 1]
2. [Step 2]

## Prevention Actions
- [x] Action 1: Set up an automatic alert from the Kaleyra dashboard directly to L2 Team. Basically, if a sender ID gets a bunch of "REJECTED" errors (like more than 10 in 5 minutes), it will immediately notify the team so it is possible to catch it early instead of waiting for users to complain. — Owner: L2 Network Team — Due: 2026-04-15
- [x] Action 2: Provision a dedicated sender ID that is not shared with anyone else for premium enterprise customers. Since sharing the route with another company is what caused the carrier block in the first place, giving them their own unshared ID will completely prevent this from happening again. — Owner: Account Management — Due: 2026-05-01

## Open Items
- [x] Write a help guide: "How to fix Kaleyra 'REJECTED' SMS errors and switch sender IDs" — Assigned to: Ishaan Dhar — Due: 2026-04-12
