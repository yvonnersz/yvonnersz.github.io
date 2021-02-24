What is the difference between fork, clone, and pull on GitHub?

> Forking is done on GitHub while Cloning is done using Git. When you fork a repository, you create a copy of the original repository (upstream repository) but the repository remains on your GitHub account. Whereas, when you clone a repository, the repository is copied on to your local machine with the help of Git.

> Changes made to the forked repository can be merged with the original repository via a pull request. Pull request knocks the repository owner and tell that “I have made some changes, please merge these changes to your repository if you like it”. 

Now imagine today: When I start a new project, I create a repo and everyone can clone it, modify it locally and ask me to push so that I need to give you write access to my repo on Github. I don't want that except for people I trust. So what is the other way when you want to contribute occasionally ?

You fork my repo (technically it's just a clone on the Github server in your profile area and you have the permission to push on it). Then you clone it locally, then make your modifications and push them to your fork. After that, you ask me to pull your changes in my repo: It's a "pull request". As you, I have a local clone of my project (the original you forked) but with write permissions. As Git is distributed, I can add your repo as a remote and pull your commits. If I'm happy with that, I merge your commits and push them on the original commit. You are an "occasional" contributor and I didn't need to give you write access to get your contribution.

> For the sake of simplicity, we can consider a fork to be a personal copy of the repository that can be edited by you even when you cannot edit the original repository. Creating a fork on GitHub is as easy as clicking the “fork” button on the repository page.

