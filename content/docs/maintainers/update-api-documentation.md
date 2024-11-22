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
lead = "Update the public API documentation."
toc = true
top = false
+++

Make sure you have Doxygen installed; else this will fail.

Like so:

```bash
git checkout 3.0 #your stable branch
mkdir build-apidox; cd build-apidox
cmake -G Ninja .. && ninja docs
git checkout gh-pages
cd ..; rm -rf apidocs; cp -dpr build-apidox/apidocs/html apidocs
git add apidocs #make sure to include any newly generated files
git commit -m "update apidox" --no-verify . && git push
```

view it on [https://libical.github.io/docs/developer/libical/](@/docs/developer/libical.md) (might take a couple minutes to update)

add the generated `build-apidox/libical.tag` file to the github release
