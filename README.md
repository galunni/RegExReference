# RegExReference

Regular Expressions reference and tools - PCRE Flavor

---

**[quick javascript Software for RegEx testing ](http://galunni.github.io/tools/regex_tester.html)** - 
**[view sourcecode on GitHub](./regex.js)**</br>

- this script is making use of the javascript regex engine to test a regular expression on a given text input

---

**[reference_chars_soft.md](./reference_chars_soft.md)**</br>
code examples for the following meta characters:</br>
- . single dot
- \ escape chars
- \w alphanumeric char
- \d one number, \s spaces
- \b \B word boundaries
- \C forced match of single byte (char)
- ^ \A begin of a line
- $ \Z \z end of a line/string
- | alternate
- [] char class
- ^ negative class
- \W not alphanumeric char
- \D not a number
- \S not a \s
- \- inside a class defines a range
- \l \u fold next character's case
- \Q....\E Literal text span


**[reference_modifiers.md](./reference_modifiers.md)**</br>
code examples for the following regex modifiers:</br>
- g global match
- i	ignore case
- s single line
- m multiline
- o compile once
- x	extended free spaces and comments mode
- e execute
- c in gc keeps the current position during repeated matching
- \G start of match / end of previous match

**[reference_parenthesis_operators.md](./reference_parenthesis_operators.md)**</br>
code examples for the following parenthesis operators:</br>
- (?:...) - turn off backreferences
- (?modifier-modifier) - turn on/off modifier
- (?modifier-modifier:....) - modifier span
- (?=...) - positive lookahead
- (?!...) - negative lookahead
- (?<=...) - positive lookbehind
- (?<!...) - negative lookbehind
- (?...) - named capture
- (?{...}) - insert perl code
- (??{...}) - dynamic regex
- (?if then|else) - conditional
- (?>...) - atomic grouping

**[reference_quantifiers.md](reference_quantifiers.md)**</br>
code examples for the following quantifiers</br>
- \* some, one or no one
- ? one or no one
- \+ one or some
- { } a number of {exactly} {min,max} {min,}
- ( ) delimit the value of a quantifier
- *? +? ?? {min,max}? lazy quantifiers
- ?+ ++ *+ {min,max}+ possessive quantifiers

**[reference_perl_operators.md](reference_perl_operators.md)**</br>
code examples of specific regex use in perl</br>
- m/regex/mods simple match
- s/regex/replacement/mods substitute (or count)
- tr/before/after/ transliteration operator
- =~ !~ positive and negative match operators
- regex delimiters
- built in variables:  $` $& $' $1 $2 $+ $^N @- @+
- pos()
- (X|Y) - alternation priority
- study()

---

**references / resources:**</br>
- [Mastering Regular Expressions](http://regex.info/book.html) - in my opinion the best book about Regular Expressions
- [RegEx tester with debugging and backtracking](https://regex101.com/)
- [RegEx tester accepting URL as input](https://www.myregextester.com/)
- [RegEx tester for the ruby engine](http://rubular.com/)
- [Italian corpus regex search engine](http://www.corpusitaliano.it/it/access/advanced_interface.php)


<br/><br/><br/>

The MIT License (MIT)
---

Copyright (c) 2015 Giovanni Alunni

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
