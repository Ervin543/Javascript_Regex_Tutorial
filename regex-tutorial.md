# Javascript Regex Tutorial (Matching an HTML Tag)

This Gist was created in order to better explain the uses and applications of Regular Expressions, or a Regex for short. It aims to showcase a specific Regex and hopefully break down its most basic fundamentals in order to make it easier to understand and implement.

## Summary

This Regex matches an opening HTML tag followed by optional attributes and a closing tag (if it's not a self closing tag). The Regex uses capturing groups to extract the tag name and any content within the tags. We'll be using the Regular Expression below to match an HTML tag:
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

Anchors are used to match a specific position in the string. This Regex uses two anchors: `^` and `$`. The caret (`^`) matches the start of a string, while the dollar sign (`$`) matches the end of a string.
Code Snippet:
(Start) =>  /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/  <=(End)

Example:

Suppose we have the following HTML Tag:
<div class="container">Hello, world!</div>

To match this tag using our Regex, we would do the following:
const regex = /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/;
const html = '<div class="container">Hello, world!</div>';
const match = regex.exec(html);
console.log(match[0]); // "<div class="container">Hello, world!</div>"


### Quantifiers

Quantifiers specify how many times a character or group should be matched. This Regex expression uses the `+` quantifier to match one or more characters, amd the `*` quantifier to match zero or more characters.  
Code Snippet:
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
       +      *
      
Example:
Suppose we have the following HTML Rag:
<p>This is a paragraph</p>

To match this tag using our Regex, we would do the following:
const regex = /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/;
const html = '<p>This is a paragraph</p>';
const match = regex.exec(html);
console.log(match[0]); // "<p>This is a paragraph</p>"

### OR Operator

The OR operator `|` allows you to match any one of a set of alternatives. For example, to match either "cat" or "dog", you can use the regular expression `/cat|dog/`. The `|` character is used to separate the alternatives. This regular expression will match either the string "cat" or the string "dog".
Example:
Suppose you want to find all instances of the words "color" or "colour" in a text. You can use the following regular expression:
/colou?r/
The `?` character in the regular expression specifies that the preceding "u" character is optional. This regular expression will match both "color" and "colour".

const text = "The color of the sky is blue, but in England they spell it colour.";
const regex = /colou?r/g;
const matches = text.match(regex);
console.log(matches); // Output: ["color", "colour"]

In the above example, the regular expression `/colou?r/g` matches both "color" and "colour" in the given text. The `g` flag is used to perform a global search, meaning that it will find all matches in the text, not just the first one.


### Character Classes

Character classes are used to match any character within a set of characters. In the Regex `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, we use the character class `[a-z]` to match any lowercase letters from a to z. This is used to match the tag name, which is always made up of lowercase letters.
Example:
const regex = /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/;
const match = '<div class="container">Hello World!</div>'.match(regex);
console.log(match[1]); // Output: div

In this example, the Regex matches the opening `div` tag and captures the tag name using the character class `[a-z]`. The captured tag name is then outputted to the console using `match[1]`

### Flags

Flags are used to modify the behavior of a Regex. In the Regex `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, we don't use any flags, but there are several flags that can be used with Regular Expressions.

Here are some common Flags:
* `g` - Global Match.
* `i` - Case-Sensitive Match
* `m` - Multi-Line Match

Example: Here we are using the `g` Flag:
const regex = /hello/g;
const str = 'Hello, hello, HELLO!';
const matches = str.match(regex);
console.log(matches); // Output: ["hello", "hello"]

In this example, the `g` flag is used to perform a global match, which finds all occurences of the word "hello" in the string.

### Grouping and Capturing

Grouping and capturing are used to capture part of a match. In the regex `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`, we use grouping and capturing to capture the 'tag name' and 'tag content'.
Example:
const regex = /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/;
const match = '<div class="container">Hello World!</div>'.match(regex);
console.log(match[1]); // Output: div
console.log(match[3]); // Output: Hello World!

In this example, the regex matches the opening `div` tag and captures the tag name and tag content using grouping and capturing. The captured tag name and tag content are then outputted to the console using `match[1]` and `match[3]`, respectively.

### Bracket Expressions

A bracket expression is a way to match a single character out of a set of characters. You can use square brackets `[]` to define a bracket expression. For example, the regular expression `/[abc]/` will match any single character that is either "a", "b", or "c".
Example:
Suppose you want to find all instances of vowels in a text. You can use the following regular expression:
/[aeiou]/
This regular expression will match any single character that is either "a", "e", "i", "o", or "u".
const text = "The quick brown fox jumps over the lazy dog";
const regex = /[aeiou]/g;
const matches = text.match(regex);
console.log(matches); // Output: ["e", "u", "i", "o", "o", "u", "e", "a", "o"]

In the above example, the regular expression `/[aeiou]/g` matches all vowels in the given text. The `g` flag is used to perform a global search, meaning that it will find all matches in the text, not just the first one.

### Greedy and Lazy Match

When a regular expression contains quantifiers, such as `*`, `+`, or `?`, it will match as much as it can by default. This is called greedy matching. However, you can make a quantifier lazy by adding a `?` after it.

For example, the regular expression `/a.+b/` will match the longest possible string that starts with "a" and ends with "b". However, the regular expression `/a.+?b/` will match the shortest possible string that starts with "a" and ends with "b".
Example:
Suppose you want to extract the text between the first occurrence of <h1>` and the first occurrence of `</h1>` in an HTML document. You can use the following regular expression:
`/<h1>(.*?)<\/h1>/`
The `.*?` in the regular expression specifies a lazy match, meaning that it will match the shortest possible string between the `<h1>` and `</h1>` tags.
const html = "<html><body><h1>Welcome to my website</h1><p>Here is some content.</p></body></html>";
const regex = /<h1>(.*?)<\/h1>/;
const match = html.match(regex);
console.log(match[1]); // Output: "Welcome to my website"

In the above example, the regular expression `/<h1>(.*?)<\/h1>/` matches the text "Welcome to my website" between the `<h1>` and `</h1>` tags in the given HTML document. The `.*?` in the regular expression specifies a lazy match, meaning that it will match the shortest possible string between the `<h1>` and `</h1>` tags. The parentheses in the regular expression capture the matched text.

### Boundaries

Boundaries are a way to match characters based on their position relative to other characters in the string. For example, the `^` character is an anchor that matches the beginning of a string, and the `$` character matches the end of a string. These can be useful for ensuring that a regex matches the entire string, rather than just a part of it.

There are also several boundary types that can be used to match specific positions within a string. Here are some examples:

* `\b` matches a word boundary, which is defined as the transition between a word character (e.g. a letter, digit, or underscore) and a non-word character (e.g. whitespace or punctuation).
* `\B` matches a non-word boundary, which is the opposite of a word boundary. It matches any position that is not a word boundary.
* `^` matches the beginning of a string or line.
* `$` matches the end of a string or line.
* `\A` matches the beginning of a string, even if it is not at the beginning of a line.
* `\Z` matches the end of a string, or the end of a line before any trailing newline character.
* `\z` matches the absolute end of a string.
Example using the word boundary `\b`:
const regex = /\bfoo\b/;
const str = 'foo bar baz';
console.log(regex.test(str)); // true

In this example, the regex will only match the exact word "foo", because it is surrounded by word boundaries.

### Back-references

A back-reference is a way to refer back to a previous capture group in a regex. This can be useful for matching repeated patterns, or for ensuring that two parts of a string match each other.

To create a back-reference, use a backslash followed by the number of the capture group you want to reference. For example, the regex `/(foo)bar\1/` will match the string "foobarfoo", because the `\1` back-reference matches the text captured by the first capture group, which is "foo".

Here is an example of using a back-reference to match repeated patterns:
const regex = /(\d{3})-\1/;
const str = '123-123 456-456 789-789';
console.log(regex.test(str)); // true

In this example, the regex will match any three-digit number followed by the same three-digit number, separated by a hyphen. The `\1` back-reference ensures that the second group matches the same text as the first group.

### Look-ahead and Look-behind

In some cases, you may want to match a pattern only if it is followed or preceded by a certain pattern, but without including that pattern in the actual match. This is where look-ahead and look-behind come into play.

Positive Look-Ahead
Positive look-ahead is denoted by `(?=pattern)` and matches the pattern that follows it only if it is followed by another pattern. For example, let's say we want to match all instances of the word "cat" only if it is followed by the word "in" but we don't want to include "in" in our match. We can use positive look-ahead to achieve this:
/cat(?= in)/
This regex will match "cat" only if it is immediately followed by "in". For example, it would match "cat in the hat" but not "cat on the mat".

Negative Look-Ahead
Negative look-ahead is denoted by (?!pattern) and matches the pattern that follows it only if it is not followed by another pattern. For example, let's say we want to match all instances of the word "cat" only if it is not followed by the word "in". We can use negative look-ahead to achieve this:
/cat(?! in)/
This regex will match "cat" only if it is not immediately followed by "in". For example, it would match "cat on the mat" but not "cat in the hat".

Positive Look-Behind
Positive look-behind is denoted by `(?<=pattern)` and matches the pattern that precedes it only if it is preceded by another pattern. For example, let's say we want to match all instances of the word "cat" only if it is preceded by the word "the" but we don't want to include "the" in our match. We can use positive look-behind to achieve this:
/(?<=the )cat/
This regex will match "cat" only if it is immediately preceded by "the". For example, it would match "the cat in the hat" but not "a cat on the mat".

Negative Look-Behind
Negative look-behind is denoted by `(?<!pattern)` and matches the pattern that precedes it only if it is not preceded by another pattern. For example, let's say we want to match all instances of the word "cat" only if it is not preceded by the word "the". We can use negative look-behind to achieve this:
/(?<!the )cat/
This regex will match "cat" only if it is not immediately preceded by "the". For example, it would match "a cat on the mat" but not "the cat in the hat".

## Author

Thank you for taking the time to read through this Tutorial, and I hope it was helpful in understanding Regexes, Specifically the `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` Regex. If you have any questions or feedback, feel free to contact me via my GitHub profile at https://github.com/Ervin543.
