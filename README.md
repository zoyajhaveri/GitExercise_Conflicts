# GitExercise_Conflicts

This exercise assumes you are using recent Jupyterlab with the git extension built on nbdime.  For this quarter in COGS108 those assumptions are true on Datahub. If you try this on your local computer this may or may not be true. If you are using VSCode on your local computer or something else entirely, there are other ways of doing these operations... you should figure it out yourself for whatever tools you like to use!

This repo contains two branches: main and ex1. There is a single line text conflict in one cell between the two branches. The goal is to merge branch ex1 into branch main.


1. Clone this repo to your datahub or local computer. In a terminal window type `git clone https://github.com/COGS108/GitExercise_Conflicts.git`
2. This clone only brings the main branch to your computer... we also need a local copy of the ex1 branch which you can get by typing the following two lines of code in the terminal (press return each time)<br>
`cd GitExercise_Conflicts`<br>
`git checkout -b ex1 origin/ex1`<br>
that last line sets up a local branch called ex1 to track the remote branch of the same name (origin is git's word for the remote repo)
3. We want to merge ex1 into main, not the other way around! The merge command assumes the branch you're in right now is the destination, but the checkout command above put us on ex1.  Let's hop back to main to do this right... type `git checkout main`
4. Ok now we have both branches locally, and we are ready to merge ex1 into main. Let's see what the difference between branches actually is.  Type `git diff ex1`
5. Now merge ex1 into main by typing `git merge ex1` ... and yes it will give you the conflict message we expect
6. Up to this point I very purposefully did NOT tell you to open Project.ipynb... if you try to double click on the notebook now you will get an error message telling you that file is NOT correct JSON. This is becuase the merge conflict has broken the syntax of a notebook file... a snippit of the file will at this moment look like:
```JSON
    "ax.set(xlabel='time (s)', ylabel='voltage (mV)',\n",
<<<<<<< HEAD
    "       title='The simplest plot in the world')\n",
=======
    "       title='This plot is simple!')\n",
>>>>>>> ex1
    "ax.grid()"
```
and all those greater than/less than/equals symbols set off the conflict and also break JSON syntax.  So you can't look at this merged/conflicted notebook the way you normally do.
7. Let's use Jupyterlabs built in git extensions to view and deal with the conflict.  First go to the far left of the window, and you will see a vertical stack of icons in a grey panel.  Click on the one that's a diamond with some lines inside it, that's the git panel. 
8. Now you will see a set of panels, one of which shows Conflicted files... there it is Project.ipynb!  Double click to open a tool for resolving the conflict
9. The tool shows 3 versions of the conflicted cell from left to right... the current (main), the most recent ancestor when both branches were the same, and the incoming branch (ex1). Underneath those 3 panels is a fourth panel... this is the one you edit to resolve the conflict
10. Change the fourth panel to be whatever you want the end result to be. 
11. Click the "Mark as resolved" button the top right, now you will see Project.ipynb change from the Conflicted to Staged (the tool automagically did a `git add` for you)
12. You can actually make the commit right underneat the Staged file... make sure to put a message in to the commit before you press the commit button!
ommit the changes on e2
   

Congrats!! You've dealt with a VERY SIMPLE version of the notebook conflict problem. 

And now you know why version control with notebooks is hard!  It would have been slightly easier with a normal set of .py files.  It could have been a lot harder if the notebooks involved hadn't had all their outputs cleared before commit.  When notebooks have metadata or binary data from the actual plot stored in the .ipynb file version control can be even more annyoing. 
