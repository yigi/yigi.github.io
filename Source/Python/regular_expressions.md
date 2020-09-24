https://regex101.com
_____________________________________________________________________________________________________________


## Meta character	Description
- .	Period matches any single character except a line break.

- []	Character class. Matches any character contained between the square brackets.

- [^ ]	Negated character class. Matches any character that is not contained between the square brackets

- *(asteriks)	Matches 0 or more repetitions of the preceding symbol.

- +(plus) Matches 1 or more repetitions of the preceding symbol.

- ?	Makes the preceding symbol optional.

- {n,m}	Braces. Matches at least "n" but not more than "m" repetitions of the preceding symbol.

- (xyz)	Character group. Matches the characters xyz in that exact order.

- |	Alternation. Matches either the characters before or the characters after the symbol.

- \	Escapes the next character. This allows you to match reserved characters [ ] ( ) { } . * + ? ^ $ \ |

- ^	Matches the beginning of the input.

- $	Matches the end of the input.


_____________________________________________________________________________________________________________

## Shorthand	Description
- .	Any character except new line

- \w	Matches alphanumeric characters: [a-zA-Z0-9_]

- \W	Matches non-alphanumeric characters: [^\w]

- \d	Matches digit: [0-9]

- \D	Matches non-digit: [^\d]

- \s	Matches whitespace character: [\t\n\f\r\p{Z}]

- \S	Matches non-whitespace character: [^\s]

_____________________________________________________________________________________________________________




### 1.  get only numbers

```
20.02.001.X-M,! 
\d+
```

### 2. get string with any character

```
daaqsa3q120*"889^e442aq3fsdf+.d
aq.
```

### 3. get string with any starting character

```
The car parked in the garage.
[Tt]he
```

### 4. get string with following character

```
The car parked in the garage.
ar[.] -> ar.
ar+ -> ar ark ara
```

### 5. get string without starting character

```
The car parked in the garage.
[^c]ar -> par gar
```

### 6. get string ending with specific character

```
The fat cat. sat. on the mat.
"(at\.)$" -> mat.
```

