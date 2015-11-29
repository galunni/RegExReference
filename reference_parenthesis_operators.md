reference_parenthesis_operators.md

Regular Expression Reference
---
PCRE compared to other flavors

Parenthesis operators
---

**(?#...) - comment**</br>
```perl
echo "abc" | perl -pe 's/a(?#this is just a comment)/A/;'  # output: Abc
```

---

**(?:...)	- turn off backreferences**</br>
do not apply backreference to this pharenthesis (faster)</br>
helpful when you need grouping, quantifying or alternating and you do not need backreferences</br>
```perl
echo "abc" | perl -pe 's/(?:ab|c)/CASA/g;'	 # output: CASACASA
```

---

**(?modifier-modifier)	- turn on/off modifier**</br>
i, x, s, m are allowed
```perl
echo 'abc' | perl -ne 'if(/(?i)A(?-i)bc/){print $_;}'    # output: abc
```
in the past example the "ignore case" modifier was turned on and off inside the regex

---

**(?modifier-modifier:....)	- modifier span**</br>
works like the turn on/off modifier explained above, but the influence is only limited to the non capturing parenthesis
```perl
echo "the Dog" | perl -ne 'print if/(?s-i:the).*dog/i'   # output: 
```
in the example above the s modifier is temporary turned on inside the parenthesis and the i modifier is turned off

---

**(?=...)	- positive lookahead**</br>
match but do not consume</br>
```perl
echo "My Name" | perl -pe 's/My (?=Name)/Your/g;'          # output: YourName
echo "Frau Guenda" | perl -pe 's/(?=Frau Gue)Frau/Herr/g;' # output: Herr Guenda
echo "the name" | perl -pe 's/(?=name)/best /g;'         # outupt: the best name
```
Notice how in the last example nothing was removed. The lookahead operator is useful there to find the
right position for the substitution.

---


