# 系统相关

## 打开不明身份文件

`sudo spctl --master-disable`

可通过`sudo spctl --master-enable`重新打开安全策略

## Dock

### 给Dock加一些“分割线”

```
defaults write com.apple.dock persistent-apps -array-add '{ "tile-type" = "spacer-tile"; }'
killall Dock
```