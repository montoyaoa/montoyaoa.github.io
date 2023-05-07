---
layout: essay
type: essay
title: "Keeping track of spaces"
# All dates must be YYYY-MM-DD format!
date: 2023-02-08
published: false
labels:
  - Javascript
---

I had figured there was some way of enforcing code standards, but I didn't know much about how it was implemented. In the overwhelming majority of the code I have written, I just wrote what worked, without worrying about tabs, spaces, or where the curly brace is. I recognize then and now that that isn't a good idea for code I intend to share with others.

After trying ESLint to enforce Javascript coding standards, I feel that I can more easily write code with a consistent syntax. To me, it's easy now that I know useful keyboard shortcuts: `F2` for moving to the next suggestion, and `Alt + Shift + Enter` to take the suggested corrective action. By doing so, I feel confident that I can achieve the green checkmark easily.

Something I've noticed that is missing from the linting is the recommendation to convert inline functinos to anonymous functions. This is particularly useful for inline functions, like an Underscore call:
```
    return _.map(inputArray, function(num) { return num * num; });
```
Which can be written as
```
    return _.map(inputArray, (num) => num * num);
```
I'm not sure if that's a setting I don't have enabled, but I don't see that sort of suggestion, which is helpful to me as I learn Javascript.

To conclude, I'll include a link to a clip from Silicon Valley that epitomizes the concern about code standards. I don't think anyone takes the difference between tabs and spaces that seriously, but this did reflect my views on code standards prior to learning about linting.

<iframe width="560" height="315" src="https://www.youtube.com/embed/SsoOG6ZeyUI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>