# my GRUB theme

本主题参考：[ClF3's blog](https://blog.clf3.org/post/grub-theme-tutorial/)

还可参考：[voidlhf/StarRailGrubThemes](https://github.com/voidlhf/StarRailGrubThemes)

## 使用

1. 将主题文件夹保存到`/boot/grub/themes`
2. 编辑`/etc/default/grub.d/90_custom.cfg`，添加如下内容指定GRUB主题文件的位置：

```
GRUB_THEME="/boot/grub/themes/bonjean-grub-theme/GRUB_theme/theme.txt"
```

3. 重新编译GRUB：`sudo update-grub`

## 文件说明

* `icons`文件夹存放各种系统的图标，用在各种类型系统的选项前面；
* `background.png`定义背景图片；
* `selected_*.png`定义操作系统选框的贴图；
* 最核心的`theme.txt`包含了整个主题的配置信息

## theme.txt 介绍

```
title-text: ""
desktop-image: "background.png"
terminal-left: "0"
terminal-top: "0"
terminal-border: "0"
terminal-width: "100%"
terminal-height: "100%"
 
+ boot_menu {
  left = 120
  top = 47%
  width = 472
  height = 35%
  item_color = "#cccccc"
  selected_item_color = "#ffffff"
  icon_width = 36
  icon_height = 36
  item_icon_space = 20
  item_height = 40
  item_padding = 2
  item_spacing = 40
  selected_item_pixmap_style = "select_*.png"
}
 
+ label {
  left = 120
  top = 83%
  align = "center"
  id = "__timeout__"
  text = "Selected OS will start in %d seconds"
  color = "#cccccc"
}
```

最开始的一段是一些全局属性：
* title-text是标题，显示在上方中央的位置
* desktop-image指定了背景图片
* terminal-left和terminal-top指定了Grub Terminal的左上角的位置
* terminal-width和terminal-height指定了Terminal的宽度和高度。这些宽度、高度和位置的指定都支持使用像素或者百分比或者两者混合，例如"12%+100"。下文提到的宽度、高度和位置也同理

下面的boot_menu和label是两个组件(component)：boot_menu给出选项的启动菜单；label代表你希望自定义显示的一段话

每个组件有自己的属性，其中：
* left, top, width, height含义和全局属性类似，表示左上角的位置以及组件本身的长宽
* item_color和selected_item_color指定每一项的文字默认颜色以及被选中时的颜色
* 下面一些项指定了图标的长宽，项目文字和图标的距离，项目之间的距离等等，具体可以查阅官方文档
* selected_item_pixmap_style通过9张小图片指定了一个item的四角、四边以及内部应该用什么样的贴图，我们需要提供9张后缀分别为c, e, n, s, w, ne, nw, se, ew的小图片，GRUB就会把它们拼成一个完整的背景框，用在这个item上
* selected_item_pixmap_style表明仅有被选中的item适用这个贴图

label组件的各种东西是类似的，需要注意的是id设为"timeout“就可以使用%d在文字中代表剩余秒数

## 技巧

由于Grub的字体比较有限，而且大小也很难调整，因此可以选择直接将标题做到背景图片里
