# 安装

## Mac

通过Homebrew安装：

<http://blog.teamtreehouse.com/install-node-js-npm-mac>

更新：`brew upgrade node`

卸载：`brew uninstall node`

### 切换到国内镜像

命令行输入，注意使用 bash 的对应修改相关 .bashrc 或 .bash_profile 文件

```
echo '\n# alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org --cache=$HOME/.npm/.cache/cnpm --disturl=https://npm.taobao.org/dist --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc
```