[Rime](https://rime.im/) 输入法是一个输入框架，不是输入法本身。

配置文件参考了： [KyleBing](https://github.com/KyleBing/wubi-jidan-dict)。


**将文件复制到Rime工作目录中，部署后即可使用。**

# 说明

1. `z`键可用来快速输入刚才的内容，最多显示三项，可在`dianer.schema.yaml`中修改。
2. `/`可用来输入各种特殊符号，具体可查看`symbols.yaml`
3. `` ` ``可用拼音来反查五笔编码，在一时想不起五笔编码时，这个功能比较有用。
4. `;`和`'`用来选择第二、第三候选词上屏。
5. `Tab`和`]`向后翻页，`Shift+Tab`和`[`向前翻页。
6. `Ctrl+8`切换中英文标点，`Ctrl+9`切换生僻字。
7. 候选字数量可在`dianer.schema.yaml`中修改。
8. 时间插件命令：`now` `date` `week` `mont` `year` `dwt` `time` 
9. 如果需要编码逐渐提示，在`dianer.schema.yaml`中修改`enable_completion`的值为`true`。
10. 如果需要以`z`、`8`和`9`来选择第3、4、5候选项，可以在`dianer.schema.yaml`取消相应注释。

更多设置请查看配置文件。

# 091五笔，点儿词库

在**王永民**发明的86五笔基础上，**行走的风景**改良了字根及词库，称为**091五笔**。

后来由**晓览**（[晓览的网盘](http://gaokuan.ysepan.com/)）接手，又增添、删改了大量的字根和词条，最终命名为**点儿词库**，按年或季度更新。我询问过他是否可以放在GitHub上，他说可以**随意传播**这个词库。

## dianer.dict.yaml
本词库词条均来自晓览的原版点儿词库（2025春版），主要是改成Rime格式，增加权重，未删改任何词条，共有21.9万多词条。

词条在`dianer.dict.yaml`文件中。

生僻字在`dianer_spz.dict.yaml`中，已在dianer.dict.yaml中挂载，默认过滤生僻字，可按快捷键`Ctrl+0`选择相应的选项启用。

## dianer_spz.dict.yaml
除了`dianer.dict.yaml`中的27345个生僻字（权重为0）以外，其它生僻字（66119个）都在`aniu_spz.dict.yaml`这个文件中，几乎包含了所有的生僻字。

配置中默认过滤僻字，按快捷键`Ctrl+0`可选择相应的选项启用。

## dianer_user.dict.yaml
本来是用来记录用户词条，如果不需要可以在**dianer.dict.yaml**中注释掉。

## symbols.yaml
标点符号映射和各种特殊的符号（以`/`开头，具体请查看文件）。

# ri脚本
这是一个bash脚本，用来查询、修改、增删、导入词条的小工具，需要安装fzf，`-v`选项使用了`nvim`。

对应的输入法是fcitx5，工作目录是`~/.local/share/fcitx5/rime/`如果是别的输入法，那就需要修改脚本中的相应路径了（第4行）。

**修改字典文件和配置文件后，要重新部署才能生效。**

## 语法：

- `ri [-h|--help]`  显示本帮助
- `ri code`         查询形如`code`的编码，支持以`.`替代字母，如`ri ad.`，`ri ad..`，`ri .d.`等，不包括生僻字
- `ri code,`        查询以`code`的单字编码，包括生僻字
- `ri 词条`         查询`词条`的编码，支持以`.`代替汉字，包括生僻字
- `ri -d code`      删除词条，支持多选删除
- `ri -c code`      修改编码或权重，在修改环节，如果修改权重只需要数字；修改编码则需要提供`词条 编码 权重`，以空格区分即可，如果词条中带有空格，请使用`---`代替。不支持多选。
- `ri -a code`      在所选词条后添加新的词条，在新增环节，输入`词条 编码 权重`，以空格区分即可，如果词条中带有空格，请使用`---`代替。不支持多选。
- `ri -s code`       交换**两行**的位置及权重，注意：只能选两行，不能多选，也不能少选，如果词条中带有`:`或`;`或空格的话，不要用这个命令。
- `ri -p 词条 code 权重`    在`user`词库末尾追加新的编码，如果词条中有空格，请以双引号包裹词条
- `ri -v <aniu>`    使用nvim打开`aniu`文件
- `ri --sort`       将主字典按code和权重重新排序，并去重
- `ri --input file`      将file文件中的词条导入主字典，文件中的格式要符合词典要求，脚本本身并不严格审查，只将可能存在的空格替换为制表符，并且至少有三列（即xxx yyy zzz）的数据才会导入

上述`code`指的是词条的编码。

**注意**：不支持同时使用多个参数。

除了查询和`-p`处理`dianer_user.dict.yaml`外，其它参数处理的主字典文件是`dianer.dict.yaml`。



# 简体拼音
 `pinyin_simp`方案，词库文件主要来自**白霜拼音**（[rime-frost](https://github.com/gaboolic/rime-frost)）

# 英文
 `melt_eng`方案，一个简单的英文输入方案，词条数并不多，也是来自**白霜拼音**（[rime-frost](https://github.com/gaboolic/rime-frost)）。

# 皮肤
 `aniu.trime.yaml`是适用于安卓端同文输入法的皮肤文件，我结合默认的同文风皮肤和[mytrime](https://github.com/chwt163/mytrime)的色彩风格修改而来，适用于`3.3.3`的版本。

 至于`squirrel.custom.yaml`和`weasel.custom.yaml`，它们是其它平台的皮肤文件，我没有用过，不知是否还能用，不需要可以删除。

# 其它
 方案`numbers` （大写数字）,如果觉得不需要，可以删除。


 # 推荐
五笔学习推荐B站[晓览YMPA](https://space.bilibili.com/108585624)的视频。

官方教程：[rime输入法用户指导](https://github.com/rime/home/wiki/UserGuide)
