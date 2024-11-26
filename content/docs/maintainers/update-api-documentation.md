+++
title = "Updating the API Documentation"
description = "Update the public API documentation."
date = 2021-05-01T19:30:00+00:00
updated = 2021-05-01T19:30:00+00:00
draft = false
weight = 30
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "Update the Website and public API documentation."
toc = true
top = false
+++

Clone the website:

```
git clone https://github.com/libical/io.github.libical.git
```

Open the file in `.github/workflows/main.yml` and update `LATEST_VERSION` to the
new version. Commit and push to the repository to trigger a website and
documentation update.
