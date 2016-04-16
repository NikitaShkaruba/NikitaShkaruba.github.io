---
title: "Hello, regular expressions"
ref: hello-regular-expressions
layout: post
lang: en
---

Hello, today i want to talk about *Regular expressions* - which are really powerful tool for work with text.
Every programming language supports them, so be confident with them is important.
Form validation, text substitution, replacement, or even simple pattern seek - it's easy for regexes.
Have you ever saw masks like "\*.pdf" or "123.???", so regexes - is just a really powerful masks :)

### Regular expressions in Ruby(which is needed for next samples)
Regexes is embedded in language itself, we can use them like that:

* Operator `=~` which returns matched position in the string

```Ruby
"Pretty notation" =~ /notation/ # => 7
"wtf" =~ regex                  # => nil
```

* Regex.match(str) - it returns object `<MatchData>` which contains some information about match

```Ruby
matchData = /mismatch/.match("What is regex?") # => nil#
matchData = /(Java).*(Ruby)/.match("Java is good, but I am so in love with Ruby!")  # => <MatchData>

# Captured groups
matchData.captures        # => ["Java", "Ruby"]
matchData[0]              # => "Java"
matchData.captures 0              # => "Java"

# matched positions
matchData.begin(0)        # => 0    Regex itself position
matchData.begin(1)        # => 0    Group 1 position
matchData.begin(2)        # => 39   Group 2 position

# String before and after match
matchData.pre_match       # => ""
matchData.post_match      # => "!"
```

### Basics
Every symbol sequence in regex means exactly that sequence itself

```Ruby
"ab" =~ /abc/                     # => nil
"abc" =~ /abc/                    # => 0
"christmas" =~ /Merry christmas/  # => nil
"Nick" =~ /Nick/                  # => 0
```

We can use wildcard-characters, which means everything but the newLine-symbol
'.' - Every symbol but newLine-symbol

```Ruby
"health" =~ /.ealth/       # => 0
"wealth" =~ /.ealth/       # => 0
```

[some symbols] - means one of those symbols inside brackets

```Ruby
"health" =~ /[hw]ealth/       # => 0
"wealth" =~ /[hw]ealth/       # => 0
"realth" =~ /[hw]ealth/       # => nil

# 1, т.к. получается лишь один символ, а не их последовательности
"stealth" =~ /[st]ealth/       # => 1
```

We can use ranges!

```Ruby
"8" =~ /[0-9a-z]/       # => 0
"f" =~ /[0-9a-z]/       # => 0
```

[^some symbols] - '^' means everything but symbols inside

```Ruby
"2" =~ /[^0-9]/       # => nil
"b" =~ /[^0-9]/       # => 0
```

### Special escape-sequences
Because these ones are often used, there are special symbols for them

```Ruby
/\d/  # (digit) - every digit
/\w/  # (word) - every digit, alphabetical character of _
/\s/  # (space) - every space-character - space, tab or newLine
```

And their reverses

```Ruby
/\D/  # everything but every digit
/\W/  # everything but every digit, alphabetical character of _
/\S/  # everything but every space-character - space, tab or newLine
```

### Repetition symbols
In regex there are special symbols that causes pattern repeated several times

* ? - zero or one
* \+ - one or more
* \* - zero or more
* {5} - exactly 5 times
* {2, 8} - from 2 to 8 times
* {2,} - two or more
* {,4} - up to four times

```Ruby
/(hello )?world!/.match("hello world!")   # regexData
/(hello )?world!/.match("bye world!")     # regexData
/.*world!/.match("hello there, world!")   # regexData
/(hi ){1, 3}.+/.match("hi hi Mathew")     # regexData
```

### String capturing
One of the really good features in regual expressions is string capturing, which are stored in regexData object
Earlier the parenthesis - lower index

```Ruby
fullNameRegex = /([A-Z][a-z]+ ){3}/
matchData = dateRegex.match("Matthew David McConaughey")

matchData.captures        # => ["Matthew", "David", "McConaughey"]
name = matchData[0]       # => "Mathew"
patronymic = matchData[1] # => "David"
surname = matchData[2]    # => "McConaughey"
```

Grouping without capturing(for repetition symbols) is made by symbol '?:'

```Ruby
/(?:20|19){2}/.match("2020").captures   # => []
```

### Bounds
* ^ - points at the beginning of string
* $ - point at the end of the string
* \b - point at the beginning of the word
* \B - point at the end of the word

```Ruby
# Hexadecimal digit in C-notation
/^0x[0-9a-fA-F]{1,8}$/
# matches: 0x5f3759df, 0xDEADBEEF
# not matches: 0x1234xxx, xxx0x5678, xxx0x9ABCxxx

/\bruby\B/
# matches: hello ruby
# not matches: hello rubymine
```

### Some handy examples
```Ruby
# String substitution
"My name is Andrew".sub /My name is/, "Hi, I'm"   # => "Hi, I'm Andrew"
"The man in the park".gsub /the/, "a"             # => "a man in a park"

# String reformatting
"1234567890".sub /(\d{3})(\d{3})(\d{4})/, '(\1) \2-\3' # => "(123) 456-7890"

# Get all the images from page
require "open-uri"

imgLinks = /<img\s+src=\"(.+)\"\/>/.match(File.open("somePage.html").read)

imgLinks.each_with_index do |link, index|
  File.open('img' + index ".img", 'wb') do |file|
    file.write open(link).read
  end
end

# Form validation
dayRegex = /(0[1-9]|1[0-9]|2[0-9]|3[0-1])/
monthRegex = /jan|feb|mar|apr|may|jun|jul|aug|sep|oct|nov|dec/i
yearRegex = /(201[4-9]|202[0-9])/
dateRegex = /#{dayRegex}-#{monthRegex}-#{yearRegex}/

fullNameRegex = /([A-Z][a-z]+ ){3}/

phoneNumberRegex = /(+7|8)\d{10}/
```

### Afterword
So, that's all. You just need some practice to be used with regex.
My absolutelly favourite cite for testing regexes online is: [regex101.com](https://regex101.com/)
And if you don't want to practice, you can always google needed regular expressions.

Hey, see you :smile: And stay awesome, my reader! :wink:
