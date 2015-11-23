reference.md

Regular Expression Reference
---
PCRE compared to other flavors

META CHARS SOFT
---

**. - single dot**<br/>
one char - it may not mach a newline (depending on s modifiert settings) - like ? in the bash
```perl
echo "a" | perl -ne 'print if/a/;' # output: a
```
```perl
echo "b" | perl -ne 'print if/a/;' # output:
```

---

**\	- escape chars**<br/>
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

---

**\w - one alphanumeric char**<br/>
like [a-zA-z0-9_] and eventually other unicode letters (depending on your local environment)
```perl
echo "C1" | perl -ne 'print if(/\w/);' # output: C1
```
```perl
echo "$&" | perl -ne 'print if(/\w/);' # output:
```

---

**\d - one number**<br/>
like [0-9]
```perl
echo "123" | perl -ne 'print if(/\d/);' # output: 123
```
```perl
echo "abc" | perl -ne 'print if(/\d/);' # output:
```

---

**\s - spaces tabs and newlines**<br/>
like [ \t\n\r] - doesn't match a \v (vertical tab)<br/>
```perl
echo "1 2" | perl -ne 'print if(/\s/);' # output: 1 2
```

---

**\b \B - word boundary (or not)**<br/>
since perl 5.8: fully support unicode - matches just a position not a char!! - means backspace if used in a class<br/>
egrep (usually): \< (begin) \>(end)
```perl
echo "il cane" | perl -ne 'print if(/il\b/);' # output: il cane
```
```perl
echo "il cane" | perl -ne 'print if(/il\bcane/);' # output:
```

---

**\C - forced match of single byte (char)**<br/>
not so smart if using utf-8 - lookbehind still not supported

---

**^ \A - begin of a line/string**<br/>
\A does not respect the m mode -  ^ has a different meaning into a class.

---

**$ \Z \z	- end of a line/string**<br/>
\Z does not respect the m mode -\z matches just after the last \n and not before
```perl
echo "duc" | perl -ne 'print if(/c$/);' # output: duc
echo "duc" | perl -ne 'print if(/c\Z/);' # output: duc
echo "duc" | perl -ne 'print if(/c\n\Z/);' # output: duc
echo "duc" | perl -ne 'print if(/c\n\z/);' # output: duc
```
```perl
echo "duc" | perl -ne 'print if(/c\z/);' # output:
```

---

**| - alternate**<br/>
```perl
echo "a" | perl -ne 'print if(/a|b/);' # output: a
```
```perl
echo "d" | perl -ne 'print if(/a|b|c/);' # output:
```

---

**[ ] - create a class**<br/>
inside a class only ^ and - are metachars
```perl
echo "a" | perl -ne 'print if(/[ab]/);' # output: a
```
```perl
echo "A" | perl -ne 'print if(/[ab]/);' # output:
```
```perl
echo "ca" | perl -ne 'print if(/[[a-z]&&[^aeiou]]/);');' # this only works in java regex engine

#for doing the same in perl use lookarounds: 
echo "ca" | perl -ne 'print if(/(?![aeiou])[a-z]/);' + output: ca
```

---

**^ - something not in the class**<br/>
Meaning of [^x] -> Match unless there is an x
^ has a different meaning out of a class (as explained above)

```perl
echo "Ce" | perl -ne 'print if(/C[^abc]/);' # output: Ce
```
```perl
echo -n "C" | perl -ne 'print if(/C[^ABC]/);' # output:
```

---

**\W	- something that is not an alphanumeric char**<br/>
same as [^a-zA-Z0-9_] and eventually unicode letters depending on your local environmen

---

**\D	- something that is not a number**<br/>
like [^0-9]

---

**\S -	something that is not a \s**<br/>
like [^\s]

---

**-	- defines a range**<br/>
- has this meaning just in a class
```perl
echo "5" | perl -ne 'print if(/[4-6]/);' # output: 5
```
```perl
echo "5" | perl -ne 'print if(/[6-8]/);' # output:
echo "5" | perl -ne 'print if(/[3-40]/);' # output:
```

---

**\l \u	- fold next character's case**<br/>
lowercase / uppercase next char
```perl
echo "AbC" | perl -pe 's/A\lBC/X/;' #output: X
```

---

***\Q....\E	- Literal text span***<br/>
\Q turns off every metachar, until \E - Supported only by java and perl - VB uses Regex.escape method instead
```perl
echo "[" | perl -pe 's/\Q[/X/;' # output: X
echo "[g" | perl -pe 's/\Q[\E[a-z]*/X/;' # output: X
````

---

**\U \L ... \E	- Case folding span**
useful to turn upper/lower case on/off on the fly - Make sense used with variables
```perl
echo "abcde" | perl -ne '$a="CD";print if/ab\L$a\Ee/;' # output: abcde
````

QUANTIFIERS
---

**\*	- quantifier: some, one or no one**</br>
```perl
echo "13" | perl -ne 'print if(/12*3/);' # output 13
echo "1222223" | perl -ne 'print if(/12*3/);' # output: 1222223
```

---

**?	- quantifier: one or no one**<br/>
```perl
echo "13" | perl -ne 'print if(/12?3/);' output: 13
echo "123" | perl -ne 'print if(/12?3/);' # output: 123
```

---

**+	- some, or at less one**<br/>
x+ means the same as xx*
```perl
echo "12223" | perl -ne 'print if(/12+3/);' # output: 12223
echo "123" | perl -ne 'print if(/12+3/);' # output: 123
```

---

**{ }	- quantifier: a number of	{exactly} {min,max} {min,}**<br/> 
The min is required, the max allowed
```perl
echo "abbc" | perl -ne 'print if(/ab{2}c/);' # output: abbc
echo "abbbbbc" | perl -ne 'print if(/ab{3,}c/);' # output: abbbbbc
```
```perl
echo "abbbbbc" | perl -ne 'print if(/ab{2,4}c/);' # output:
```

---

**( ) -	delimit the value of a quantifier**<br/>
() are also used for many other reasons such as 

