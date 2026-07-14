<h1>DevOps</h1> =bridge in between development in operation
tools: Git&GitHub (version tools and kit), terraform(infra create), ansible(configuration),docker,  k8s, Jenkins(CI/CD pipeline),Prometheus(monitor ci/cd pipeline), grafana(cheking logs

What is Git ?
Git is version control system tools used to track changes in your code(track code). popular, free & Open Source, fast &scalable
-track history
-helps to collaborate with project worker
What is git hub ?
GitHub is cloud platform used to store source code in the form of repositories(folder).
website that allow developers to store and their code using git
in this changes = commit
What is repository?
It is folder or storage location used to store source code, files, and the history of changes
What is Token?
Token is secret key that allows your computer or application to accesss your github account without using your real password
create token profile pic- settings- Developer settings- personal access tokens- token(classic)- gernerate token


git config --global user.name "sonu"
git config --global user.email "bhavanaghule23@gmail.com"
git config user.name
git config user.email
git config --list

What is Origin?
origin is nickname (alias) for the remote repository URL
git clone "url"
git add ./filename
git commit -m "one file xyz added"
git push origin main
\\after that they will ask you the password then enter the token


Clone& Status:->
clone- cloning a repository on our local machine === git clone <-some link->  /// it helps to connect your project to the server
status- displaying the states of the code  ==== git status
- when we uses remote and local so it mean to remote= GitHub and local= laptop/pc
the status of git:-
*untracked-new files that git doesn't yet track
*modified - changed but not staged
*staged - file is ready to be committed
*unmodified - unchanged
*commited - saved history
 
Add & Commit:->
=add- adds new or changed files in your working directoring to the git staging area
git add <- filename->
=commit-it is the record of change
git commit -m "some message"

push command:->
=push - upload local repo content to remote repo
git push origin main

Creates Repo:->
//see you want to add the repository and file in the git hub without clone so just create the folder and just run following commands through that
Init command:
init=used to create a new git repo
git init
git remote add origin <-link->
git remote -v      		///to verify remote
git branch 	   		///to check branch
git branch -M main 	///to rename branch
git push origin main


Branch Command:-> branch means the path where independently developer working on project at same time without affecting each other and waiting for each other and also one thing after creating completion we can merge the branches.
it use to create independent copy of the code so developers cn work sfely without affecting m,ain projects.
git branch 							                  ///to check branch
git branch <-branch name->			        	///to create the branch
git branch -m main 				              	///to rename branch
git checkout <- branch name	->		      	///to navigate means changing the branch
git checkout -b <- branch name->	      	///creating new branch
git branch -d <- branch name->		      	///to delete branch
git push origin <-branch name->		       	///to push branch into the github
git push origin  --delete <-branch name->	///to delete branch from the remote server as well as local

Merging Code:->
way1 :
git diff <-branch name-> 				///to compare commits, brnches, files & more
git merge <-branch name->				///to merge 2 branches
way2:
Create a PR(pull request)       //pull request - It lets you tell others about changes you've pushed to branch in a repository on GitHub.
Pull Command:->
git pull origin main
used to fetch and download content from a remote repo and immediately update the local repo to match that content.

Resolving Merge Conflicts:->   an event that takes place when git is unable to automaticvally resolve differences in code between two commits.

Undoing changes:->
case 1 : staged changes(add zalet)
   git reset <-file name->
   git reset
case 2 : commited changes(for one commit)
   git reset HEAD~1
case 3 : commited changes(for many commits)
   git reset <-commits hash ->	        ///this is for undo the changes in remote server (github)
   git reset --hard <-commit hash ->    ///this for undo the commited changes in the local server also

Fork :->
A fork a new repository that shares code and visibility settimgs with the original "upstream" repository.
Fork is a rough copy.
