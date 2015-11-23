reference_quantifiers.md

Regular Expression Reference
---
PCRE compared to other flavors

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
