Before you can answer "What is Github?", you must first answer "What is Git?".

Git is a distributed revision control and source code management system with an emphasis on speed. Git was initially designed and developed by Linus Torvalds for Linux kernel development in 2005.

Basically, Git provides a mechanism for multiple people to work on different offline copies of the same code project, and then (relatively) easily merge the two copies of the project together at a later point in time.

The Git server (in addition to many client-side implementations of Git) is open source and anyone can run their own Git server and Git repositories for free.

Github, on the other hand, is simply a company that provides Git hosting. They handle all the server-side stuff and provide a nice web interface. This makes it easier for people around the world to just focus on their code projects (instead of worrying about server administration).

Github hosts public repositories for free, which means they are a great place to put an open source project. This friendliness towards the open source community has greatly increased the popularity and adoption of Github over the years.

GIT is a form of tracking changes to your code.

> You are working on a paper. You write five paragraphs. Then your friend comes along later, and writes another five paragraphs. Then you edit a few paragraphs, and your friend edits a few more paragraphs.

At the end of it, there are some issues, but its hard to coordinate who edited what and when.

With a system like GIT, you would first create the file on the GIT server, and add your changes. Then, you commit those changes to the repository, which will basically say 'Hey, this file exists and looks like this.'

Then, your friend checks out that repo, pulling the latest changes. He adds some stuff, then commits to the repo. The repo says 'Hey, this file exists and is different from the previous version, so we will save it as version 2.'

GITHUB is just a website that works using GIT that has a lot of code. Most of it is opensource, and the idea there is that if you wanted to add some paragraphs from someone on GITHUB, you would just check out their GIT repository and add it to your document, more or less.

Git is a source control system. It allows you to track changes to code files down to the exact line and characters changed. Imagine you got a school project working after hours of coding. Then, you need to add a feature that will change some existing code. You're scared to mess your program up, so you copy all of the code to another folder, making your new feature changes to the original copy. Git solves this by allowing you to have different "copies" of your source files (called branches) without actually copying the files. It does this by keeping a history of all changes (called commits) and the order they occurred in, so you can rewind, undo, or even develop two features in parallel without them affecting each other.

Github allows you to host it on their platform and adds a nice GUI as well as features for collaborating with other users on the same repo (like Pull Requests). Repos on Github can be private or public, so you can use it for publishing to the world (and getting strangers to collaborate with you!) or keep it private it and use it for your company/personal projects.
