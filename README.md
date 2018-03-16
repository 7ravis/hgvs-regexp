## Work in Progress
There are many [HGVS nomenclature types and sub-types](http://varnomen.hgvs.org), so my plan is to chip away at the types that I have the most experience with first (cDNA, genomic DNA, and protein). However, if you have any pressing requests, please create an issue because I'm happy to prioritize whichever type would be the most helpful. If you would like to contribute, please do! Each prefix sub-type (e.g. genomic DNA insertions) is a convenient size for a single sitting.

## Overview
This project contains regular expressions for parsing HGVS ([Human Genome Variation Society](http://varnomen.hgvs.org)) sequence variant nomenclature. There are existing projects on Github that provide a high-level API for working with HGVS nomenclature; the purpose of this project is to create a lower-level tool with more focus and documentation on regular expressions that can be used under the hood in your own project.

## Format
There is a prefix file for each HGVS sequence type. For example, the regular expressions for coding DNA are in the `prefix-c.md` file. These markdown files are generally organized by the sub-types used on the [HGVS website](http://varnomen.hgvs.org) (substitution, deletion-insertion, etc.). 

**Example** (not necessarily up-to-date!) copied from the `prefix-c.md` file:

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
The hope is that you can use these regular expressions with a variety of approaches. That said, if I were using them, I would create a collection of all the regular expressions or a separate collection for each prefix (if you're looking at the prefix first to know which collection is relevant). I would wrap each regular expression in an enum or object, so I can access the type (substitution, insertion, etc.). Next, I would loop through the regex collection and use a regex matching API to see if the HGVS name is a match. If it's a match, I would assign that regex type to a variable declared before the loop, then break the loop. Next, I would plug the matching regex type into a switch statement and evaluate the HGVS name again with the matching regex, this time extracting the values that I expect/want. Despite the redundancy of looping over a decent number of regular expressions, this should be a very fast process. 

If you are using the algorithm above on a large data set and the computation time is too slow, you might look for ways to batch similar HGVS names and/or evaluate specific characters or substrings beforehand in order to narrow down the number of regular expressions to loop through. 

## Overwhelmed?
If you are inexperienced with regular expressions or HGVS names, I would recommend starting out with a single regular expression, like [genomic DNA](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-g.md) or [protein](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-p.md) substitutions. The vast majority of HGVS names are for substitutions, and they are among the easiest to use, so they are a natural starting point. [Coding DNA](https://github.com/7ravis/hgvs-regexp/blob/master/prefix-c.md) might be the most difficult to work with because you have to consider things like the 5' UTR, 3' UTR, intron offsets, and strand direction.

## See Also
If you are developing in Python, there are some large projects already on Github, including [counsyl/hgvs](https://github.com/counsyl/hgvs), [biocommons/hgvs](https://github.com/biocommons/hgvs), and [mutalyzer/mutalyzer](https://github.com/mutalyzer/mutalyzer). If you are looking for a command-line or website interface, I would look into [zwdzwd/transvar](https://github.com/zwdzwd/transvar) and [TransVar web](http://bioinformatics.mdanderson.org/transvarweb/), respectively.
