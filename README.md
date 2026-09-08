# gradle-versions-mirror

Byte-identical hourly mirror of the endpoints under
<https://services.gradle.org/versions/>, for networks where that host is blocked.

| Upstream | Here |
|---|---|
| `/versions/all` | `versions/all.json` |
| `/versions/current` | `versions/current.json` |
| `/versions/milestone` | `versions/milestone.json` |
| `/versions/nightly` | `versions/nightly.json` |
| `/versions/release-candidate` | `versions/release-candidate.json` |
| `/versions/release-nightly` | `versions/release-nightly.json` |

```
https://raw.githubusercontent.com/tonyklawrence/gradle-versions-mirror/main/versions/current.json
https://cdn.jsdelivr.net/gh/tonyklawrence/gradle-versions-mirror@main/versions/current.json   # ~12h cache
```

Files are copied verbatim, not reconstructed — `checksum`, `commitId`, `broken`
and the rest are exactly as upstream publishes them. `downloadUrl` /
`checksumUrl` fields still point at `services.gradle.org`; if that host is
blocked too, the distribution zips are also on `downloads.gradle.org` and
`mirrors.cloud.tencent.com/gradle/`.

Refreshed hourly by `.github/workflows/mirror.yml`, which runs on GitHub's
infrastructure — nothing in your network talks to the blocked host. Each
response is parsed as JSON before it replaces the previous copy, so a proxy
error page or truncated download can't overwrite good data.
