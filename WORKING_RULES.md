# Working Rules

Presentation Date and Deadline: **Dec 11, 2026** (target submission **Nov 27**).

## Ownership

| Person | Parts |
|---|---|
| Jeffar | 1 (setup), 2 (Sysmon), 4 (Wazuh integration), 5 (FIM) |
| Matthew| 3 (Suricata), 6 (attack tests), 7 (Active Response) |
| Both | Reflection, References |

## SSD schedule

| Dates | Holder | Work |
|---|---|---|
| Nov 4-6 | Jeffar | Parts 1-2 |
| Nov 9-13 | Matthew | Part 3 |
| Nov 16-20 | Jeffar | Parts 4-5 |
| Nov 23-27 | Matthew | Parts 6-7 |

## SSD rules

1. Only the current holder touches the VMs.
2. Shut VMs down fully. Never suspend.
3. Safely eject the SSD every time, and never unplug it while a VM is running.
4. No deleting, moving or renaming VM folders.
5. Take a snapshot at the end of every turn, named `Part#`.

## Lab settings (same on every machine)

- Hypervisor: VMware Workstation Pro
- VMnet8 (NAT): subnet `192.168.121.0/24`, mask `255.255.255.0`, gateway `192.168.121.2`.
- IPs: WazuhManager `.10`, Windows11 `.11`, UbuntuDesktop `.24`, KaliLinux `.25`
- Never use bridged mode or port forwarding for these VMs.

## Evidence

- Every screenshot has a caption saying what it shows, and the file name says which part it is for.
- Take your own screenshots for your own parts.
- Write up your sections right after your lab turn.

## Credentials

Do **not** commit passwords, the Wazuh admin password or API keys to the repo. Share them privately.