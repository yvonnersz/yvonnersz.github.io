---
layout: post
title:      "Git Etiquette"
date:       2021-02-09 21:41:00 +0000
permalink:  git_etiquette
categories: git
tags: git, message
# image: /assets/article_images/2014-11-30-mediator_features/night-track.JPG
# image2: /assets/article_images/2014-11-30-mediator_features/night-track-mobile.JPG
---


Why do we need to add messages to our commits? It is easy to not give a great deal or thought to the messages added to commit our code onto GitHub. But a git commit message is the best way to communicate a change to your future self and also other developers that are working on the same project.

> It can be hard to understand why you made some changes in the past. Commit messages can adequately communicate why a change was made, and understanding that makes development and collaboration more efficient. This is even more important when your project grows or people move on. Knowledge is power and as developers, we need to know why things may have been done in a certain way. Git log should be your answers.

While our code should be self-documenting, the git commit logs should explain what was done and when. So how do we set up our git commit messages to make it easier for our future self and other developers?

## Rules of Great Commit Messages

Commit messages should describe what was changed and why it was changed.

According to Chris Beam, here are the seven rules of a great Git commit message:

1. Separate subject from body with a blank line
2. Limit the subject line to 50 characters
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Wrap the body at 72 characters
7. Use the body to explain what and why vs. how

### Separate subject and body with a blank line

Until now, I didn't even know that you can have a subject and body when it came to git commits. However, not every commit requires a subject and a body. 

Sometimes a single line is fine, especially when the change is simple that needs no further context. For example:

> Fix typo in introduction to user guide

For commit messages that do require a body, using the -m option would not be ideal. It would be better writing the message in a proper text editor.

### Subject line should be short, capitalized, and have no punctuation

Rules 2, 3, and 4 can be grouped together and is pretty self-explanatory.

Also, 50 characters is not a hard limit but just a rule of thumb. 

> Keeping subject lines at this length ensures that they are readable, and forces the author to think for a moment about the most concise way to explain what’s going on.

### Use the imperative mood in the subject line

Imperative mood just means “spoken or written as if giving a command or instruction”. 

A few imperatives that can be used:

- Refactor
- Update
- Remove
- Release

### Limit body to explain what & why

Documentation is ALWAYS important. By using the body to explain the what and why, the author is saving future self and developers a lot of time. Without the body message, the context would be lost forever.

Code is generally self-explanatory so focus on the reasons why you made the change in the first place.
- Document the way things worked before the change and the issues that came up
- The way it works now and why you decided to take this route to solve the issue

Hope this helps,
Yvonne