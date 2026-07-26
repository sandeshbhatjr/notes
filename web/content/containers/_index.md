+++
title = 'containers'
+++

# Containers

Containerisation is staple of modern software development. It provides a well established solution for packaging applications and running them in a well-bounded context. There are two aspects that make this possible:

- the construction of the rootfs over which the containerised process runs: This enables the packaging of an application with its own userspace tools for compatibility (for example, a bespoke libc version and openssl library and so on). This does NOT say anything about the kernel being used.
- the actual isolation of the resources available to the container process via namespaces and cgroups (and also seccomp filtering in older cases).

{{< hint info >}}
A very big misconception that I regularly encounter is the belief that containers are a form of lightweight VMs. Container is NOT a lightweight VM, even on a conceptual level. A VM boots its own kernel on virtual hardware; a container shares the host kernel and uses kernel features to isolate syscalls- in more ways than not- it is a chroot with isolation features provided by the kernel.
{{< /hint >}}
