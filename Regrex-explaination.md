# REGEX: AKA REGULAR EXPRESSION

A regular expression (regex) is a sequence of characters that defines a search pattern. It is a powerful tool for text manipulation, used to match and search for patterns within strings of text. With its concise syntax and versatile functionality, regex is widely used in programming, data analysis, and other fields where text processing is necessary.

## Summary

In order to determine a valid URL, a URL matching regex can be used. An example of a regex pattern that matches URLs with the HTTP or HTTPS protocol, domain names containing alphanumeric characters and hyphens, and a path that may contain alphanumeric characters, hyphens, underscores, or forward slashes:

 /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/


Lets break these down a bit more to understand the a few of the components considered using a regex:

- Protocol: This component specifies the type of protocol used for the URL, such as HTTP, HTTPS, FTP, etc.

- Domain name: This component specifies the domain name or IP address of the website, such as example.com or 192.168.1.1.

- Path: This component specifies the path to the resource on the server, such as /blog/post/123.

- Query string: This component specifies any additional parameters passed in the URL, such as ?page=2&sort=asc.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)


## Regex Components

### Anchors

As a regular expressions, "anchors" are used to specify the start and end points of a string. Anchors help ensure that the regular expression only matches the intended pattern and are not apart of a larger string. When matching a URL, anchors can be used to specify that it should only match URLs that begin and end with specific characters.

The two most common anchors used when matching a URL are ^ and $. The caret is used to indicate the start of a string, while the dollar sign is used to indicate the end of a string.

Here's an example of how anchors can be used to match URLs that begin with "http://" or "https://" and end with a valid top-level domain (e.g. ".com", ".org", ".edu", etc.):

```text
^(http|https):\/\/[a-zA-Z0-9]+\.[a-zA-Z]{2,}(\/\S*)?$
```

### Quantifiers

Quantifiers in this instance are used to specify how many times a particular pattern should be matched. Quantifiers help to make regular expressions more flexible by allowing for variations in the number of characters or sequences of characters that can be matched.

When matching a URL, quantifiers can be used to specify the number of occurrences of certain characters or character classes that are expected to be found in the URL. Here are some commonly used quantifiers when matching URLs:

```text
- * (0 or more occurrences): This quantifier indicates that the preceding character or group may appear 0 or more times. For example, a* would match zero or more occurrences of the letter "a".

- + (1 or more occurrences): This quantifier indicates that the preceding character or group must appear at least once. For example, a+ would match one or more occurrences of the letter "a".

- ? (0 or 1 occurrences): This quantifier indicates that the preceding character or group may appear zero or one time. For example, a? would match zero or one occurrences of the letter "a".

- {n} (exactly n occurrences): This quantifier indicates that the preceding character or group must appear exactly n times. For example, a{3} would match exactly three occurrences of the letter "a".

- {n,} (n or more occurrences): This quantifier indicates that the preceding character or group must appear at least n times. For example, a{2,} would match two or more occurrences of the letter "a".

- {n,m} (between n and m occurrences): This quantifier indicates that the preceding character or group must appear at least n times, but no more than m times. For example, a{2,4} would match between two and four occurrences of the letter "a".
````

```text
Example of quantifiers used in to match urls:

^(http|https):\/\/[a-zA-Z0-9]+\.[a-zA-Z]{2,}(\/\S*)*$
```

### OR Operator

The OR Operator is denoted by the "|" - side note: this is my favorite to use for readability - back to our regular scheduled information: 

The OR operator can be useful when matching URLs that have different possible schemes (e.g. http or https) or different possible top-level domains (e.g. .com, .org, or .edu). Using the OR operator can make regular expressions more flexible and allow them to match a wider range of URLs that have different possible variations.

```text
Examples:
^(http|https):\/\/[a-zA-Z0-9]+\.[a-zA-Z]{2,}(\/\S*)?$

^https?:\/\/[a-zA-Z0-9]+\.(com|org|edu)(\/\S*)?$
```

### Character Classes
In general character classes are used to match a set of characters, as the name suggests. Used in a URL patter - it is used to match characters that are common to appear in specific parts of the URL. 

The most common example of this would be the "." This is often used to match the dot in the top-level domain (e.g. ".com"). Some other common character classes are the "+" , used after the character class indicates that one or more occurrences of the character class should be matched. The "=" and "&" characters are matched literally, while the () and ? characters are used for grouping and optional matching, respectively.

```text
Example:
^(http|https):\/\/[a-zA-Z0-9]+\.[a-zA-Z]{2,}(\/[\w-]+)*(\?([\w%]+=[\w%]+)(&([\w%]+=[\w%]+))*)?$
```

### Flags
Flags are used to modify the behavior of the regular expression pattern. Flags can also be used to perform case-insensitive matching, global matching, etc.

Commonly used flags are: 

```text
- i: Performs case-insensitive matching.
- g: Performs global matching (i.e. finds all matches rather than stopping after the first match).
- m: Performs multi-line matching (i.e. treats each line of the input string as a separate string).
```

```text
Example:
/^(https?):\/\/([a-z0-9-]+\.)+[a-z]{2,}(\/[\w.-]*)*(\?[\w%&=]*)?$/ig
```

### Grouping and Capturing

This refers to refers to the ability to group parts of the pattern together and capture the matched text. Grouping and capturing can be useful for extracting specific parts of a matched string. Specifically it can be used to find the scheme, domain, path, and query parameters of a URL, many mentioned above in my summary. 

```text
Example:
/^(https?):\/\/([a-z0-9-]+\.)+([a-z]{2,})(\/[\w.-]*)*(\?([\w%]+=[\w%]+)(&([\w%]+=[\w%]+))*)?$/i

// Group 1: Scheme (e.g. http or https)
// Group 2: Domain (e.g. example.com)
// Group 3: Top-level domain (e.g. com)
// Group 4: Path (e.g. /path/to/page.html)
// Group 5: Query string (e.g. ?param1=value1&param2=value2)
```

### Bracket Expressions

Bracket expressions have been defined in mutiple ways, some group bracket expressions with character classes, others refer to this as the expression between the brackets like seen above:

```text
Example:
[a-z0-9]
[a-z]
[\w.-]
```

### Greedy and Lazy Match
Separating them out: Greedy Matching refers to matching as many characters as possible, often combining domain and subdomian as one group. Lazy Matching matching as few of characters as possible. This is used to match specific parts of a url, such as wanting to match a domain name but not a path.

```text
Examples:
/^https?:\/\/[a-z0-9-]+(\.[a-z]{2,})+/i

// Greedy matching: Matches the entire domain name (e.g. example.com) as one group.

/^https?:\/\/[a-z0-9-]+(\.[a-z]{2,})+?/i

// Lazy matching: Matches each level of the domain name (e.g. example and com) as separate groups.

```

## Author

This research was done using the following resources available in 2023. As provided by my school, UC Berkeley: https://www.youtube.com/watch?v=7DG3kCDx53c , https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial , https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial . Along with this information I used tutorials from github user: Shilohjones194 who wrote an informative paper here: https://gist.github.com/Shilohjones194/474bca145fc361bd9ec6d8c4d3bf71ae . 

As a disclaimer, Open AI's tool Chat GPT was used as a tool to understand and research this topic. As a student and tech enthusist, I encourage you to also use the tools available to you to better yoru understanding of the world around you. 

Maislinn Helfer | Github @maislinn
