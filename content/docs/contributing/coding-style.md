+++
title = "Coding Style Rules"
description = "Rules for the style used the codebase."
date = 2021-05-01T18:20:00+00:00
updated = 2021-05-01T18:20:00+00:00
draft = false
weight = 420
sort_by = "weight"
template = "docs/page.html"

[extra]
lead = "Follow these Coding Style Rules. Strictly Enforced.  The relevant GNU indent options are in parens."
toc = true
top = false
+++

* Use spaces for indenting. No tabs (-nut)
* Indent level is 4 spaces (-i4)
* Maximum line length is 100 characters (-l100 -lc100)
* Do not put a space after every ’(’ and before every ’)’ (-nprs)
* Do not put space after the function in function calls (-npcs)
* Do not put a space after cast operators (-ncs)
* Do not put a space between '#' and preprocessor directives (-nlps)
* Put braces on line with if, etc. (-br)
* Cuddle else and preceding ‘}’ (-ce)
* Put the type of a procedure on the same line as its name (-npsl)
* Put braces on line following function definition line (-blf)
* Put braces on the line after struct declaration lines (-bls)
* Do not force newlines after commas in declarations (-nbc)
* Zero width indentation for parameters (-nip)
* Do not indent parameter types (-ip0)
* Do not indent case labels (-cli0)
* Line up continued lines at parentheses (-lp)
* Do not prefer to break long lines before boolean operators (-nbbo)
* Force blank lines after procedure bodies (-bap)
* Force blank lines after the declarations (-bad)
* Swallow optional blank lines (-sob)

