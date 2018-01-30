### Emmet 安装成功补全失败问题

安装完成后我们利用Emmet插件去快速生成HTML代码，例如输入html:5按住Tab键即可生成HTML文件完整的结构

但是很多人在安装完成后输入html:5然后按住Tab键并没有反应，这是什么原因导致的呢？原来Emmet默认的快捷键是Ctrl+E，我们需要将其设置成常用的Tab键。


在菜单栏选择Preferences-->PackageSettings-->Emmet-->KeyBindings-->User，将以下信息粘贴进去即可。
```
[{"keys": ["tab"], "args": {"action": "expand_abbreviation"}, "command": "run_emmet_action", "context": [{"key": "emmet_action_enabled.expand_abbreviation"}]}]
```

