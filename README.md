## Work in Progress
There are many [HGVS nomenclature types and sub-types](http://varnomen.hgvs.org), so my plan is to chip away at the types that I have the most experience with first (cDNA, genomic DNA, and protein). However, if you have any pressing requests, please create an issue because I'm happy to prioritize whichever type would be the most helpful. If you would like to contribute, please do! Each prefix sub-type (e.g. genomic DNA insertions) is a convenient size for a single sitting.

## Overview
This project contains regular expressions for parsing HGVS ([Human Genome Variation Society](http://varnomen.hgvs.org)) sequence variant nomenclature. There are existing projects on Github that provide a high-level API for working with HGVS nomenclature; the purpose of this project is to create a lower-level tool with more focus and documentation on regular expressions that can be used under the hood in your own project.

## Format
There is a prefix file for each HGVS sequence type. For example, the regular expressions for coding DNA are in the [prefix-c.md](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-c.md) file. These markdown files are generally organized by the sub-types used on the [HGVS website](http://varnomen.hgvs.org) (substitution, deletion-insertion, etc.). 

**Example** (not necessarily up-to-date!) copied from the [prefix-c.md](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-c.md) file:

>### Substitution
>**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?([GCTAgcta])?>([GCTAgcta])`
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

## How to Use
The hope is that you can use these regular expressions with a variety of approaches. That said, my strategy would be to wrap the regular expressions in enums or something else that can be used in a switch statement. For a given input, I would then loop through a set of regular expressions to look for a match. Once a match is found, I would assign that regular expression to a variable and break the loop. Then I would plug that variable into a switch statement and extract values from the appropriate groups. If the algorithm speed needs to optimized, I would determine a broader variant category first using a different set of regular expressions, then only loop through that smaller subset to look for a match.

## Overwhelmed?
If you are inexperienced with regular expressions or HGVS names, I would recommend starting out with a single regular expression, like [genomic DNA](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-g.md) or [protein](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-p.md) substitutions. The vast majority of HGVS names are for substitutions, and they are among the easiest to use, so they are a natural starting point. [Coding DNA](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-c.md) might be the most difficult to work with because you have to consider things like the 5' UTR, 3' UTR, intron offsets, and strand direction.

## See Also
If you are developing in Python, there are some large projects already on Github, including [counsyl/hgvs](https://github.com/counsyl/hgvs), [biocommons/hgvs](https://github.com/biocommons/hgvs), and [mutalyzer/mutalyzer](https://github.com/mutalyzer/mutalyzer). If you are looking for a command-line or website interface, I would look into [zwdzwd/transvar](https://github.com/zwdzwd/transvar) and [TransVar web](http://bioinformatics.mdanderson.org/transvarweb/), respectively.
