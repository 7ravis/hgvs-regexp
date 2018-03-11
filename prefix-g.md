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
