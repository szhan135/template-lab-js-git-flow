# GitHub Flow

> Author(s): Brian Crites ([@brrcrites](https://github.com/brrcrites))

Many [git workflows](https://www.endpoint.com/blog/2014/05/02/git-workflows-that-work) exist today and they all have their pros and cons. However, GitHub flow is one of the simplest to learn and is our preferred method for this course. A brief overview of GitHub flow is found in the diagram below.

<img src="images/github-flow.png?raw=true" width="1000">

Source: [GitHub Guides](https://guides.github.com/introduction/flow/)

The goal of this lab is to get you more comfortable using Git and GitHub when working on a team. For this lab you will be playing the part both partners in a two person group so you can see what it is like from both sides of working on a collaborative project. By the end of this lab you should be familiar with the following:

* Create issues to manage development tasks
* Use branches to reduce conflicts and keep your code in good working order
* Using pull requests to review and merge changes in a predictable manner
* Tackle merge conflicts
* Semantically tag versioned releases
* Revert bad commits

> Note: please wait to clone this repository until instructed to later in this README

## Tracking Work Through Issues

The first thing we are going to do is use [Trello](https://trello.com) to create development tasks (often referred to as issues in the GitHub parlance) so they can be more easily tracked, assigned, and managed. A large portion of the overhead associated with the actual development process is keeping track of who should be working on what features when, and issues (which are generally also used to track features, user stories, bugs, taking out the trash, etc.) are a great way to annotate and track different development tasks over the lifetime of a project. In many tools this type of tracking will also let you automatically create useful burndown charts for seeing where tasks are getting stuck in your process (although with the quick and process light systems you will use in this course, this feature will probably remain largely unused).

Start by creating a new Trello account if you don't already have one (you'll use this same account for the rest of the course). From there, create a new board for this lab named "GitHub Flow Lab" which you will use to track the (small number of) issues that you'll create for this lab. Then create three columns in your board for "Backlog", "In Progress", and "Done". The "Backlog" will hold all the tasks which you've yet to complete, while "In Progress" will be the ones you are currently working on and "Done" will be the ones you've finished. Once you have created the board you'll create the development issues for this lab. When creating a Trello issue you should consider the following:

* Text: when you create a new card it requires some initial text which is typically a short description of the development task, this is the only thing you can enter when creating a new card
* Description: once you've created a card you can add a description, which is where you should put any additional details necessary for that issue
* Members: you can assign the card to be completed by a specific person, which can be useful when using these cards in conjunction with Scrum or Kanban
* Labels: teams often use labels to descibe what category of work this issue belongs to, making it easier to know what type of work will need to be completed for that issue

For this lab you should create the following issues (we only list the titles and descriptions here):

* Create fizzbuzz file: implement a file which prints 1 to 100 replacing the values divisible by 4 with fizz and the values divisible by 6 with buzz
* Functionalize fizzbuzz: the fizzbuzz functionality is hard to use as inline code, it needs to be converted into a function for easier usage
* Additional Bool Functionality; add the ability to print "bool" when the number is divisible by 5

There is some more detail that we'll go into for each of these issues but that is pretty typical as issues will rarely go into all the detail necessary to implement them in code. We will go into additional detail when we get to impleemnting each issue later in this lab.

## Effective Branching

In the Git lab, you learned that branching is used when developers want to change code without having to deal with conflicts between other contributors. When working on a team, it is wise to separate what each person is working on (and often each feature that person is working on) by making a branch unique to that change or set of changes. When that team member finishes their part, they can then merge back into the master or main development branch to signify that it is complete and should be part of the code everyone uses moving forward.

> Note: You should refer back to the links we provided in the git lab for creating good commit messages, however these are not the only good methods for commit messages. Lots of organizations have requirements on commit messages as they do reviews and style. Some of these try and categorize the commits such as the [gitmoji](https://gitmoji.carloscuesta.me/) system.

You should prepend your branch with your username to make it easy to see who owns which branch and to avoid naming conflicts between individual contributors branches. After you have each created your individual branch, **it is very important** that you change to that branch with `git checkout <branch-name>`

### Your First Branch

For this exercise we will create a program to solve one of the most used basic interview questions, commonly known as "fizzbuzz". This problem is usually used to screen candidates for basic programming skills and while there are a lot of different varitions it generally goes something like this.

> Create a program that prints the numbers between 0 and 100 but replacing every value divisible by 4 with the word "fizz", every value divisible by 6 with the word "buzz", and every value evenly divisible by both 4 and 6 with the word "fizzbuzz".

Start by creating a new branch named `<github-username>/fizzbuzz` and switch to that branch to create your program. Write a solution to the problem (committing when appropriate) and when you are done (and after making at least one commit) you should `git push` your changes to GitHub. Once you've pushed your code is saved on GitHub, however it isn't accessible from the `master` branch yet, which is by default the main branch tracked by GitHub for releases and issues.

> Note: Since these branches were made locally and need to be pushed up to GitHub, you might be shown an error and prompted to run `git push --set-upstream origin <branch name>` when pushing a branch for the first time. You can simply use the proposed command to create a branch on GitHub before it gets pushed.

## Pull Requests

Because the `master` branch is considered (in most git workflows) to be the most up to date working code most organizations (likely including yours for this course) will lock their `master` or main development branches. Often they lock it so that code reviews and a passing set of unit and/or integration tests are required before code can be merged in to `master` or main devleopment branches. The GitHub pull request (PR) system allows for maintainers to block changes to a branch until they meet specific requirements, such as having a minimum number of approved code reviews and successfully passing automated tests. By having GitHub enforce these rules for us *before* our stable branches (like `master`) can have code added to them, we greatly increase the changes that our stable branches will continue to be stable.

### Requiring Reviews for PRs

In a future lab we will introduce a more formal unit testing framework which can be coupled with continuous integration (CI) tools. The CI tools will automatically run the unit tests when new code is commited, check to see if all the tests pass, and report that status to GitHub (which can then be used as another block for PRs). For now, we are just going to require that PRs have a single approved code review before they can be merged into `master`.

Follow [this GitHub walkthrough](https://help.github.com/en/articles/configuring-protected-branches) to add protections to your `master` branch (you don't need to worry about protecting any other branches for now). The only requirement you need to have is to "Require pull request reviews before merging" and you only need to require one.

### Creating a Pull Request

Navigate to your repository on GitHub and above your files list on the left hand side you should see a "New pull request" button. Click this to be taken to a screen asking you which two branches you want to merge (one being merged, known as the compare, and the one its being merged into, known as the base). Choose the branch you just created in the "Your First Branch" step as the compare and the `master` branch as your base branch. From there you can edit the title (which will default to mimic the branch name), add a description for the PR (it will also show the commits its associated with), assign the PR to a member of your team, request a reiewer of the PR, and add tags (there is more you can do, but these are the basic steps).

Go ahead and set a reasonable name and description of the work that is included in this PR. Over on the right hand side under "Asignees" click the "assign yourself" button or click the gear and choose yourself from the drop-down menu. You can also choose a reviewer under the "Reviewers" menu, but since it won't let you pick yourself it isn't necessary for this lab (but this is normally how you would choose a reviewer). You can also add labels to let others know what this PR regards, but we will skip that step for this lab. Once you have set all the proper information click the "Create pull request" button to make your draft an official PR.

### Code Reviews

When developing on existing projects, team members will usually be working on integrating features, squashing bugs, refactoring, or otherwise working with existing code. To help make sure that new changes will not adversely affect the system and are of generally high quality, code reviews are usually held with other members of the team. While there are lots of different ways to perform a code review, it is typically done through comments (either generally on the PR or related to specific lines of code changed in that PR). This is because GitHub is primarily focused on remote and decentralized teams. Because you are likely to see your team members often, you may find it easier to work through code reviews in person. This is fine, but we do request that you write a simple "Reviewed in person" comment before merging a PR (more on merging in a later section).

You should review this [guide](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/) for some good practices for code reviews, but here are some general rules to keep in mind:

* Start with a positive note: reviewees will be more receptive to your comments if you start with something positive rather than only pointing out the negatives.
* Reference the code not the coder: when you make a comment, reference the code and not the person who wrote the code.
* Use line item suggestions: when reviewing the files you can make a comment on a specific line making it much easier for the reviewee to know exactly what code you are referencing with your comment
* Don't assume you know better: you may think a piece of code is incorrect or inefficient but it maybe that you simply don't have the full context of the problem. Rather than saying something is wrong suggest a way it might be improved and ask if there is an issue with your proposed solution or request more context about why a peice of code was written the way it was.

You should now review the code changes in the PR that you just created. Normally this would be done by someone else in your group (since you are less likely to find issues and errors in your own code), but you will perofrm this step for this exercise. Navigate to the "Pull requests" tab and choose the PR you just created. From here, you can review comments made about the PR under the "Conversation" tab, all commits associated with that PR under the "Commits" tab, and what changes have been made to various files under the "Files changed" tab.

Near the bottom of the "Conversation" tab, you should see a green checkmark next to a title reading "This branch has no conflicts with the base branch". This means GitHub found no merge conflicts between this branch and the master branch. Take a look over your code again and make sure there aren't any issues. Once you've confirmed everything is correct, go ahead and press "Squash and merge" to merge the branches together. There are a number of different methods to merge a PR into another branch, but this is the one we recommend for you to use.

> Note: since this PR does not have an approved code review (since you can't review your own code) you will have to click the override box to allow it to be merged without the approval. Normally you would recieve an "Approved" code review on your PR before merging it and this override wouldn't be necessary

It will give you a chance to write a new PR title and comment, and you might want to write a new comment to clean up the message and remove any unnecessary information or make it generally more readable. After you've merged the PR it will ask you if you want to remove the branch, which you should typically do to keep your list of branches clean. Note that this will remove the branch on the remote but you will need to run `git branch -d <branch-name>` to remove the local branch (replaceing `<branch-name>` with the name of the branch you want to remove). This will cause GitHub to essentially call `git checkout master && git merge <partner-1-github-username>/count-func` behind the scenes and merge the branch into master.

### Tracking Issues

Now that you have completed the initial development you can move the card associated with that task from the "In Progress" column of your Trello board to the "Done" column. This lets everyone else know that you've completed it, and you can now pull another card into the "In Progress" column to signify what you are now working on. You would need to move the card out of "In Progress" before claming a new one if you are limiting your work in progress (WIP) as suggested by Kanban. You might also have moved it into an "In Review" column to signify that it isn't in your working queue (because it is being reviewed and not actively worked on) and to signal to the others in your group that it needs review as a substitution for assigning PRs to a specific indivudal for review. You could also create a new card for "Review PR <pr-name>" which would then be its own task someone could pick up on the Kanban board. All of these are valid development processes, and you are your team should figure out what works best for you.

## Branching to Avoid Merge Conflicts

### The Second Branch

Switch back to the `master` branch with a `git checkout master`. Notice that the code you just merged into `master` doesn't appear in your local copy. This is because while its been updated on the GitHub remote it hasn't been updated locally yet. Update your `master` branch by running `git pull` (this will pull in the changes from remote for whatever branch you are currently on) and you should see your fizzbuzz code get added to your local copy of the repository.

While the program we have developed meets specifications, its not going to be easy to augment or test because its written as inline code. We need to convert the code into a function and pass in the maximum value it should print up to as a parameter. Before you start working take the issue associated with this development and move it to the "In Progress" column on your Trello. Then, create a new branch named `<github-username/fizzbuzz-functionalization` (make sure you switch to `master` before creating your new branch) and convert your current code to be a function with the following signature

```js
function fizzbuzz(max_val):
    // Your modified code here
```

Once you have converted the code into a function make sure to `git push` your local changes to the GitHub remote. After you've pushed, go ahead and open a new PR for this change *but don't merge it yet*.

### The Third Branch

Pretend that you are another developer on your team, and while other you is turning the fizzbuzz program into a function you pulled a newly created issue. Create an issue on your Trello board with the following information:

> Add fizzbuzz functionality so numbers divisible by 5 are replaced with "bool", and "bool" is added to any other words ("fizz" or "buzz") if they are also divisible by 5.

Move the issue associated with this to the "In Progress" column to signify that you (the other developer) are working on this new feature. Switch to the `master` branch and run a `git pull` to make sure you have the latest changes (since we didn't merge the last set of changes, you should). Then create a new branch off master named `<github-username>/fizzbool` which you can use to develop your new feature.  Then switch to that branch and modify the original code with the new functionality. After you are finished push your changes to GitHub and then open a new PR against master with these changes (you should now have 2 PRs open).

## Fixing a Merge Conflict

Go ahead an merge the PR you created for functionalizing the fizzbuzz code (you can do this the same way as before) and move the associated issue from "In Progress" to "Done". Now go to the fizzbool PR and scroll down to the bottom. You should see that the last section says its unable the automatically merge the conflics. Sometimes this last button will allow GitHub to automatically update a PR based on other code being merged, assuming there isn't any quesiton about how the new code and the PR should be combined, but thats not the case here. We will need to merge the PR code into the new master by hand before we can move on.

Let's resolve the merge conflict. Type the following commands which will change your current branch to master, update it to match what is on GitHub, and switch them back to their new branch:

```bash
git checkout master
git pull
git checkout <github-username/fizzbool
git merge master
```

> Note: somtimes when you perform this task you will get an error message about local files being overwritten when attempting to perform this operaiton. If this happens you might need to remove local changes to that file or stash the lcoal changes before you can move on.

The last line will attempt to auto-merge master with the current branch, which we already know from GitHub will cause a conflict. Now you need to open the file which has the conflicts, which you can check by running `git status` and seeing which files are listed with a "both modified" tag before them. Open the "both modified" file in your favorite editor and you'll see there are some new and special symbols in it.

Everything past `<<<<<<< HEAD` and before `=======` is the new code coming in from the branch being merged, while everything past `=======` and before `>>>>>>> master` is existing code from the master branch (the branch that is being merged into). You'll want some code from both versions, so go ahead and pick, choose, and correct the code to be a combination that includes both the functionalization as well as the additional divisible by 5 implementaton, then save it.

Once you are done, be sure to `git add` the file you just modified, commit it, and push to GitHub. When committing a merge, simply typing `git commit` without the `-m` flag will automatically populate a merge message. You should now refresh the PR on GitHub. Notice that every commit made in the branch should appear within the PR automatically, so you don't need to close and re-open a PR if there are issues. PRs and the conversation and commit history associated with them can serve as valuable documentation about why certain design or coding decisions were made.

Using the good practices for code reviews reference above, make sure everything looks good with this PR. There should no longer be any merge conflicts, so go ahead and merge the PR (overriding it since it doesn't have a review) and repeat the same process of deleting the branch as stated above. Make sure to move the last issue from "In Progress" to the "Done" column since its now been merged.

## Tagging

Often, you’ll want to tag certain git commits because they are special. The most common reason to tag a commit in git is to tag it as a stable version, especially when using the [semantic versioning schemes](https://semver.org/). Let's assume that our code is now ready for release as `v1.0.0` and tag it as such.

```
$ git tag -a v1.0.0 -m “Initial stable release”
```

The `-m` in this case works the same as it does when performing a commit, allowing us to add a message but bypassing the editor to do so. The `-m` flag will only allow you to set the title, so make sure to follow the 50 character commit title rule from the Git lab and only use it when no additional information would be necessary in the commit message body. If you wanted to tag a commit besides the current commit you would need to add the commit hash after the version number (but before the message). Normally a 1.0.0 release would have lots of additional notes on the current state of the software, but this is just an example. These tagged versions are stored in a special section of the repository on GitHub along with compressed versions of the source files to make public releases easier. This command creates the tag, but like most git commands it will only create the tag locally. In order to push this tag to GitHub you need to execute the following command.

```
git push origin v1.0.0
```

This will push the tag we just created (`v1.0.0`) to GitHub which is our remote git repository. The remote repository (by convention) is named `origin` which is where we designated the tag to be pushed to.

> Note: It is possible to create both annotated tags using the `-a` flag and unannotated flags. Annotated flags carry additional information about their creation and should be preferred over regular non-annotated tagging.
