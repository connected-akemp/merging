#Repository setup  

These are the steps taken to set up this repository (prior to any merging), so that you can replay them for yourself.  


`git checkout -b develop`  
`echo '#INSTALL' > INSTALL`  
`echo '' >> INSTALL`  
`echo '#Instructions' >> INSTALL`  
`git add .`  
`git commit -m 'added INSTALL file'`  

`git checkout -b feature#123`  
`git checkout develop`  
`git checkout -b feature#124`  
`git checkout feature#123`  

`touch animations`  
`git add .`  
`git commit -m 'added animations file'`  

`git checkout feature#124`  

`touch shaders`  
`git add .`  
`git commit -m 'added shaders file'`  

`git checkout feature#123`  
`echo '- compile animations file' >> INSTALL`  
`git commit -am 'updated INSTALL file'`  

`git checkout feature#124`  
`echo '- compile shaders file' >> INSTALL`  
`git commit -am 'updated INSTALL file'`  

`git checkout feature#123`  
`echo '#Animations' >> animations`  
`git commit -am 'updated animations file'`  

`git checkout feature#124`  
`echo '#Shaders' >> shaders`  
`git commit -am 'updated shaders file'`  

##Merging

###Basic merge
`git checkout develop`  
`git checkout -b basicMerge`  
`git merge feature#123 feature#124`  
`sed -i '' '/[<=>]/d' INSTALL`  
`git commit -a --no-edit`  

`git log --oneline` now produces:  

`06728ea Merge branches 'feature#123' and 'feature#124' into basicMerge`  
`ce8292f updated animations file`  
`da810ff updated shaders file`  
`77ac9ff updated INSTALL file`  
`b63ec10 updated INSTALL file`  
`71abaf3 added shaders file`  
`b4a6eef added animations file`  
`1af0739 added INSTALL file`  
`c4b6c0a Initial commit`  

`git log --oneline --graph` produces:

`*   06728ea Merge branches 'feature#123' and 'feature#124' into basicMerge`  
`|\  `  
`| * da810ff updated shaders file`  
`| * 77ac9ff updated INSTALL file`  
`| * 71abaf3 added shaders file`  
`* | ce8292f updated animations file`  
`* | b63ec10 updated INSTALL file`  
`* | b4a6eef added animations file`  
`|/  `  
`* 1af0739 added INSTALL file`  
`* c4b6c0a Initial commit`  

##Rebase Like "Merge"

`git checkout develop`  
`git checkout -b rebaseMerge`  
`git rev-list --reverse ..feature#123 ..feature#124 | git cherry-pick --stdin`  
`sed -i '' '/[<=>]/d' INSTALL`  
`git add .`  
`git cherry-pick --continue`  

`git log --online` produces:

`4ae6ac2 updated animations file`  
`f0f8f24 updated shaders file`  
`f6b88d8 updated INSTALL file`  
`29869d6 updated INSTALL file`  
`8553dbc added shaders file`  
`08ba55c added animations file`  
`1af0739 added INSTALL file`  
`c4b6c0a Initial commit`  

`git log --online --graph` produces:

`* 4ae6ac2 updated animations file`  
`* f0f8f24 updated shaders file`  
`* f6b88d8 updated INSTALL file`  
`* 29869d6 updated INSTALL file`  
`* 8553dbc added shaders file`  
`* 08ba55c added animations file`  
`* 1af0739 added INSTALL file`  
`* c4b6c0a Initial commit`  

##Rebase

`git checkout feature#124`  
`git checkout -b rebase#123onto#124`  
`git rebase feature#123`  
`sed -i '' '/[<=>]/d' INSTALL`  
`git add .`  
`git rebase --continue`  

`git log --oneline` produces:

`67ac05e updated shaders file`  
`63445ec updated INSTALL file`  
`6750b7f added shaders file`  
`ce8292f updated animations file`  
`b63ec10 updated INSTALL file`  
`b4a6eef added animations file`  
`1af0739 added INSTALL file`  
`c4b6c0a Initial commit`  

`git log --oneline --graph` produces:

`* 67ac05e updated shaders file`  
`* 63445ec updated INSTALL file`  
`* 6750b7f added shaders file`  
`* ce8292f updated animations file`  
`* b63ec10 updated INSTALL file`  
`* b4a6eef added animations file`  
`* 1af0739 added INSTALL file`  
`* c4b6c0a Initial commit`  
