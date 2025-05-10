---
{"dg-publish":true,"permalink":"/temp/","dgPassFrontmatter":true}
---

juna3066@163.com 重新和 16639002690  关联 注册 vercel.com
(juna3066@qq.com 和 16639002690 关联 已经 注销 vercel.com)
再看和github关联页面。


## 1. 测试图

![assets/temp/IMG-20250509-200545-142.png](/img/user/assets/temp/IMG-20250509-200545-142.png)

## 2. 问题

### 2.1. git最新提交记录90f3e4e多提交了文件,且为提价到远程，如何解决？

```
# 1. 从提交中移除不需要的文件但保留在工作目录
git reset --soft HEAD~1

# 2. 取消暂存不需要的文件
git reset HEAD 不需要的文件名

# 3. 重新提交
git commit -c ORIG_HEAD
```