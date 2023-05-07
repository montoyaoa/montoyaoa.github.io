---
layout: essay
type: essay
title: "Are you smarter than a StackOverflow user?"
# All dates must be YYYY-MM-DD format!
date: 2022-10-20
published: true
labels:
  - StackOverflow
  - Communication
---

[Has you really been far even as decided to use even go want to look more like?](https://www.youtube.com/watch?v=wqTpHhaKtL8)

An incomprehensible question can be frustrating and hard to read, much less pay attention to, isn't it? More likely than not, you skipped over the rest of the sentence once the first few words didn't make sense. It's an innate reaction to spare us from wasting precious brainpower on deciphering nonsense. It is therefore important for software engineers to understand what makes a "smart" question, and a "not-so-smart" question, which would be easily skipped just as you likely did before.

Because software engineers communicate primarily through text communications (well before COVID!), asking questions properly is an important communication skill to know. Additionally, one can take advantage of the knowledge of the global software development community. By approaching with a well-formed, coherent, and researched question, one shows respect for those answering the question, and minimizes confusing back-and-forth dialogue about what the actual question is.

## So, to begin, a "smart" question:

[What is the "-->" operator in C++?](https://stackoverflow.com/questions/1642028/what-is-the-operator-in-c)

The question text, verbatim:

>>After reading [Hidden Features and Dark Corners of C++/STL](http://groups.google.com/group/comp.lang.c++.moderated/msg/33f173780d58dd20) on `comp.lang.c++.moderated`, I was completely surprised that the following snippet compiled and worked in both Visual Studio 2008 and G++ 4.4.
>>
>>Here's the code:
>>
>>```
>>#include <stdio.h>
>>int main()
>>{
>>    int x = 10;
>>    while (x --> 0) // x goes to 0
>>    {
>>        printf("%d ", x);
>>    }
>>}
>>```
>>
>>Output:
>>
>>```
>>9 8 7 6 5 4 3 2 1 0
>>```
>>
>>I'd assume this is C, since it works in GCC as well. Where is this defined in the standard, and where has it come from?

This question provides:
- A source (with link) to the original source of this information
- The IDE and compiler used to verify the behavior
- A specific question (Where is this operator defined in the standard?)

The top answer respects the asker with a short, but useful reply. Verbatim:
>`-->` is not an operator. It is in fact two separate operators, `--` and `>`.
>
>The conditional's code decrements `x`, while returning `x`'s original (not decremented) value, and then compares the original value with `0` using the `>` operator.
>
>**To better understand, the statement could be written as follows:**
>
>```
>while( (x--) > 0 )
>```

This reply to the question results from the asker asking a direct question: "What is the `-->` operator and where is it defined?". The answerer identifies the misunderstanding (those are *two separate operators*), and corrects the asker by providing an example. There are 29 answers in total to the question, with none containing snarky, gruff, or rude replies. Indeed, some answers go into further technical detail on why decrementing was preferred on older hardware, and even joke about decrementing faster by making the "arrow" larger.

## Next, here's the "not-so-smart" question: 

[How the following goto stament is not returning error?](https://stackoverflow.com/questions/75190915/how-the-following-goto-stament-is-not-returning-error)

The question text, verbatim:

>[goto execution in gdb compiler](https://i.stack.imgur.com/MugrX.png)
>
>How the program flows. Here the i variable is not declared according to goto statement.

To summarize the issues with this question:
- Grammatical and spelling errors (English may not be the user's first language, but the question text is difficult to decipher regardless)
- There is no code in the body of the question
- Rather, the code is an imgur link to a screenshot of code and output!
- There is an extraneous line (line 13) which is not necessary to reproduce the problem.
- There is no description of the specific compilation or execution environment. I saw in the screenshot that the code was written on [GDB Online](https://www.onlinegdb.com/), but there is no further information available about the exact compiler or flags used. 
- I didn't notice this at first, but the question is tagged as both C and C++, but the asker does not specify which language the example code is written in. The screenshot does not include this information, either. With some trial and error I found that this code was written in C, as selecting C++ as the language in GDB Online causes a compilation error not shown in the screenshot.

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
>
>```
>#include <stdio.h>
>
>int main()
>{
>    goto a;
>    int i = 1;
>    a:
>    printf("i=%d", i);
>
>    return 0;
>}
>```
>
>When run on [GDB Online](https://www.onlinegdb.com/), using gcc 9.3.0 c99, the output is `i=0`.

When stated this way, the problem is easier to understand. The question was not about program *flow*, it was about an uninitialized variable. The example code is simplified and minimized to make the question clear. Full sentences with proper spelling and grammar are used, along with a specific question at the end. Information, such as the language and compiler are given. All of this serves to help quickly solve the problem.

The solution to this question, in fact, was hinted at by a commenter before the question was closed. The commenter stated that using an uninitialized variable was undefined behavior. Assuming I didn't know what that meant, plugging in `undefined behavior C` into Google returns the [cppreference page on undefined behavior](https://en.cppreference.com/w/c/language/behavior), which defines (emphasis added):

>undefined behavior - there are no restrictions on the behavior of the program. Examples of undefined behavior are memory accesses outside of array bounds, signed integer overflow, null pointer dereference, modification of the same scalar more than once in an expression without sequence points, access to an object through a pointer of a different type, etc. ***Compilers are not required to diagnose undefined behavior*** (although many simple situations are diagnosed), and the compiled program is not required to do anything meaningful.

And therefore, the answer to the question of "Why isn't the compiler catching my bad code?" is "Don't rely on the compiler to catch your bad code".

In summary, a "smart" question is one that respects the people reading and answering it. It is direct, provides minimal example code, and contains proper spelling and grammar. If the answer can be found through searching through documentation or Google, it is not asked at all. I feel that knowing this, and practicing Markdown, I can confidently ask questions as needed on StackOverflow without being flamed and downvoted to oblivion. 
