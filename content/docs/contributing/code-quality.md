+++
title = "Code Quality"
description = "Ensuring good overall code quality."
date = 2021-05-01T18:20:00+00:00
updated = 2021-05-01T18:20:00+00:00
draft = false
weight = 420
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "Ensuring good overall code quality."
toc = true
top = false
+++
### Introduction ###

> I insist on code quality — Allen

This means:

1. No build failures on supported platforms (obviously including our [Continuous Integration ("CI") systems](https://travis-ci.org/libical/libical))
2. No compiler warnings allowed using "strict" (strict being a relative term) compiler warning options
3. No [splint](http://www.splint.org) issues using -weak checking
4. No serious [Coverity Scan](http://scan.coverity.com) issues
5. No serious [scan-build](http://clang-analyzer.llvm.org/scan-build.html) issues
6. No [Krazy](https://github.com/Krazy-collection/krazy) issues
7. No failed regression tests
8. Coding Style is very strictly enforced
9. (A goal) API documentation must be complete
10. Each source file must have a proper license and copyright header (Krazy tests for this)
11. Other stuff as I think of it

We want to be as portable as possible. We welcome ports to platforms we haven't encountered previously.

#### Compiler Warnings ####

See the top-level CMakeLists.txt for the options we use for each compiler.  Expect those options to get stricter over time.  Feel free to suggest compiler options that increase our code quality.

#### Continuous Integration ####

We use [Travis](https://travis-ci.org/libical/libical) to perform CI for libical on Linux and OSX.
For Windows we use the [Appveyor](https://ci.appveyor.com/project/winterz/libical) CI

#### Lint Checking ####

We use [Splint](https://www.splint.org) for lint checking our source code.  I'd love to have lint-checking as part of the CI reporting, but until then we run it by hand and fix the issues as part of the pre-release checklist.

#### Static Analysis ####

We're grateful to the good folks at [Coverity](https://coverity.com) for giving the FOSS world free access to their wonderful static analysis tool, Coverity Scan.  As a goal, I'd like to get the number of Coverity Scan issues down to zero.  It might take a few major releases to get there.

[scan-build](http://clang-analyzer.llvm.org/scan-build.html) is also good for static analysis checking but I've seen quite some false positives.  Good for a free tool, however.

By the way, [cppcheck](http://cppcheck.sourceforge.net) is another tool I like for static code analysis.  Occasionally we should run cppcheck as well.

#### Krazy Analysis ####

[Krazy](https://github.com/Krazy-collection/krazy) is another static analysis tool, but it checks mostly for non-C specific stuff, like it ensures Copyrights and License headers, looks for spelling mistakes and also coding style problems. We must be 100% "Krazy clean".

#### Coding Style ####

[Coding Style](@/docs/contributing/coding-style.md) is enforced.

#### API Documentation ####

We use [Doxygen](http://www.doxygen.org) to generate our [API Documentation](@/docs/developer/libical.md) and put the result on our [GitHub provided webspace](http://libical.github.io).  At this time our API Documentation is horrible and needs a lot of attention (see [libical#175](https://github.com/libical/libical/issues/175)), so one of our long term goals is to get the API Documentation into shape with full coverage.

