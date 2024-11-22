+++
title = "Update Zoneinfo"
description = "How to use the vzic program to update the libical builtin zoneinfo database."
date = 2021-05-01T19:30:00+00:00
updated = 2021-05-01T19:30:00+00:00
draft = false
weight = 30
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "How to use the vzic program to update the libical builtin zoneinfo database."
toc = true
top = false
+++

### Preparations ###

1. clone vzic some place

```bash
git clone git@github.com:libical/vzic.git
```

2. Retrieve the most recent tzdata from IANA from [http://www.iana.org/time-zones](http://www.iana.org/time-zones)<br>
    Look for a gzip-compressed tar file (a "tarball") named tzdata2024b.tar.gz, for example.<br>
    Save the tarball into your Downloads folder.

3. Uncompress and untar the "tarball" file into the vzic folder:

```bash
cd vzic
mkdir tzdata2024b
cd tzdata2024b; tar xvfz ~/Downloads/tzdata202ba.tar.gz; cd ..
```

### Building vzic ###

```bash
cd vzic
make -B OLSON_DIR=tzdata2024b CREATE_SYMLINK=0 IGNORE_TOP_LEVEL_LINK=0
```

pass `PRODUCT_ID` and `TZID_PREFIX` as necessary (shouldn't be) or you could edit the top-level Makefile

### Running vzic ###

```bash
./vzic
```

The output is placed in the zoneinfo subdirectory by default, but you can use the `--output-dir` options to set another toplevel output directory.

You'll probably see some warning messages but not sure what to do about those.  The "Modifying RRULE to be compatible with Outlook" warnings are normal and can be ignored.

### Merging Changes to the Master Set of VTIMEZONES ###

1. Run `./vzic-merge.pl --master-zoneinfo-dir=/home/allen/projects/libical/libical/zoneinfo --new-zoneinfo-dir=/home/allen/projects/libical/vzic/zoneinfo`

2. _**You must add the new timezones in the zones.tab file by hand.**_

   cd to the libical git repo (eg. `/home/allen/projects/libical/libical/zoneinfo`)<br>
   run `git status`<br>
   look for new .ics files to be added (i.e untracked files in the zoneinfo directory)

3. diff the new from `vzic/zoneinfo/zones.tab` versus the updated zones.tab in the libical git repo

    copy lines from the new `vzic/zoneinfo/zones.tab` that are new (or differ) from the git repo version

### Testing ###

1. run `make test-vzic` and then run `./test-vzic`  (make sure libical is installed to /usr/local)
2. run the libical test-suite (`./scripts/buildtests.sh`)
