Power JBIG2 test files
======================

Thsi contains JBIG2 test files. See <https://nico.github.io/power-jbig2-tests/>
for an overview of the files.

These files used to be at
<http://spmg.ece.ubc.ca/jbig2/bitstreams/>. The index file is still on
[archive.org](https://web.archive.org/web/20030117183317/http://spmg.ece.ubc.ca/jbig2/bitstreams/),
but the all-important link to jb2streams.zip 404s there.

<http://jbig2dec.com/tests/index.html> used to mirror these files at some point
too, but at the moment it just redirects to a GitHub repo that doesn't have
the test files.

These test files also used to be available in the `jbig2/` subdirectory of
<http://git.ghostscript.com/tests.git>, but that repository too seems to be
inaccessible at the moment.

I'm uploading the files in case there's someone else out there writing a
JBIG2 decoder and thinks these bitstreams are useful.

The PDF in here is still available at the web site of one of the original
authors at <https://cs.uwaterloo.ca/~dtompkin/papers/t89-halftone.pdf>.

(See also [this post](https://web.archive.org/web/20030224122004/http://www.ece.ubc.ca/spmg/jbig2/software/main.html)
by the same author!)

There are very few JBIG2 test files that use halftoning, but t89-halftone.zip
in this repository contains several. I'm not aware of any open-source software
that can create JBIG2 files with pattern and halftone dictionaries.

(Some PDF files in the wild actually use this feature, so if you're writing
a JBIG2 decoder for a PDF renderer, you have to add support for it.)

A short ad
----------

<https://github.com/SerenityOS/serenity/tree/master/Tests/LibGfx/test-inputs/jbig2>
contains a bunch more JBIG2 test files.
