# Gentoo CI fixtures only

**Never add this directory as a Portage overlay on a real machine.** It includes synthetic ebuilds named `dev-lang/go` whose binaries only print sample outputs, *not* real Go toolchains.

`app-misc/version-manager-fixture` provides two independent slots; `app-misc/unslotted-fixture` exercises unslotted operation. The mock Go packages exist solely to verify the Go adapter in disposable Gentoo containers.

The installable overlay is at the repository root, and intentionally excludes these fixtures.
