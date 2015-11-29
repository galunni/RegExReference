# RegExReference

Regular Expressions reference and tools

---

**regex.js**</br>
- make use of the javascript regex engine to develop and test a regex on a given input text

---

**reference_chars_soft.md** code examples for the following meta character:</br>
- . single dot
- \ escape chars
- \w alphanumeric char
- \d one number, \s spaces
- \b \B word boundaries
- \C forced match of single byte (char)
- ^ \A begin of a line
- $ \Z \z end of a line/string
- | alternate
- [ ] char class
- ^ negative class
- \W not alphanumeric char
- \D not a number
- \S not a \s
- - class defines a range
- \l \u fold next character's case
- \Q....\E Literal text span


**reference_modifiers.md** code examples for the following regex modifiers:</br>
g global match, i	ignore case, s single line, m multiline, 
o compile once, x	extended free spaces and comments mode, e execute,
c in gc keeps the current position during repeated matching,
\G start of match / end of previous match

**reference_parenthesis_operators.md** code examples for the following parenthesis operators:</br>
- (?:...) - turn off backreferences</br>
- (?modifier-modifier) - turn on/off modifier</br>
- (?modifier-modifier:....) - modifier span</br>
- (?=...) - positive lookahead</br>
- (?!...) - negative lookahead</br>
- (?<=...) - positive lookbehind</br>
- (?<!...) - negative lookbehind</br>
- (?...) - named capture</br>
- (?{...}) - insert perl code</br>
- (??{...}) - dynamic regex</br>
- (?if then|else) - conditional</br>
- (?>...) - atomic grouping</br>

