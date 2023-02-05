<h1>Git</h1> 


1. Commits are immutable
2. Commits contain all information about repository.
3. How do you know which commit are you working on?
   - It references/pointed to head.
4. Can we make Empty commits in Git?
   - No.
5. 

<h1>Git commands</h1>

+ git add .
+ git commit -m <message>
+ cdgitgraph
+ git log -p
+ git diff <> <>
+ git diff --cached <h3> shows the differnce between staged and whats the last commit in repository <h3>
+ git diff <h3> Between working and last commit <h3>
+ git diff HEAD <h3> Between working to commit in repository <h3>
+ git reset <h4> It will remove all the staged content. So basically it matches the last commit in the  repository   <h4>
+ git reset --hard <h4> It will remove from the working direcory. So basically it matches the last commit in      the working directory<h4>
