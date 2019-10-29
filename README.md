# git-practice
 
## 具体规则
    <type>(<scope>): <subject>
    
    type
    
    用于说明commit类别，只允许使用以下7个标识
    
    1.  feat：新功能（feature）
    2.  fix：修补 bug
    3.  docs：文档（documentation）
    4.  style： 格式（不影响代码运行的变动）
    5.  refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
    6.  test：增加测试
    7.  chore：构建过程或辅助工具的变动
    
    scope
    
    用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同
    
    subject
    
    是 commit 目的的简短描述，不超过 50 个字符。
    
    以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
    第一个字母小写
    结尾不加句号（.）
    
## 异常处理
     INVALID COMMIT MSG: does not match "<type>(<scope>): <subject>" !jartto:fix bug
     
     原因：使用了规范外的关键字； 其二，很细节的问题，jartto：后少了空格
     
## 修改之前的commit信息

    将当前分支无关的工作状态进行暂存
    git statsh
    
    将 HEAD 移动 到需要修改的commit上
    
    1、git rebase 9633cf0919^ --interactive
    3、找到需要修改的 Commit，将首行的 pick 改成 edit
    4、开始着手解决你的 bug
    5、 git add 将改动文件添加到暂存
    6、 git commit –amend 追加改动到提交
    7、git rebase –continue 移动 HEAD 回最新的 commit
    8、恢复之前的工作状态
    9、git stash pop
    
## 项目中使用 Node 插件 validate-commit-msg 来检查项目中 Commit message 是否规范
    安装插件
    npm install --save-dev validate-commit-msg
    
    使用方式一：建立.vcmrc文件
    
    {
        "types": ["feat", "fix", "docs", "style", "refactor", "perf", "test", "build", "ci", "chore", "revert"],
        "scope": {
    
            "required": false,
    
            "allowed": ["*"],
    
            "validate": false,
    
            "multiple": false
        },
    
        "warnOnFail": false,
    
        "maxSubjectLength": 100,
    
        "subjectPattern": ".+",
    
        "subjectPatternErrorMsg": "subject does not match subject pattern!",
    
        "helpMessage": "",
    
        "autoFix": false
    } 
    
    使用方式二：写入 package.json
    {
        "config": {
            "validate-commit-msg": {
              /* your config here */
            }
        }
    } 
    
    自动使用ghooks 钩子函数
    
    {
        …
        "config": {
            "ghooks": {
    
              "pre-commit": "gulp lint",
    
              "commit-msg": "validate-commit-msg",
    
              "pre-push": "make test",
    
              "post-merge": "npm install",
    
              "post-rewrite": "npm install",
              …
            }
        }
        …
    } 

## Commit 规范的作用
    
    1、提供更多的信息，方便排查与回退；
    2、过滤关键字，迅速定位；
    3、方便生成文档。
    
## 使用工具 Conventional Changelog 生成 change log
    
    npm install -g conventional-changelog 
    
    将其写入 package.json 的 scripts 字段  
    { 
      "scripts": { 
        "changelog": "conventional-changelog -p angular -i CHANGELOG.md -w -r 0" 
      } 
    } 
    使用
    npm run changelog 
    
## Commitizen是一个撰写合格 Commit message 的工具。
    
    安装命令如下。
    
    $ npm install -g commitizen
    然后，在项目目录里，运行下面的命令，使其支持 Angular 的 Commit message 格式。
    
    $ commitizen init cz-conventional-changelog --save --save-exact
    以后，凡是用到git commit命令，一律改为使用git cz。这时，就会出现选项，用来生成符合格式的 Commit message
## ghooks 为nodejs打造，帮助实现本地 git hooks     
    npm install ghooks --save-dev
    
    git commit 提交报错时 可用 git cz 按照规范选择提交
