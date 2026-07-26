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

Sometime around 2013, as a solution to making it easier to ship software onto servers and reducing the friction between developer and operations, docker released a new approach built on top of existing Linux technologies. It provided a simple and intuitive `Dockerfile` to build the rootfs, registries to distribute it, namespaces and cgroups to isolate it, and an intuitive CLI that most programmers could easily use. The tool became extremely successful, and has become the de facto way in which workload are distributed these days. The containerisation ecosystem is not a proprietary framework these days, ever since Docker submitted the pieces for standardisation — donating its image format and its runtime internals (which became `runc`) to the [Open Container Initiative](https://opencontainers.org/) — which turned the product's internals into open specs:

- **Image format specification** — the format of the rootfs which consists of a manifest (or an index), a config, and a stack of content-addressed layer tarballs. The specification can be found [here](https://github.com/opencontainers/image-spec/blob/main/spec.md).
- **Runtime specification** — provides the interface on how to run an given rootfs based on the config manifest. The original implementation was *runc* which was donated by docker. The specification can be found [here](https://github.com/opencontainers/runtime-spec/blob/main/spec.md).
- **Distribution specification** — HTTP based REST API on how clients can interact with registries to push/pull images. The specification can be found [here](https://github.com/opencontainers/distribution-spec/blob/main/spec.md).

Following the standardisation, the ecosystem has matured significantly with many tools from different vendors. We will have a look at some of the prominent tools later.


## Userspace and *rootfs*

The construction of the rootfs is the packaging aspect of it that makes your application see the same background as where it was packaged. The idea is older than containers — and the history is roughly: hand-built chroots, then distro bootstrapping tools, then Docker turning the whole thing into a build artefact you can ship.
