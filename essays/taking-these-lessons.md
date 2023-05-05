---
layout: essay
type: essay
title: "Taking these lessons forward"
# All dates must be YYYY-MM-DD format!
date: 2023-05-04
published: true
labels:
  - Software Engineering
  - Coding Standards
  - Agile
---

As I'm wrapping up my work in ICS 314, I can take several lessons with me into my future coding work. My particular interest is embedded systems, where compact, efficient code is necessary. To that end, my experience in ICS 314 has helped me learn new skills and concepts to be a better engineer in those projects. 

Even though this is separate from web development, the coding concepts still carry. I will be continuing on to a Master's in Electrical Engineering and continuing my VIP project called [Ke Ao](https://www.teamlaniakea.com/), a CubeSat. I was the Software team lead this semester, and I have seen many ideas that could help us provide better code. 

## Coding Standards

Something that I've gained more experience with is linting and using consistent coding standards. Truthfully, I hadn't given much thought to how many spaces are in a tab, and other "decorative" elements of code. But I've seen that enforcing those rules does make the code more readable, especially once your eye "knows" where everything should be.

IDE-integrated linting through IntelliJ IDEA made using linting really easy once it's set up. I'll have to look into doing the same using VSCode for my next coding work with Ke Ao. The code for that project is all C++, so I'm sure I can find some good linting standards and programs for that purpose. 

## Agile Project Management

I hadn't given much though to how projects should be organized. In most of my experiences with group work, especially in classwork, I usually take a leadership role and tell people what to do. I *really*, *really*, tried to avoid doing this for the ICS 314 project. The use of a more decentralized approach did take a lot of pressure off of me to create and assign tasks to people based on their skills.

I had heard of Agile before, but haven't used it in practice. In theory, both Ke Ao and my internship used Agile, but my internship used a heavily modified version without sprints or milestones and Ke Ao didn't use it much this semester. 

I think that for code projects, Agile works best when managing many tasks that can be done independently by people of similar skill levels. It breaks down when there is a large gulf between skill levels, or if the code is heavily bottlenecked and sequential in nature. I tried to apply some of Agile this semester with the Ke Ao Software team, but lack of familiarity with the codebase and documentation systems meant that we didn't have much time to work after we came up to speed. That's something that I'd need to suggest improvements on in the future. More likely than not, new Software team members should have a smooth onboarding. That's the goal, at least.

## Deployment and Documentation
Something that has been critical this semester was using GitHub Actions to automatically deploy code, and GitHub Pages to host a website. I didn't know that was possible. I suggested then implemented Doxygen documentation for the Ke Ao codebase, hosted on a public GitHub Pages page. This is a really neat feature, and a great onboarding tool for new students.

I would like to eventually automate the generation and updating of this code. As of now, the Doxygen output has to be manually generated from the latest main branch. I'd imagine that there could be some way to update the "documentation" repo from the "source" repo, and redeploy the updated Doxygen HTML to match the latest changes to the code. That's definitely something to look into.

EDIT: I asked my friend ChatGPT to see if there is a way to automate this using GitHub Actions. It is absolutely possible, and it gave me a useful script to automate Doxygen HTML generation. I will implement this and save future students one more step in the development process.

## Where to go from here
I think I can confidently say I've learned a lot about more than just web development from ICS 314. I've learned valuable skills in software engineering that makes the code that I produce and the teams I am a member of better. I look forward to apply them in my career.

