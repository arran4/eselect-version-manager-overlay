# eselect-version-manager-overlay

Portage overlay for [eselect-version-manager](https://github.com/arran4/eselect-version-manager). Portage installs packages; the version manager chooses among installed versions.

**Status:** initial migration of the Draft PR #1 test overlay. The `app-eselect/eselect-version-manager-0.1.0` ebuild refers to an as-yet-unpublished `v0.1.0` source archive. Integration CI generates a matching archive from source. Do not treat this ebuild as a tested release package until the tag, Manifest and installation have been verified.

## Layout

- `app-eselect/eselect-version-manager/`: initial package ebuild and metadata.
- `metadata/` and `profiles/`: normal Gentoo Portage overlay metadata.
- `tests/portage-overlay/`: separate **CI-only fixture repository**. It contains synthetic slotted and unslotted tools, plus *mock* `dev-lang/go` packages. **Never add this fixture repository to a real Gentoo system.** Fake Go ebuilds are deliberately excluded from the installable overlay root.

## Testing

The [version manager's Gentoo E2E suite](https://github.com/arran4/eselect-version-manager/blob/feat/eselect-version-manager/scripts/test_in_gentoo.sh) registers the production overlay and the fixture overlay separately inside a disposable Gentoo container, prepares a source archive for the draft ebuild, and runs real `emerge` transactions.

Port the full fixture set here; keep source-repository tests synced with the fixture paths and revisions. Do not duplicate the test fixture packages in the application repository.

## Toolchains

The test Go ebuilds output canned version strings; **they are not Go backports**. No production-ready slotted Node.js or Go ebuild was available in the source overlay, so neither is asserted by this migration. For tools already slotted in Gentoo (such as Python and Maven), prefer the real Gentoo package/selector integration instead of copying their ebuilds. Any future backport must be verified for provenance, noncolliding installation paths, dependencies, licensing, Portage manifests and actual emerge/unmerge behaviour.

## Generated assets

Portage `Manifest` files are **generated** by `ebuild ... manifest` or `pkgdev manifest`; do not hand-edit them. CI also generates the draft package's source tarball and temporary fixture revision ebuild. None of these test artifacts constitutes a published upstream release.
