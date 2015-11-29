reference_modifiers.md

Regular Expression Reference
---
PCRE compared to other flavors

MODIFIERS
---

**g - global match**</br>
```perl
echo "abaca" | perl -ne 'while(/.?a/g){print "$&-";}'  # output: a-ba-ca-
```
```perl

```perl
# notice how the g modifier does not have an influence if not setted inside a loop
echo "abaca" | perl -ne 'if(/.?a/g){print "$&\n";}'    # output: a 
```

---

**i	- ignore case**</br>
makes the pattern case insensitive
```perl
echo "A" | perl -ne 'print if(/a/i);'  # output: A
```

---

**s	- . matches also \n**</br>
```perl
echo "" | perl -ne 'print "yes\n" if/./s;'   # output: yes
```
```perl
echo "" | perl -ne 'print "no\n" unless/./;' # output: no
```

---

**o -	compile only once**</br>
Makes the regex execution faster.</br>
Do not use this operator if the RegEx contain a variable which is changing when using the RegEx a second time.</br>
If your RegEx doesn't contain variables, the modificator o is automatically on.</br>

notice how in this example the $a variable is not changing because of the o modifier
```perl
echo "1234
1234
1234
1234"  | perl -ne '$a=$.; s/$a/X/o; print;'
# output: X234
# output: X234
# output: X234
# output: X234
```

instead of changing with every interaction in absence of the o modifier
```perl
echo "1234
1234
1234
1234"  | perl -ne '$a=$.; s/$a/X/; print;'
# output: X234
# output: 1X34
# output: 12X4
# output: 123X
```

---

**x	- extended free spaces and comments mode**</br>
```perl
#!/usr/bin/perl -w
use strict;

undef $/;
$_=<>;

s/^.+<table/<html><body><table/s;


s/<tr>[^<]+?
    
    <td>(.+?)<\/td>[^<]+?
    
    <td>(.+?)<\/td>[^<]+?

    <td>(.+?)<\/td>[^<]+?

  <\/tr>
/
    <tr>
    <td><br><h3 style='color:blue;'>  $1 <\/h3> <br><\/td>
    <td><br><h3 style='color:red;'>   $2 <\/h3><br><\/td>
    <td><br><h3 style='color:green;'> $3 <\/h3><br><\/td>
    <\/tr>
/sxg;

print $_;
```

---

**c in gc - keep the current position during repeated matching**</br>

```perl
# notice how in this case using gc mofifier after the first regex the pos() is setted to 4 and
# how the second regex only outputs one "a" (the last one in the string)
echo "mamma" |
perl -ne 'while(/m/gc) {print $& . pos() . "-";} print "after: " . pos() . "\n"; while(/a/g) {print $&;}'
# output: m1-m3-m4-after: 4
# output: a
```

```perl
# notice in this case without the gc modifier the pos() after the first regex is unset
# and the second regex matches two times an a because in starts matching from the beginning of the string
echo "mamma" |
perl -ne 'while(/m/g) {print $& . pos() . "-";} print "after: " . pos() . "\n"; while(/a/g) {print $&;}'
# output: m1-m3-m4-after: 
# output: aa
```

in other words using the gc modifiers the pos() is not resetted after a failure match and the second regex starts when the first one failed

---

