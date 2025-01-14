If you want to highlight text which contains default line separator `|` or the default text separator `:`, you can redefine them with the `lsep` and `tsep` parameters.

For example: 
- `hlt:5^|ˇ: lsep:^ tsep:ˇ` would highlight text from `|` to `:`.

TLDR:
- if you want to highlight `|`, redefined the `lsep`
- if you want to highlight `:`, redefined the `tsep` 

If you want to highlight text which contains a `"` or `'`, escape it with a backslash.
For example: `\"`