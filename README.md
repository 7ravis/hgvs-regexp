#### work in progress
*There are many [HGVS nomenclature types and sub-types](http://varnomen.hgvs.org), so my plan is to chip away at the types that I have the most experience with first (cDNA, genomic DNA, and protein). However, if you have any pressing requests, please create an issue because I'm happy to prioritize whichever type would be the most helpful. If you would like to contribute, please do! Each prefix sub-type (e.g. genomic DNA insertions) is a convenient size for a single sitting.* 


## Overview
This project contains regular expressions for parsing HGVS ([Human Genome Variation Society](http://varnomen.hgvs.org)) sequence variant nomenclature. There are existing projects on Github that provide a high-level API for working with HGVS nomenclature; the purpose of this project is to create a lower-level tool with more focus and documentation on regular expressions that can be used under the hood in your own project.

## Format
There is a prefix file for each HGVS sequence type. For example, the regular expressions for coding DNA are in the `prefix-c.md` file. These markdown files are generally organized by the sub-types used on the [HGVS website](http://varnomen.hgvs.org) (substitution, deletion-insertion, etc.). 

**Example** (not necessarily up-to-date!) copied from the `prefix-c.md` file:

>### Substitution
>**Regular Expression:** `(?:[cC]\.)(\d+|\*\d+|-\d+)([+-]\d+)?([GCTAgcta])?>([GCTAgcta])`
>- *non-capturing:* `c.` (required, case-insensitive)
>- *Group 1:* base position (required). If there is a `*` or `-` preceding the number, it will also be captured.
>- *Group 2:* base position offset (optional). This number will be captured with a preceding `+` or `-`.
>- *Group 3:* reference allele (optional, case-insensitive)
>- *non-capturing:* `>` (required)
>- *Group 4:* alternate allele (required, case-insensitive)

>**Example:** `c.*93+1G>T`
>- *Group 1* = `*93`
>- *Group 2* = `+1`
>- *Group 3* = `G`
>- *Group 4* = `T`

## See Also
If you are developing in Python, there are some large projects already on Github, including [counsyl/hgvs](https://github.com/counsyl/hgvs), [biocommons/hgvs](https://github.com/biocommons/hgvs), and [mutalyzer/mutalyzer](https://github.com/mutalyzer/mutalyzer). If you are looking for a command-line or website interface, I would look into [zwdzwd/transvar](https://github.com/zwdzwd/transvar) and [TransVar web](http://bioinformatics.mdanderson.org/transvarweb/), respectively.
