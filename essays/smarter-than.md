---
layout: essay
type: essay
title: "Are you smarter than a StackOverflow user?"
# All dates must be YYYY-MM-DD format!
date: 2016-02-06
published: false
labels:
  - Engineering
---

So, to begin, here's the "not-so-smart" question: [How the following goto stament is not returning error?](https://stackoverflow.com/questions/75190915/how-the-following-goto-stament-is-not-returning-error)

The question text, verbatim:

[goto execution in gdb compiler](https://i.stack.imgur.com/MugrX.png)

How the program flows. Here the i variable is not declared according to goto statement.

To summarize the issues with this question:
- Grammatical and spelling errors (English may not be the user's first language, but the question text is difficult to decipher regardless)
- There is no code in the body of the question
- Rather, the code is an imgur link to a screenshot of code and output!
- Ther is an extraneous line (line 13) which is not necessary to reproduce the problem.
- There is no description of the specific compilation or execution enviornment. I saw in the screenshot that the code was written on [GDB Online](https://www.onlinegdb.com/), but there is no further information available about the exact compiler or flags used. 
- I didn't notice this at first, but the question is tagged as both C and C++. They are distinct languages, and a program must be written in either one or the other. This code was written as C code, as selecting C++ as the language in GDB Online causes a compilation error not shown in the screenshot.

Searching the [FAQs for GDB Online](https://www.onlinegdb.com/faq) shows the compiler used is gcc 9.3.0 c99 for C.
Now, we can combine this information into a "smart" question, by being more clear about what the question is, and providing as much information as necessary.

Title: Why does an uninitialized variable 
Tags: C

Hello, I am not sure I understand the flow of Below is a program that reproduces this error. 
```
#include <stdio.h>

int main()
{
    goto a;
    int i = 1 > 5 ? 2:3;
    a:
    printf("i=%d", i);

    return 0;
}
```
When run on [GDB Online](https://www.onlinegdb.com/), using gcc 9.3.0 c99, the output is
```
i=0
```
