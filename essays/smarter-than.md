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

>[goto execution in gdb compiler](https://i.stack.imgur.com/MugrX.png)
>
>How the program flows. Here the i variable is not declared according to goto statement.

To summarize the issues with this question:
- Grammatical and spelling errors (English may not be the user's first language, but the question text is difficult to decipher regardless)
- There is no code in the body of the question
- Rather, the code is an imgur link to a screenshot of code and output!
- Ther is an extraneous line (line 13) which is not necessary to reproduce the problem.
- There is no description of the specific compilation or execution enviornment. I saw in the screenshot that the code was written on [GDB Online](https://www.onlinegdb.com/), but there is no further information available about the exact compiler or flags used. 
- I didn't notice this at first, but the question is tagged as both C and C++. They are distinct languages, and a program must be written in either one or the other. This code was written as C code, as selecting C++ as the language in GDB Online causes a compilation error not shown in the screenshot.

The issues with this question are stated in the replies to this problem. The few replies merely inform the asker that they did not include the code as text and did not specify the language or compiler. The question was up on StackOverflow for a total of eight minutes before being marked as closed, being removed entirely for moderation shortly thereafter.

Searching the [FAQs for GDB Online](https://www.onlinegdb.com/faq) shows the compiler used is gcc 9.3.0 c99 for C.
Now, we can combine this information into a "smart" question, by being more clear about what the question is, and providing as much information as necessary.

>Title: gcc 9.30 c99 - Uninitialized variable has a default value
>
>Tags: C
>
>Hello, I have found that gcc 9.30 c99 does not flag referencing an integer that has not been initialized as an error. In fact, the integer is returned with a value of 0. Is this expected behavior for gcc?
>
>Below is a program that reproduces this error. 
```
#include <stdio.h>

int main()
{
    goto a;
    int i = 1;
    a:
    printf("i=%d", i);

    return 0;
}
```
>When run on [GDB Online](https://www.onlinegdb.com/), using gcc 9.3.0 c99, the output is `i=0`.

When stated this way, the problem is easier to understand. The question was not about program *flow*, it was about an uninitialized variable. The example code is simplified and minimized to make the question clear. Full sentences with proper spelling and grammar are used, along with a specific question at the end. Information, such as the language and compiler are given. All of this serves to help quickly solve the problem.

The solution to this question, in fact, was hinted at by a commenter before the question was closed. The commenter stated that using an unintialized variable was undefined behavior. Assuming I didn't know what that meant, plugging in `undefined behavior C` into Google returns the [cppreference page on undefined behavior](https://en.cppreference.com/w/c/language/behavior), which defines (emphasis added):

>undefined behavior - there are no restrictions on the behavior of the program. Examples of undefined behavior are memory accesses outside of array bounds, signed integer overflow, null pointer dereference, modification of the same scalar more than once in an expression without sequence points, access to an object through a pointer of a different type, etc. ***Compilers are not required to diagnose undefined behavior*** (although many simple situations are diagnosed), and the compiled program is not required to do anything meaningful.

And therefore, the answer to the question of "Why isn't the compiler catching my bad code?" is "Don't rely on the compiler to catch your bad code".
