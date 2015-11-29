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

**(?!...)	- negative lookahead**</br>
negative match but do not consume</br>
```perl
echo "Max Mad" | perl -pe 's/Max(?! Good)/Marc/g;'     # output: Marc Mad
```

---

**(?<=...)	- positive lookbehind**</br>
match but do not consume</br>
only support static length regex</br>
```perl
echo "ab cd ab ef" | perl -pe 's/(?<=cd )ab/X/g;'           # output: ab cd X ef
echo "ab cd ab ef" | perl -pe 's/ab(?<=cd ab)/X/g;'         # output: ab cd X ef
echo "Jeffs" | perl -pe 's/(?<=\bJeff)(?=s\b)/`/;'          # output: Jeff`s
echo "Jeffs" | perl -pe 's/(?=s\b)(?<=\bJeff)/`/;'          # output: Jeff`s
echo "12345678"|perl -pe 's/(?<=\d)(?=(?:\d{3})+$)/./g;'    # output: 12.345.678
```

```perl
echo "ab cd ab ef" | perl -pe 's/ab(?<=cd )/X/;'            # output: ab cd ab ef
echo "ab cd ab ef" | perl -pe 's/(?<=cd +)ab/X/g;'          # error in perl only static length is supported!
# Variable length lookbehind not implemented in regex m/(?<=cd +)ab/ at -e line 1.
```

---

**(?<!...) - negative lookbehind**</br>
match but do not consume</br>
only support static length regex
```perl
echo "abac" | perl -pe 's/(?<!b)a/X/g;'    # output: Xbac
echo "abac" | perl -pe 's/(?<!^)a/X/g;'    # output: abXc
echo "abac" | perl -pe 's/(?<!c)a/X/g;'    # output: XbXc
```

---

**(?<name>...) - named capture**</br>
giving names to backreferences provide a better overview</br>
only supported by python and .NET</br>
```
echo 'abc' | perl -ne 'if(/a(?<uno>.)c/){print $uno;}'  # .net (not working in perl)
echo 'abc' | perl -ne 'if(/a(?P<uno>.)c/){print $uno;}' # python (not working in perl)
```

---

**(?{...}) - insert perl code**</br>
only supported by perl engine</br>
interesting for debugging+learning purposes</br>
avoid use in CGI for security reasons</br>
WARNING: This extended regular expression feature is considered highly 
experimental, and may be changed or deleted without notice.
```perl
echo "mamma" | perl -pe 's/.(?{print "debug:-$&-\n";})/-$&/g;'
# output: debug:-m-
# output: debug:-a-
# output: debug:-m-
# output: debug:-m-
# output: debug:-a-
# output: -m-a-m-m-a

echo "mamma" | perl -ple 's/.(?{print "debug:-$`-$&-" . pos($_) . "-";})/X$&/g;'
# output: debug:--m-1-
# output: debug:-m-a-2-
# output: debug:-ma-m-3-
# output: debug:-mam-m-4-
# output: debug:-mamm-a-5-
# output: XmXaXmXmXa

---

**(??{...})	- dynamic regex**</br>

---

**(?if then|else)	- conditional**
not always supported</br>
```perl
echo "abc" | perl -pe 's/(?(?<=a)b|c)/X/;'    # output: aXc
echo "abc" | perl -pe 's/(?(?<=a).c|b)/X/;'   # output: aX
```

---

**(?>...)	- atomic grouping**
does not allow backtracking to the matches (increasing speed)</br>
supported by: perl, java, .net, ruby</br>
backrefs are turned off by this operator</br>

```perl
perl -le 'print $& if "abcd" =~ /(?>\w+)/'    # output: abcd
```

```perl
perl -le 'print $& if "abcd" =~ /(?>\w+)d/'   # output: 
```
The example above uses atomic grouping.</br>
The \w matches every letter in abcd to the end of the string.</br>
Since backtracking is not allowed, when trying to match d the regex fails.

---

