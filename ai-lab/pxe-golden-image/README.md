# 💿 PXE golden image

**Goal.** Plug in a new mini PC, boot it from the network, and have it come up as a ready Ubuntu 22.04 host with Docker and our base tooling. No manual setup.

**How it works.** PXE boot → Ubuntu autoinstall (`user-data`) → late-commands lay down Docker and a golden tarball → a one-shot first-boot service finishes the job → the technician runs one script to set the static IP and hostname.

**The bug worth telling: a kernel panic from one missing tar flag.**
Ubuntu 22.04 uses *merged /usr*: `/lib` is a symlink to `usr/lib`. Our golden tarball came from an older machine where `/lib` was a real directory. Extracting it replaced the symlink with a directory, and the next boot panicked.

```diff
- tar -xzf golden.tgz -C /target
+ tar -xzf golden.tgz -C /target --keep-directory-symlink
```

**Other lessons**
- **Order matters in late-commands.** The setup script must run *before* the tarball, or the chroot breaks.
- **The installer rewrites the user's password at the end**, so setting it during install doesn't stick. A one-shot first-boot service sets it, and cloud-init is disabled so it can't re-apply identity.

**Built with:** PXE / iPXE, Ubuntu autoinstall (subiquity + curtin), systemd, Bash. Debugged with Claude Code.

[← AI Lab](../README.md)
