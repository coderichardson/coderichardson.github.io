---
title: "Regular Expressions (Regex) for Beginners"
date: 2023-09-17 21:39:00 +0000
tags:
  - "regex"
---

![](/assets/img/posts/regular-expressions-regex-for-beginners/01.jpeg)
Regular expressions (regex) are used to to extract information or patterns from text. They are used by programming languages, AV/EDR software, application whitelisting software, data loss prevention (DLP) software, personally identifiable information scanning software, and more. While simple in concept, regex can become quite complex depending on what strings of text need to be extracted.

I'll be using [regex101.com](http://regex101.com) to show my examples, but there are a ton of great resources and "testers" available for free on the Internet.

*Tokens* are how regular expressions are defined. There are dozens available, and we'll get to them in a minute, but nothing is more basic in regex than just typing the exact string you're looking for.

## Example 1 - string

If you're searching for the string "fire" in a given sentence, you would make your regular expression fire.

![](/assets/img/posts/regular-expressions-regex-for-beginners/02.png)
We can see here that this regex pattern patches on lines "fire", "firetruck", "fireman", and "the house is on fire." This type of matching can be done with any character -- numbers, letters, special characters, etc.

## Example 2 - ^, $

Next, we'll introduce some of those tokens were discussed earlier. The most basic of these are **^** and **$**.

^ = without any other context, indicates the beginning of the desired string

![](/assets/img/posts/regular-expressions-regex-for-beginners/03.png)
^fire matches against "fire", "firetruck", and "fireman", but does not match "The house is on fire" because the sentence does not start with the word "fire". Note that "Fire" would also not match as regex is case-sensitive in this context.

$ = without any other context, indicates the end of the desired string.

![](/assets/img/posts/regular-expressions-regex-for-beginners/04.png)
fire$ matches against "fire", "The house is on fire", and "test-fire" because all of these end with the string "fire".

## Example 3 - [a-z]

[a-z] matches any character in the given range.

![](/assets/img/posts/regular-expressions-regex-for-beginners/05.png)
Imagine you are given a large number of files containing only text and you want to know which files contain hex. One way to do this is to look for characters g through z or their uppercase counterparts. This is because hex numbers are 0-9 and A-F.

With the regex [g-zG-Z] we can find any text that contains characters g through z or the uppercase counterparts.

This is why we match on both lines in our example as they contain non-hex characters. In this case, we would know that the file is at least not all hexadecimal. To ensure a given block of text contains just hexadecimal numbers we would want to try something such as [0-9a-zA-Z].

## Other Popular Tokens

\d = any digit

\D = any character besides a digit

\s = any whitespace character (space, tab, or newline)

\w = any letter, number, or underscore

\b = boundary character (boundary for work characters)

\ = escape character that tells regex the following character should be interpreted literally

+ = one or more of the preceding character

. = any single character

## Example 4 - Phone Numbers

Let's try to find some phone numbers. Depending on where you live in the world, you phone number may be formatted differently. I'm going to assume a phone number format of "(123) 456-7890". Space included and country code (+1) excluded.

My first thoughts are that I'm going to need to match on:

- exactly the opening and closing parenthesis
- the space between the area code and the rest of the phone number
- the dash in the middle of the phone number

So I'll try a regex of (\d\d\d) \d\d\d-\d\d\d\d.

![](/assets/img/posts/regular-expressions-regex-for-beginners/06.png)
As we can see, that doesn't match our example of (123) 456-7890.

![](/assets/img/posts/regular-expressions-regex-for-beginners/07.png)
This is because (...) is actually another token known as a Capture Group. By adding \ before the opening and closed parenthesis we tell regex to interpret the characters literally instead of as a Capture Group. Once this is done we can see our phone number matches no problem.

## Conclusion

Hopefully this gives an overview of some of the most common regex expressions and provides some examples of how they may be used. As I said earlier, regex can become very complex. To give you an idea, I wanted to provide a few examples I found on [variables.sh](https://www.variables.sh/complex-regular-expression-examples/):

Matching a Phone Number Regardless of How It's Formatted:

/^\+?(\d[\d-. ]+)?(\([\d-. ]+\))?[\d-. ]+\d$/

Matching an Email Address:

/(?:[a-z0-9!#$%&'\*+/=?^\_`{|}~-]+(?:\.[a-z0-9!#$%&'\*+/=?^\_`{|}~-]+)\*|"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])\*")@(?:(?:[a-z0-9](?:[a-z0-9-]\*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]\*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]\*[a-z0-9]:(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21-\x5a\x53-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])+)\])/i

Matching a Date Regardless of How It's Formatted:

/^(?:(?:31(\/|-|\.)(?:0?[13578]|1[02]))\1|(?:(?:29|30)(\/|-|\.)(?:0?[13-9]|1[0-2])\2))(?:(?:1[6-9]|[2-9]\d)?\d{2})$|^(?:29(\/|-|\.)0?2\3(?:(?:(?:1[6-9]|[2-9]\d)?(?:0[48]|[2468][048]|[13579][26])|(?:(?:16|[2468][048]|[3579][26])00))))$|^(?:0?[1-9]|1\d|2[0-8])(\/|-|\.)(?:(?:0?[1-9])|(?:1[0-2]))\4(?:(?:1[6-9]|[2-9]\d)?\d{2})$/

See? I wasn't kidding. And clearly whoever wrote these does regex more than me! For more of these, examples, and explanations for some of the expressions, I'd encourage you to visit the site linked above.

## Additional Resources

Some other great regex resources I wanted to mention here

- [RegexOne](https://regexone.com/): interactive lessons covering most tokens and general usage in regex.
- [RegExr](https://regexr.com/): another regex tester I've used in the past that provides real-time explanations of the regular expressions entered.