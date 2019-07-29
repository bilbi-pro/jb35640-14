# **Task #1: Git Operations**


## content table
* Task #1: Git Operation

    
  
## Task review
- Sub-task 2.1: **maven based build** 
## SUB TASKS:
### sub-task 1: simple operations with Git repo with single branch
explanation:
- here you will create a new repo in your github account, feel free to chose one, 
- you  will clone it to your local workstation, perform some modifications and commit and push it properly 
steps:
1. perform login to your gitHub account
2. create new public repository, 
3. clone the newly repo created, using following command
  ```bash
git clone https://github.com/<github-username>/<repo>.git
``` 
4. cd into the new directory
5. create new 4 files, use following code to help you
```bash
touch {fil1.txt,fil2.txt,fil3.txt,fil4.txt}
```
6. add only 2 file to be tracked: file1.txt and file2.txt
```bash
git add file1.txt
git add file2.txt
```
7. commit your changes
```bash
git commit -a "my message"
```

8. tag your commit 
```bash
git tag "my important tag"
```

9. push your changes
```bash
git push
```

