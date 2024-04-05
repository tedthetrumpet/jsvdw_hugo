---
title: "Raving the netbook again"
date: "2018-07-13"
---

Once again happily proving to myself how possible it is to work with open-source software on basic hardware. Just upgraded to [Ubuntu Studio](https://ubuntustudio.org/) 18.04 on a refurb 11" Dell Inspiron netbook, and built [SuperCollider](https://supercollider.github.io/) 3.9.3 from source. Here's an algorave-ish test track made using this setup:

[https://clyp.it/5d3lo4na](https://clyp.it/5d3lo4na)

Some new code idioms:

```
Plazy({Pseq((0..15).scramble,4)}).repeat(inf)
```

is easier to type than

```
Pn(Plazy({Pseq((0..15).scramble,4)}))
```

and similarly

```
Pseq([2,6,4,7],inf).stutter(32)
```

instead of

```
Pstutter(32, Pseq([2,6,4,7],inf))
```

also

```
Pseq((0..15).scramble,inf).clump(3)
```
