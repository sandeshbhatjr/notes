+++
title = 'containers'
+++

# Containers

Containerisation is staple of modern software development. It provides a well established solution for packaging applications and running them in a well-bounded context. There are two aspects that make this possible (as probably popularised by docker):

- the construction of the rootfs over which the containerised process runs: This enables the packaging of an application with its own userspace tools for compatibility (for example, a bespoke libc version and openssl library and so on). This does NOT say anything about the kernel being used.
- the actual isolation of the resources available to the container process via cgroups and namespaces (and also seccomp filtering in older cases).

*Remark:* Container is not a lightweight VM, even though many people tend to think that. A VM boots its own kernel on virtual hardware; a container shares the host kernel and uses kernel features to isolate syscalls- in more ways than not- it is a chroot with isolation.
