# gradle-versions-mirror

Byte-identical hourly mirror of the endpoints under
<https://services.gradle.org/versions/>, for networks where that host is blocked.

| Upstream | Here |
|---|---|
| `/versions/all` | `versions/all` |
| `/versions/current` | `versions/current` |
| `/versions/milestone` | `versions/milestone` |
| `/versions/nightly` | `versions/nightly` |
| `/versions/release-candidate` | `versions/release-candidate` |
| `/versions/release-nightly` | `versions/release-nightly` |

```
https://raw.githubusercontent.com/tonyklawrence/gradle-versions-mirror/main/versions/current
https://cdn.jsdelivr.net/gh/tonyklawrence/gradle-versions-mirror@main/versions/current   # ~12h cache
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
