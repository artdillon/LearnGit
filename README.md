### create a new repository on the command line



```bash
echo "# LearnGit" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main   # 修改分支的名字
git remote add origin https://github.com/artdillon/LearnGit.git
git push -u origin main
```

###  push an existing repository from the command line



```bash
git remote add origin https://github.com/artdillon/LearnGit.git
git branch -M main
git push -u origin main
```