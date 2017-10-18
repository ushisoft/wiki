# Homebrew

## 安装

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

## Cask

brew常为command line工具，cask多为gui工具。

### 使用版本

先执行`brew tap caskroom/versions`

再查找`brew cask search java`

就可以找到java的历史版本

#### jenv

用于方便切换Java版本，参考<http://www.jenv.be/>

同样使用brew安装`brew install jenv`

初始化jenv，添加如下代码到`~/.bash_profile`

```shell
# Init jenv
if which jenv > /dev/null; then eval "$(jenv init -)"; fi
```

添加Java环境到jenv，like：
```
$ jenv add /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
$ jenv add /Library/Java/JavaVirtualMachines/jdk17011.jdk/Contents/Home
```

使用：

List managed JDKs
```
$ jenv versions
  system
  oracle64-1.6.0.39
* oracle64-1.7.0.11 (set by /Users/hikage/.jenv/version)
```

Configure global version
```
$ jenv global oracle64-1.6.0.39
```

Configure local version (per directory)
```
$ jenv local oracle64-1.6.0.39
```

Configure shell instance version
```
$ jenv shell oracle64-1.6.0.39
```