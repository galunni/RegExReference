reference_perl_operators.md

Regular Expression Reference
---

Perl specific operators
---

**m/regex/mods - simple match**</br>
```perl
echo "Russia" | perl -ne 'print "yes\n" if(/russ/i);'
```

---
**s/regex/replacement/mods	- substitute (or count)**</br>
substitute and (if needed) gives back how often the match has been substituted
```perl
echo "superman" | perl -pe 's/man/woman/;' # output: superwoman
echo "abc" | perl -pe 'print s/ab/X/;'     # output: 1Xc
echo "abcdabdeab" | perl -pe '$a= s/ab/X/g; print "---$a---\n";'
# output:
# ---3---
# XcdXdeX
```

---

**tr/before/after/ - transliteration operator**</br>
the tr operator does not accept regexes, everything is treated as a character
```perl
echo "paperino" | perl -pe 'tr/pao/PAO/;' # output: PAPerinO
echo "p.*" | perl -pe 'tr/p.*/P?+/;'      # output: P?+
```

---

** =~ !~ - positive and negative match operators**

---

**regex delimiter - how can I delimit my regex /.../**</br>
/ works, but you can use almost every non alphanumeric simple visible ascii char</br>
the reason can be: save as many backslashes as possible</br>
echo "a&b&c" | perl -pe 's/&/X/g;'             # output: aXbXc
echo "a/b/c" | perl -pe 's&/&X&g;'             # output: aXbXc
echo "a/b/c" | perl -pe 's+/+X+g;'             # output: aXbXc
echo "a*b+c/d&e" | perl -pe 's#[*+/&]#X#g;'    #output: aXbXcXdXe

---

**built in variable**</br>
$\`	text before match</br>
$&	text matched</br>
$'	text after match</br>
$1	text matched with first parentheses</br>
$2	text matched with second parentheses</br>
$+	text matched with highest numbered parentheses</br>
$^N	text matched with most recently closed parentheses</br>
@-	array of match-start indices into target text</br>
@+	array of match-end indices into target text</br>
for better efficiency avoid $& $' $` and backref where possible</br>

---

**pos()**
Used to obtain the actual position of the match.
But you can also use the function to set the start of the match.
NEVER FORGET the g modifier when doing it!
```perl
perl -e '$a="a1a2a3"; pos($a)=3; if($a =~ /(a.)/g){print "$1\n";}'    # output: a3
```

---

**(X|Y) - about alternation**</br>
Some Implementation study the length of X and Y in order to support greedy alternation.</br>
This may take a longer time.</br>
Perl always takes the left first match of an alternation.</br>
```perl
echo "ab" | perl -pe 's/(ab|a)/X/;'   # output: X
echo "ab" | perl -pe 's/(a|ab)/X/;'   # output: Xb
```

---

**study()**</br>
When the string to analyze is very long and you need to match many regexex on it, you can first study it.
```perl
echo 'dudududadada' | perl -pe 'study($_); s/(u|a)/X/g;'     # output: dXdXdXdXdXdX
```
---
