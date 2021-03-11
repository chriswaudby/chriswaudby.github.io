---
title: 'csh cheat sheet'
date: 2021-03-11
permalink: /posts/2021/03/csh-cheat-sheet/
tags:
  - nmr
  - csh
---

Useful snippets of csh scripts.

Loops over arrays
======

```sh
set files = (2 3 4)
set phases = (252.0 250.0 254.0)

foreach i (`seq 3`)
echo $phases[$i]
mv $files[$i]/test.fid test-$i.fid
end
```
