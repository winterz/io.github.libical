+++
title = "ABI Compliance"
description = "Ensure ABI Compliance."
date = 2021-05-01T19:30:00+00:00
updated = 2021-05-01T19:30:00+00:00
draft = false
weight = 30
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "Ensure ABI Compliance."
toc = true
top = false
+++

Install [abi-compliance-checker](https://github.com/lvc/abi-compliance-checker) and [abi-dumper](https://github.com/lvc/abi-dumper)

my script to generate the ABI dumps is `gen-abi-data-libical-stable.sh`
make sure to have tagged the new release, call it `v3.0.5`

1. create the ABI dumps from the stable version,

```bash
gen-abi-data-libical-stable.sh v3.0.0
```

2. create the ABI dumps from the new release

```bash
gen-abi-data-libical-stable.sh v3.0.5
```

my script to compare the ABI dumps is `cmp-abi-data-libical.sh`

3. compare the ABI dumps
 
```bash
     cmp-abi-data-libical.sh v3.0.5
```

the standard output will show compatibility and you can look at the web pages reported there as well.

the comparison is stored in the compat_reports directory.

