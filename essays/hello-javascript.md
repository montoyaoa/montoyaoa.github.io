---
layout: essay
type: essay
title: "Hello JavaScript!"
# All dates must be YYYY-MM-DD format!
date: 2022-01-16
published: true
labels:
  - Javascript
---

I've been looking forward to this.

I've only used JavaScript last year, when working with Node-RED to build IoT devices. However, Node-RED is a very friendly, "drag-and-drop" style interface. I didn't feel like I gained any appreciable experience with JavaScript, so I would say that I'm starting fresh this semester. 

Having completed the Basic JavaScript portion of freeCodeCamp's JavaScript Algorithms and Data Structures course, I feel I have gained a little more familiarity with JavaScript. Coming from the Computer Engineering curriculum, which is all taught in C and C++, a big shift for me was the weak typing of JavaScript. Thinking about the differences I've experienced so far:
- Function parameters are typeless, meaning I may have to preform extra checks on passed in arguments for validity
- It is possible for a variable to have different type, not just value. For instance:
```
function testFunction(a) {
	let foo;
  if (a) {
  	foo = "bar";
  } else {
  	foo = 3;
  }
  return foo;
}
```
I could imagine both some useful simplification of code as a result, as well as annoying debugging if used improperly.
- I appreciate not having to implement the small details of arrays. Pushing/popping and determining length are the most common intermediate tasks I need to do. No point doing them over and over. 

I feel optimistic about this class. In particular, I'm looking forward to learning more about web development, which is something I haven't learned much about before.
