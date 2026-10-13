# Changelog

This changelog follows [Common Changelog](https://common-changelog.org/).

## [0.3.0] - 2026-10-13

### Changed

- Map thinking levels from cool to hot, from Purple at `minimal` to Red at `max`
  ([`b785fd7`](https://github.com/sherif-fanous/pi-dracula/commit/b785fd7))
- Use Pink for the bash mode border so it no longer matches a thinking level
  ([`b785fd7`](https://github.com/sherif-fanous/pi-dracula/commit/b785fd7))

### Added

- Declare `appearance` so Pi pairs Dracula with dark terminals and Alucard with
  light terminals
  ([`9523812`](https://github.com/sherif-fanous/pi-dracula/commit/9523812))
- Define scrollbar and transcript search colors instead of relying on Pi's
  fallbacks
  ([`9523812`](https://github.com/sherif-fanous/pi-dracula/commit/9523812))

### Fixed

- Fix unreadable selected rows in Alucard by using its Selection color `#CFCFDE`
  ([`ab52e33`](https://github.com/sherif-fanous/pi-dracula/commit/ab52e33))
- Fix near-invisible dim text in Dracula by using Comment
  ([`f86aea5`](https://github.com/sherif-fanous/pi-dracula/commit/f86aea5))
- Use Purple for Markdown headings, as the Dracula spec specifies
  ([`2dbe28b`](https://github.com/sherif-fanous/pi-dracula/commit/2dbe28b))
- Point `$schema` to `https://pi.dev/schemas/theme.schema.json`, as the previous
  URL no longer resolves
  ([`5f89066`](https://github.com/sherif-fanous/pi-dracula/commit/5f89066))

## [0.2.0] - 2026-04-04

### Changed

- Reference theme vars in `export` sections instead of repeating hex values
  ([`13e5961`](https://github.com/sherif-fanous/pi-dracula/commit/13e5961))

## [0.1.0] - 2026-03-21

_Initial release._

[0.3.0]: https://github.com/sherif-fanous/pi-dracula/releases/tag/v0.3.0
[0.2.0]: https://github.com/sherif-fanous/pi-dracula/releases/tag/v0.2.0
[0.1.0]: https://github.com/sherif-fanous/pi-dracula/releases/tag/v0.1.0
