reference.md

Regular Expression Reference
---
PCRE compared to other flavors

**.  single dot**<br/>
one char - it may not mach a newline (depending on s modifiert settings) - like ? in the bash
```perl
echo "a" | perl -ne 'print if/a/;' # output: a
```
```perl
echo "b" | perl -ne 'print if/a/;' # output:
```

**\	 escape chars**<br/>
turn on/off an escape - you mostly don't need to use it in a class (except for ^ and -)<br/>
\b act as a backspace if used in a class, otherwise is \b a word boundary
```perl
echo "C1" | perl -ne 'print if(/C1\n/);' # output: C1
echo "the (cat)" | perl -ne 'print if(/the \(cat\)/);' # output: the (cat)
echo "(" | perl -pe 's/[(]/MAMMA/;' # output: MAMMA
```
```perl
echo "the (cat)" | perl -ne 'print if(/the (cat)/);' # output:
echo "(" | perl -pe 's/(/MAMMA/;' # error: Unmatched ( in regex; marked by <-- HERE in m/( <-- HERE
```
\a alert, \b backspace, \e escape, \f form feed, \r carriage return, \t horizontal tab, \v vertical tab,
\cchar control char (\cg), \number octal escape (\077), \xnumber hex escape (\xFF)


**\w  one alphanumeric char**<br/>
like [a-zA-z0-9_] and eventually other unicode letters (depending on your local environment)
```perl
echo "C1" | perl -ne 'print if(/\w/);' # output: C1
```
```perl
echo "$&" | perl -ne 'print if(/\w/);' # output:
```

**\d  one number**<br/>
like [0-9]
```perl
echo "123" | perl -ne 'print if(/\d/);' # output: 123
```
```perl
echo "abc" | perl -ne 'print if(/\d/);' # output:
```

**\s  spaces tabs and newlines**<br/>
like [ \t\n\r] - doesn't match a \v (vertical tab)<br/>
```perl
echo "1 2" | perl -ne 'print if(/\s/);' # output: 1 2
```

***\b \B word boundary (or not)**<br/>
since perl 5.8: fully support unicode - matches just a position not a char!! - means backspace if used in a class<br/>
egrep (usually): \< (begin) \>(end)
```perl
echo "il cane" | perl -ne 'print if(/il\b/);' # output: il cane
```
```perl
echo "il cane" | perl -ne 'print if(/il\bcane/);' # output:
```

