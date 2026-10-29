# D Solution public content library

This repository contains only public, publishable social content and image
assets. It contains no Instagram tokens, credentials, or private publication
history.

The `dsolution-social-automation` repository fetches `posts.json` from this
repository on each scheduled run. Posts with `status: "draft"` are ignored.
Posts with `status: "ready"` are published automatically when their
`scheduled_at` time is due.

## Post format

```json
{
  "id": "post-001",
  "title": "A clear post title",
  "type": "image",
  "image_url": "https://raw.githubusercontent.com/DaniMahfoud/dsolution-content-public/main/assets/post-001.png",
  "caption": "Caption text\n\n#DSolution #Automation",
  "scheduled_at": "2026-11-01T12:00:00+04:00",
  "status": "ready"
}
```

Use unique IDs. A `ready` post needs an HTTPS `image_url`, a non-empty
`caption`, and a timezone-aware `scheduled_at`. Committing a `ready` entry is
the approval step for unattended publishing.

Generated Instagram assets must be 1080x1080 square PNG files with public URLs.
Official brand references and private review artifacts belong in the private
automation repository, not here. Do not put secrets or private customer
information in this repository.
