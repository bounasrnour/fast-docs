Find a specific alphabet

Regex starts with / and ends with / in python r ""

```python
#find a
a = r"/a/"
# add g for global all occurences
a = r"/a/g"

```

## Insensitive more

match Tree and tree using /tree/ i

## Single line

/a/ s

## Multiline

/a/ m

## Metacharacters

- \d : matches digits 0 to 9
- \D matches anything but numbers 0 to 9
- \w matches word a to z upper and lower, 0 to 9 and underscore
- \W matches anything but \w
- \s matches whitespace , space, tab
- \S matches all but \s
- . : dot wildcard , it matches all, it will match the first character whatever it is 
- ? check if character is present of not, / flavo?r / , optinal character, ,atch if the character r is there or not (both cases)
- the * match for 0 or more repetition 
-  for one or more repetition use + 
- {} precise number of match example / \d{4} / match 4 digits
- / \d{2,5} / match min 2 digits 5 at max

To match Positions instead of character use **Anchors**

- ^ matches the start of a string
- $ matches the end of a string 
- \b word boundary 

## Alternation

- |  example / I\slike \s(java|python) /g

## Character Class

[class] example / gr[ae]y / g will match grey and gray

use - for range insteaf od [abcdef] use [a-f]

## Negated Char Class

[^A-Z] not [A-Z]

a [ ^ b ] does not mean a not followed by b, it means a followed by a character that is not b.













##