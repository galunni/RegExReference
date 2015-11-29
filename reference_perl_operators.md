reference_perl_operators.md

Regular Expression Reference
---

Perl specific operators
---

**m/regex/mods - simple match**</br>

---
**s/regex/replacement/mods	- substitute (or count)**</br>
substitute and (if needed) gives back how often the match has been substituted
```perl
echo "superman" | perl -pe 's/man/woman/;' # output: superwoman
echo "abc" | perl -pe 'print s/ab/X/;' # output: 1Xc
echo "abcdabdeab" | perl -pe '$a= s/ab/X/g; print "---$a---\n";'
# output:
# ---3---
# XcdXdeX
```

---

**tr/before/after/ - transliteration operator**
the tr operator does not accept regexes, everything is treated as a character
```perl
echo "paperino" | perl -pe 'tr/pao/PAO/;' # output: PAPerinO
echo "p.*" | perl -pe 'tr/p.*/P?+/;'      # output: P?+
```

---

