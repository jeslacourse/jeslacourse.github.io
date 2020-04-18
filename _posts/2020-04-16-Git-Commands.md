# Git Commands

This was originally part of a response to #151, but it should be good information for anyone trying to troubleshoot git version control. I've pulled some of the specific troubleshooting out and added a bunch of detail on the common commands. My hope is that it gives you guys a kind of understanding of what git is doing in the background. 

Pleeease be careful about just blindly typing in git commands. As safe as git version control is, you run a real risk of overwriting your files by just trying to `pull` simply when git asks you to. 

**Short version:**
`git clone url`: Asking the remote (online) repository to make a local (PC) copy
`git pull`: Including or "pulling down" changes from the remote repository to your local
`git status`: Looking at the differences between the remote and local. Awesome tool for troubleshooting. 
`git diff`: Shows changes between the remote file and the local
`git add`: Prep stage getting ready to add new files that are local but you want to be remote. This is also where git starts tracking files if you've heard that term before. 
`git commit`:  Takes the files to be updated to the remote repo, creates a "timestamp of sorts" and stages them to be included in the remote repo, i.e. you're committing the changes you've made up to a certain point. For us, this is usually just one commit (when we complete the file). 
`git push`: Updates the remote repository

**Git Pull**
So let's talk real quick about what `git pull` does, especially considering if you're pushing your changes  you likely have a complete project that shouldn't be altered much. `git pull` is pulling remote (online) changes down to your local (PC) repository. Disclaimer, I use Git Bash console for my commands, so RStudio will be slightly different, but the commands are the same.  For this class, we don't really `pull` assignments as much since we're simply using `git clone url` to create a local copy. ~~`git pull` is more effective in cases like #80 where there's been a revision.~~[For revisions see : #153] Assuming you've already cloned the file, `git pull` will "pull down" any changes made to the remote repository and include them in your local file. 

**Git Status and Diff**
But you've been working on your files before the changes were made remotely, right? Now you have a high risk of merge conflicts. Try out `git status` to see what files have changed. 

Mine looks like this: 
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'. # where your conflict is 
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   q1.Rmd
        modified:   q2.Rmd
        modified:   q3.Rmd

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .RData
        .Rhistory
        q1.html
        q2.html

no changes added to commit (use "git add" and/or "git commit -a")
```
The first few lines are telling me that I'm on the main branch (we won't talk about branches much here, so this won't change for the time being) and that my (local) branch, or copy of the repo, is up-to-date with the remote repository, called 'origin/master'. 

After that we start to see file status changes. I'm currently working on `q3.Rmd`, and haven't pushed any changes yet, so it's intuitive that my modified files would be the three `*.Rmd` files. 

If for some reason `status tells me that I'm `x commits behind master` I can look at the difference between my repo and the remote repo line-by-line with `git diff`. 

```
$ git diff 
diff --git a/q1.Rmd b/q1.Rmd 
index 5b76ee4..7dfe81a 100644  #commit references
--- a/q1.Rmd                   # remote file
+++ b/q1.Rmd                   # local file
@@ -1,5 +1,6 @@                # lines changes
 ---
 title: "Question 1"
+author: "Jessica LaCourse"
 ---

@@ -15,32 +16,75 @@ The `walk` function is very similar to the `map` function except that it doesn't
```
Here, `a/q1.Rmd` `b/q1.Rmd` are my remote and local files being compared, respectively. Values between the `@` symbols are line references and the `+` is a line, an author tag at the start of assignment 1,  I added to the start of the file. Intuitively, you can also have `-` changes for lines deleted. `git diff` is especially handy when you are working in a team and the remote repo is changing while you're working locally. 

**Git Add, Commit and Push** 
The local repository doesn't have a copy of `q1.html` or `q2.html` so I'll tell bash "Hey, when I push, I want to push these files, too" with the command `git add q1.html q2.html` (and ultimately q3 as well).  

I've added my files, now I want to commit them, `git commit -m "Complete Assignments"`, where `-m` is called a flag saying "I want to include the message, 'Complete assignment'". 

From there, I can push my changes, `git push origin master`.

Once I push my changes, all five files (three `*.Rmd`s and two `*.htmls` will push to the local repository. 

**So why are `git add`, `git commit`, and `git push` three different commands?** 
It could be one right? 

The first, I hope it's a bit intuitive as to why `git add` is it's own command. You don't necessarily want to add ALL the files in a folder to the remote repo. There is a command, use it wisely, to add all new files `git add .` Similarly, to add all changes, added and deleted files, etc. There's `git add -A` where dot and `-A` respectively are flags for "all new" and "all" changes.  

I'm not the only one whose committed a file, gotten the message that it was successful, then... it's not there. It's not where it's supposed to be! Why isn't my file online? 
There's some nuance in the difference between `git commit` and `git push`. The way I think of it is that `git commit` is kind of like putting a bookmark in my book, while `git push` is talking about the latest changes (between this time and the last time I dropped a bookmark in my book) with a(n obviously Zoom) book club or something larger than myself. Does that make sense? `commit` logs changes locally, while `push` updates our remote repository with our changes. 

For this class, we only `commit` and `push` once, usually. But when you're working on a larger project you can absolutely `commit` and `push` to a repo dozens or hundreds of times. 

Edit: Formatting, added `git diff` information
