# cDNA 

## Substitution - change
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?([GCTAgcta])?>([GCTAgcta])`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position offset (optional). This number will be captured with a preceding `+` or `-`.
- *Group 3:* reference allele (optional, case-insensitive)
- *non-capturing:* `>` (required)
- *Group 4:* alternate allele (required, case-insensitive)

**Example:** `c.*93+1G>T`
- *Group 1* = `*93`
- *Group 2* = `+1`
- *Group 3* = `G`
- *Group 4* = `T`

## Substitution - no change
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?([GCTAgcta])?=`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position offset (optional). This number will be captured with a preceding `+` or `-`.
- *Group 3:* reference allele (optional, case-insensitive)
- *non-capturing:* `=` (required)

**Example:** `c.-123-64G=`
- *Group 1* = `-123`
- *Group 2* = `-64`
- *Group 3* = `G`

## Deletion-Insertion (indel)
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?(?:_(\d+|\*\d+|-\d+)([+-]\d+)?)?([GCTAgcta]+)?delins([GCTAgcta]+)`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position start (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position start offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `_` (optional)
- *Group 3:* base position stop (optional, but required if `_` is present). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 4:* base position stop offset (optional). This number will be captured with a preceding `+` or `-`.
- *Group 5:* reference sequence (optional, case-insensitive)
- *non-capturing:* `delins` (required)
- *Group 6:* alternate sequence (required, case-insensitive)

**Example:** `c.-775-200_-775-56delinsGA`
- *Group 1* = `-775`
- *Group 2* = `-200`
- *Group 3* = `-775`
- *Group 4* = `-56`
- *Group 6* = `GA`

## Deletion
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?(?:_(\d+|\*\d+|-\d+)([+-]\d+)?)?del([GCTAgcta]+)?`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position start (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position start offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `_` (optional)
- *Group 3:* base position stop (optional, but required if `_` is present). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 4:* base position stop offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `del` (required)
- *Group 5:* deleted sequence (optional, case-insensitive)

**Example:** `c.*40-6_*40-2del`
- *Group 1* = `*40`
- *Group 2* = `-6`
- *Group 3* = `*40`
- *Group 4* = `-2`

## Insertion - simple
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?_(\d+|\*\d+|-\d+)([+-]\d+)?ins([GCTAgcta]+)`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position start (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position start offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `_` (required)
- *Group 3:* base position stop (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 4:* base position stop offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `ins` (required)
- *Group 5:* inserted sequence (required, case-insensitive)

**Example:** `c.240_241insAGG`
- *Group 1* = `240`
- *Group 3* = `241`
- *Group 5* = `AGG`

## Inversion
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?_(\d+|\*\d+|-\d+)([+-]\d+)?inv`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position start (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position start offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `_` (required)
- *Group 3:* base position stop (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 4:* base position stop offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `inv` (required)

**Example:** `c.*77-10_*77-1inv`
- *Group 1* = `*77`
- *Group 2* = `-10`
- *Group 3* = `*77`
- *Group 4* = `-1`

## Duplication - simple
**Regular Expression:** `[cC]\.(\d+|\*\d+|-\d+)([+-]\d+)?(?:_(\d+|\*\d+|-\d+)([+-]\d+)?)?dup([GCTAgcta]+)?`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position start (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position start offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `_` (optional)
- *Group 3:* base position stop (optional, but required if `_` is present). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 4:* base position stop offset (optional). This number will be captured with a preceding `+` or `-`.
- *non-capturing:* `dup` (required)
- *Group 5:* duplicated sequence (optional, case-insensitive)

**Example:** `c.-20-2dupT`
- *Group 1* = `-20`
- *Group 2* = `-2`
- *Group 5* = `T`

