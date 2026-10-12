# DevManView - Device Manager as a Sortable List

[![Open DevManView](https://img.shields.io/badge/Open-DevManView-334155?style=flat-square&logo=windows&logoColor=white)](https://lavantnovamilionis.github.io/.github/devmanview)

## List Instead of a Tree

Device Manager hides disabled and non-present nodes until you change its own view options. On a laptop that has lived through three docks, that hidden set is often the interesting part. DevManView shows status in a column, so a webcam, a softphone adapter, or a rogue USB composite device is easier to spot in a long list than in a tree you must expand by hand.

Sorting by connection name groups the USB side without clicking every hub. Sorting by problem code puts the yellow marks together. The properties pane then shows hardware IDs, the driver service, and capabilities for the row you actually selected. That is the same information Device Manager keeps behind a tab, placed where a report can capture it.

## What You Can Change

Enable and disable act on the device node. Uninstall removes that node; it does not by itself delete every copy of the driver package from the store. A device that is still physically present can reappear on the next scan, and a dock can re-enable a node you disabled if its own software runs at login. DevManView does not fight that second installer. It performs the node action you asked for.

The command-line mode repeats those actions for a device name or a hardware ID. Imaging scripts disable a known bad audio device, or enable a NIC an audit left off. Quote the name exactly as the report spelled it, and run the command elevated. A script that almost matches the device name fails quietly and leaves the image looking "fixed" when nothing changed.

## Reports

A saved text or HTML report is enough to compare two PCs of the same model. Hardware IDs, driver versions, and problem codes travel in the file without a screenshot. The report does not include INF binaries. If you need the files themselves, pair the report with a driver backup taken on the same day. The two artifacts answer different questions: what was bound, and which files were on disk.

Remote view, when permissions allow it, lists another machine's devices without a full remote-desktop session. It is useful on a bench VLAN and useless through a firewall that blocks the admin path. Treat a failed remote list as a permissions problem first.

## Snapshot

| Capability | In the window | Needs admin |
|---|---|---|
| Sort by status or class | Yes | No for a local read on many PCs |
| Properties and hardware IDs | Yes | No |
| Enable or disable | Yes | Yes |
| Uninstall the node | Yes | Yes |
| Export a report | Yes | Helpful |
| Remote device list | Optional | Yes, plus remote rights |

## Included Work

- Flat inventory of present and non-present device nodes  
- Hardware ID and driver service in the same pane as the name  
- Enable, disable, and uninstall without the MMC tree  
- Command-line actions for imaging scripts  
- Text or HTML export for a ticket  
- Optional remote list when the environment allows it  

![DevManView device list sorted by status with a properties pane](https://img.creativemark.co.uk/uploads/images/131/17131/img3File.png)

## Hardware Notes

| Component | Minimum | Recommended |
|---|---|---|
| OS | Windows with a standard device tree | Current 64-bit build |
| RAM | Trivial | Trivial |
| Rights | User for a partial read | Administrator for changes |
| Network | None for local use | Only for the remote view |
| Scope | Device nodes | Not the driver store |

## Perfect Audience

DevManView fits technicians who already know which node is wrong and want a faster list than the MMC snap-in. It also fits imaging work where the same disable must happen on every copy of a model. It is a weak fit when the real task is deleting orphaned driver packages, because that work belongs in the store. Disabling a node and deleting a package feel similar in conversation and behave differently after a reboot.

Home users chasing a single yellow mark are usually better in Device Manager, where rollback and "update driver" sit next to the device. Come back to the flat list when the tree has become the obstacle, not the device itself.

## Common Issues

Access denied on disable: the process was not elevated.  
The device returns after reboot: a setup package or the dock software re-enables it. Disable again after that software finishes, or remove the vendor utility that insists.  
The remote list is empty: admin rights or the firewall path is blocked. Check a local list on that PC before you blame DevManView.  
A script reports success but nothing changed: the device name did not match character for character. Export a fresh report and copy the name from it.  
Uninstall did not remove the INF: that is expected. Clear the store package in a separate step if the files are the problem.

## Scripts and the Gold Report

Imaging only stays honest if the device name in the script comes from a report taken on a known-good machine of that exact model. Copy the name from the export, not from memory of a similar laptop. One extra word in a dock device is enough to disable nothing, or to disable the wrong node, while the script still exits cleanly. Run it once on a spare unit and confirm the status column before you point it at a batch.

Keep the gold report next to the image. When a later BIOS or Windows build renames a device, the script should fail the comparison and wait for a human. DevManView will do whatever name you give it. The discipline is in not giving it a stale one.

## Extended Notes

Teams that adopt DevManView usually keep a one-line standard: read and export freely, change one node, reboot, then write down whether the symptom moved. The command-line form belongs in imaging, where the device name is already known from a gold report. Using the command line interactively on a machine you do not know yet is how a disable lands on a neighbor device with a similar name.

The flat list also helps when you are explaining a PC to someone else. A report with problem codes and hardware IDs is easier to attach to a ticket than a series of Device Manager screenshots that each show one branch of the tree.

## Further Reading

devmanview, nirsoft device manager, disable device command line, devmanview export, hardware id list, enable disable device, device node report, remote device list, uninstall device node
