# Changelog

*Italic text is guidance. Delete it as you fill each section in.*

*Keep the two lines below in the file. They tell a reader what conventions you follow, which is what makes the rest scannable.*

All notable changes to this project are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project uses [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

*What has landed on the main branch but is not released. Add entries here as changes merge, not at release time. Rename this heading to the version on release and open a fresh Unreleased section.*

*This section is what makes a changelog maintainable. Writing one from a month of commits is an archaeology exercise, and it shows.*

### Added

### Changed

### Fixed

---

## [1.4.0] - 2025-03-12

*Version, then date in `YYYY-MM-DD`. Use ISO 8601 and nothing else: `03/12/2025` means two different days depending on the reader.*

*Newest version at the top. People come here to find what changed recently.*

### Added

*New features and capabilities.*

- *Bulk export of transactions as CSV (`GET /transactions/export`).*

### Changed

*Changes to behaviour that already existed. Say what the old behaviour was, so a reader can tell whether it affects them.*

- *Rate limit on `/search` lowered from 100 to 60 requests per minute per key.*

### Deprecated

*Still works, will be removed. Give the replacement and the removal version or date, every time. A deprecation notice without both is a warning nobody can act on.*

- *`GET /v1/accounts` is deprecated in favour of `GET /v2/accounts` and will be removed in 2.0.0. See the [deprecation plan](deprecation-plan.md).*

### Removed

*Gone. Name what replaces it and when it was deprecated.*

- *`GET /v0/accounts`, deprecated since 1.1.0. Use `GET /v2/accounts`.*

### Fixed

*Bug fixes. Describe the symptom the user saw, not the code that changed. "Fixed null check in parser" tells a consumer nothing; they never saw the null check.*

- *Timestamps in exports were rendered in server local time instead of UTC.*

### Security

*Vulnerabilities fixed. Include the advisory or CVE. Keep this category even when it is usually empty: consumers scan for it first, and burying a security fix under Fixed costs you their trust once they notice.*

- *Session tokens were not invalidated on password change (CVE-2025-XXXXX).*

---

## [1.3.2] - 2025-02-28

### Fixed

- *...*

---

[Unreleased]: https://.../compare/v1.4.0...HEAD
[1.4.0]: https://.../compare/v1.3.2...v1.4.0
[1.3.2]: https://.../releases/tag/v1.3.2

*Link each version to its diff or release. One line each, at the bottom, so the entries above stay readable.*

---

## Notes on using this template

*Delete this section too.*

**Use exactly those six categories: Added, Changed, Deprecated, Removed, Fixed, Security.** Their value is that consumers learn them once and then scan for the two they care about. Inventing "Improvements" or "Miscellaneous" destroys that, and "Miscellaneous" is where entries go to be unread. Omit categories with no entries in a given release.

**Write for the person who has to decide whether to upgrade.** Every entry should answer "does this affect me". Refactors, dependency bumps with no visible effect, and test changes are not notable and should not appear.

**A generated commit log is not a changelog.** It contains merge commits, obscure titles and changes nobody outside the repo can act on. Keep a Changelog puts it plainly: changelogs are for humans, not machines. The curation is the entire product.

**Add the entry in the pull request that makes the change.** The author knows the user-visible effect; the person assembling the release does not. If entries are written at release time, they will be paraphrased commit messages.

**Semantic Versioning has a precondition most teams skip.** It requires a declared public API. Without one, "backward incompatible" has no agreed meaning and your major version is decoration. Say in your README what your public surface is, or say that you do not follow SemVer. Either is honest; claiming it without an API is not.

**Where this lives:** `CHANGELOG.md` at the repository root. Consumers expect it there, and so do the tools.
