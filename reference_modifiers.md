reference_modifiers.md

Regular Expression Reference
---
PCRE compared to other flavors

MODIFIERS
---

**i	- ignore case**</br>
makes the pattern case insensitive
```perl
echo "A" | perl -ne 'print if(/a/i);'  # output: A
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

**s	- . matches also \n**</br>
```perl
echo "" | perl -ne 'print "yes\n" if/./s;'   # output: yes
```
```perl
echo "" | perl -ne 'print "no\n" unless/./;' # output: no
```

---

**m	- multiline match**</br>
if used ^ and $ also match begin and end of a line</br>
does not influences \A and \Z</br>
in perl overwrites the $* var

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



