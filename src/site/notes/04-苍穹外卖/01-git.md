---
{"dg-publish":true,"permalink":"/04-苍穹外卖/01-git/","dgPassFrontmatter":true}
---


## 1. .gitignore 语法


> [!cite]+ 
> 
> Git官方文档 https://git-scm.com/docs/gitignore 
 

`.gitignore` 文件用于指定 **Git 要忽略**（不追踪、不提交）的文件和目录。

> 通常位于项目根目录，但也可以存在于子目录，作用范围是当前目录及其子目录。

### 1.1. 📌 基本语法

- `#` 开头：注释
- `!` 开头：例外规则（取消忽略，即强制跟踪）
- `/` 开头：匹配项目根目录下的路径（相对 `.gitignore` 所在位置）
- `/` 结尾：表示目录（否则为文件）
- 没有 `/` 开头：表示匹配所有层级（等价于 `**/pattern`）
    
### 1.2. 📌 通配符

| 通配符 | 含义                     | 示例                          |
| ------ | ------------------------ | ----------------------------- |
| `*`    | 匹配任意字符（不含 `/`） | `*.log` → 所有 `.log` 文件    |
| `?`    | 匹配任意一个字符         | `?.txt` → `a.txt`, `b.txt`    |
| `**`   | 匹配任意多级目录         | `**/temp/` → 所有 temp 文件夹 |

---

### 1.3. ✅ 示例说明


```gitignore
# 忽略所有 .log 文件
*.log

# 忽略所有层级中的 target 目录
**/target/

# 仅忽略根目录下的 .env 文件
/.env

# 忽略 frontend/node_modules
/frontend/node_modules/

# 忽略所有 node_modules（任意位置）
**/node_modules/

# 忽略 test/ 目录，但不忽略其中的 keep.js 文件
test/
!test/keep.js

```


## 2. 常用命令

```bash
git rm --help
git rm -rf --cached 文件夹
git rm --cached 文件
```