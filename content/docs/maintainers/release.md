+++
title = "Tag and Release Instructions"
description = "How to create a new release."
date = 2021-05-01T19:30:00+00:00
updated = 2021-05-01T19:30:00+00:00
draft = false
weight = 20
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "How to create a new release."
toc = true
top = false
+++

### Preparations Checklist
* [[update zoneinfo|For-the-Maintainers:-Update-Zoneinfo]], if needed
* Builds ok on all supported platforms (no [Github Actions](https://github.com/libical/libical/actions) failures)
* Passes all regression tests
* Fix all compile warnings
* Fix all Krazy, splint, cppcheck, and clang-tidy warnings
* Do a [Coverity Scan](https://scan.coverity.com/projects/libical-libical)
* Any [Fuzzer problems](https://oss-fuzz.com/testcases?project=libical)?
* Fix all problems found by Clang-analyzer (scan-build)
* Compile with `-DADDRESS_SANITIZER` and run make test and fix any memory problems found
* Make sure ReleaseNotes.txt is up-to-date.  Double-check the release date.
* Make sure the `LIBICAL_LIB_*_VERSION` values in the top-level CMakeLists.txt is up-to-date

### Branch
If a major or minor release make sure to branch.

### Create the Tag
```bash
git tag -m "Libical X.Y.Z" vX.Y.Z
```

Do an [ABI Compliance Check](@/docs/maintainers/abi-compliance.md) (may not be needed for major releases, but useful nonetheless)

if all ok then go ahead and:
```bash
git push --tags
```

### Make a Release on Github
Go to [GitHub releases section](https://github.com/libical/libical/releases) and make an official release. Push the "Draft a new release" button.

Create a new tarball using git archive and add this the release (at the bottom of the page you will see a legend: "Attach images by dragging & dropping,  selecting them, or pasting from the clipboard.")

```bash
git archive --format=tar --prefix=libical-2.0.0/ v2.0.0 | gzip > libical-2.0.0.tar.gz
```

### New APIDOX

Follow the instructions for the [API Documentation](@/docs/maintainers/update-zoneinfo.md)

### New vcpkg port

The vcpkg libical port should follow a new version.

Create an issue on [vcpkg in GitHub](https://github.com/microsoft/vcpkg/issues/new?assignees=&labels=port+feature&template=request-an-update-to-an-existing-port.md&title=%5B%3Cport+name%3E%5D+update+to+%3Cversion%3E)

(also looks easy enough to make our own PR from a vcpkg fork, if we want to help out)

### New Conan package

TODO: document how to update the libical Conan package

Note that there is no conan package yet:
[we are working on it](https://github.com/conan-io/conan-center-index/issues/13268)

### Announcing
Open [Git Discussions](https://github.com/libical/libical/discussions) and make the announcement there.

Here's a sample announcement
```md
Announcing Libical 1.0.1
This is the first bugfix release for Libical 1.0.0

Highlights of this Release:
 * highlight1
 * highlight2
 * highlight3

The source code can be found on GitHub at:
https://github.com/libical/libical

Tarballs and zipballs for v1.0.1 are available from:
https://github.com/libical/libical/releases

Libical is an Open Source implementation of the iCalendar protocols
and protocol data units. The iCalendar specification describes how
calendar clients can communicate with calendar servers so users can
store their calendar data and arrange meetings with other users. 

Libical implements RFC2445, RFC2446 and some of RFC2447.

For more information about Libical, please visit
[https://libical.github.io/](https://libical.github.io/)
```

### Prepare for Next Release

#### If a patch-level release

Increase the `LIBICAL_LIB_PATCH_VERSION` value in the top-level CMakeLists.txt

Add an "UNRELEASED" section at the top of ReleaseNotes.txt
