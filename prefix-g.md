# Genomic DNA 

## Substitution - change
**Regular Expression:** `(?:[gG]\.)(\d+)([GCTAgcta])?>([GCTAgcta])`
- *non-capturing:* `g.` (required, case-insensitive)
- *Group 1:* base position (required)
- *Group 2:* reference allele (optional, case-insensitive)
- *non-capturing:* `>` (required)
- *Group 3:* alternate allele (required, case-insensitive)

**Example:** `g.33038255C>A`
- *Group 1* = `33038255`
- *Group 2* = `C`
- *Group 3* = `A`

## Substitution - no change
**Regular Expression:** `(?:[gG]\.)(\d+)([gctaGCTA])?=`
- *non-capturing:* `g.` (required, case-insensitive)
- *Group 1:* base position (required)
- *Group 2:* reference allele (optional, case-insensitive)
- *non-capturing:* `=` (required)

**Example:** `g.59283=`
- *Group 1* = `59283`

## Deletion-Insertion (indel)
**Regular Expression:** `(?:[gG]\.)(\d+)(?:(?:_)(\d+|\*\d+|-\d+))?([GCTAgcta]+)?delins([GCTAgcta]+)`
- *non-capturing:* `g.` (required, case-insensitive)
- *Group 1:* base position start (required)
- *non-capturing:* `_` (optional)
- *Group 2:* base position stop (optional, but required if `_` is present)
- *Group 3:* reference sequence (optional, case-insensitive)
- *non-capturing:* `delins` (required)
- *Group 4:* alternate sequence (required, case-insensitive)

**Example:** `g.14325_14326TAdelinsC`
- *Group 1* = `14325`
- *Group 2* = `14326`
- *Group 3* = `TA`
- *Group 4* = `C`
