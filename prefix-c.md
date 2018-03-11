# cDNA 

## Substitution
**Regular Expression:** `(?:[cC]\.)(\d+|\*\d+|-\d+)([+-]\d+)?([GCTAgcta])>([GCTAgcta])`
- *non-capturing:* `c.` (required, case-insensitive)
- *Group 1:* base position (required). If there is a `*` or `-` preceding the number, it will also be captured.
- *Group 2:* base position offset (optional). This number will be captured with a preceding `+` or `-`.
- *Group 3:* reference allele (require, case-insensitived)
- *non-capturing:* `>` (required)
- *Group 4:* alternate allele (required, case-insensitive)

**Example:** `c.*93+1G>T`
- *Group 1* = `*93`
- *Group 2* = `+1`
- *Group 3* = `G`
- *Group 4* = `T`
