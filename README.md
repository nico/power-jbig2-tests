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

Mistakes in these files
-----------------------

* `t89-halftone/*-stripe.jb2` have one PatternDictionary and then one
  ImmediateHalftoneRegion per stripe, but each ImmediateHalftoneRegion
  (incorrectly?) sets the retention flag for the PatternDictionary to 0.
  I think only the last ImmediateHalftoneRegion should do that.

* `042_*.jb2`, `amb_*.jb2` incorrectly (cf 7.3.2) associate EndOfFile
  with a page

* `042_11.jb2` has refinement huffman table bits set but the SBREFINE bit
  is not set. This isn't valid per 7.4.3.1.2. (The file still decodes fine.)

* `042_13.jb2` has an OOB in a decoder that isn't mean to produce OOBs.
  No current PDF viewer can decode this file embedded in a PDF.
  The OOB happens when reading the first refinement x offset of the
  second symbol dictionary segment in the file (which is the first with
  SDREFAGG set). Before the refinement x offset, REFAGGNINST gets decoded
  (correctly?) as `1`, and the reference symbol id as 286.

* `042_14.jb2` also fails to decode in all current PDF viewers. Not 100%
  sure why, but it uses a huffman symbol dictionary with SDREFAGG=1. Maybe
  the file is right and viewers just don't implement support for this.
  But it's the huffman version of the preceding test, so more likely
  the encoder wrote bad output for SDREFAGG=1 symbol dictionary segments.

* `042_22.jb2` does not set SDREFAGG but it does set SDREFTEMPLATE. This is
  invalid per 7.4.2.1.1 Symbol dictionary flags, Bit 12. (Other than that,
  the file decodes fine.)

* ("Columbia" is misspelled as "Columba" in the 'Source' string in the extension
  segment of most files -- but some in t89-halftone spell it correctly.)
