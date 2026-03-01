# git remote
## 添加远程库
git remote add notes git@github.com:alipuuuuu/notes.git

## 修改 origin 地址
git remote set-url origin git@github.com:alipuuuuu/notes.git

## 删除多余 remote
git remote remove notes

# git push
## 强推
git push --force-with-lease origin main

如果没有fetch，则无论如何push都会失败，fetch并不会改变本地文件，只有merge或rebase之后才会

# git fetch
git fetch origin

# 查看分叉图
git log --oneline --decorate --graph --all -n 20

# pull
git pull --ff-only

只允许快进更新（Fast-Forward），否则直接失败，不做任何修改

快进更新：远程只是比你多了几个提交，你本地没有分叉

# 以远程库为准
git fetch origin

git reset --hard origin/main