Fileseq
=======

A Python library for parsing frame ranges and file sequences based on a similar library found in Katana.

Frame Range Shorthand
=====================

Support for:

* Standard: 1-10
* Comma Delimited: 1-10,10-20
* Chunked: 1-100x5
* Filled: 1-100y5
* Staggered: 1-100:3 (1-100x3, 1-100x2, 1-100)
* Negative frame numbers: -10-100
* Padding: #=4 padded, @=single pad

FrameSets
=========

A FrameSet wraps a sequence of frames in a list list container.

Iterate a FrameSet
------------------

```
fs = fileseq.FrameSet("1-5")
for f in fs:
  print f
```

Random Access
-------------

```
fs = fileseq.FrameSet("1-100:8")
print fs[-1] # Print last frame
```

FileSequence
============

```
fileseq.FileSequence("/foo/bar.1-10#.exr")
```

Finding Sequences on Disk
=========================

```
seqs = fileseq.findSequencesOnDisk("/show/shot/renders/bty_foo/v1")
```

Changes in versions >= 1.0.0
============================

From version 1.0.0, a FrameSet allows all the normal Set operations.  It is now an immutable and
hashable object in its own right, as well.  This means that the order and contents are immutable
values internally (a tuple and a frozenset, respectively), and that the FrameSet itself can be
used as a key in a dictionary.

This also means that the null FrameSet (FrameSet('')) is a valid object, and something you should
expect to receive back from any Set operations that would result in an empty return value.  This
brings the caveat that the FrameSet.start and FrameSet.end methods on a null FrameSet will raise an
IndexError if called.

To help avoid confusion, a FrameSet.is_null attribute has been added in 1.0.1, which you can check 
before calling those methods.
