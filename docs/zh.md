# Town Pack — 城镇、住宅与酒吧背景及酒吧环境音

Town Pack 是为小镇故事准备的现成布景：三张绘制好的背景图——城镇入口的街角、住宅门厅和夜晚的酒吧——外加酒吧的环境音循环。它不含剧情、场景或角色：图在哪里出现，由游戏自己决定。

两个内置游戏已经在共用它。**Cthangover** 使用城镇入口和门厅；**My Novel** 模板则把三张背景和酒吧环境音全用上了。由于两个游戏取用的是这个模组里的同一批文件，Town Pack 里的一处修正或一张更好的图，两边都能受益。

## 里面有什么

城镇入口 `town/town_entry`：铺着石板的街角，商店遮阳篷条纹相间。

![城镇入口背景：石板路街角的一栋转角建筑，带着绿色和白色的遮阳篷。](assets/town_entry.jpg)

住宅门厅 `home/vestibule`：带楼梯、扶手椅和挂画的门厅。

![门厅背景：暖光笼罩的门厅里有木质楼梯、扶手椅、长凳和一幅装框的画。](assets/vestibule.jpg)

酒吧 `bar/bar`：挂着灯笼的桌台、吧台和一排排酒瓶。

![酒吧背景：灯笼照亮的桌台、吧台，以及横梁天花板下的酒架。](assets/bar.jpg)

酒吧环境音 `bar/bar_ambient`：供 Ambience 声音通道使用的酒吧氛围 Ogg Vorbis 循环。

三张图都是 1920 × 1024。每张图都有一个同名、带 `_depth` 后缀的灰色伴生文件：

![城镇入口的深度图：同一构图的灰度版本。](assets/town_entry_depth.jpg)

深度图不会直接展示给你看。显示背景时，游戏会同时加载 `<name>_depth` 并交给光照系统，供放置在场景上的光源使用。没有深度图的背景也能正常显示。

## 在哪里能看到它

- **Cthangover：** `town_entry` 场景（城镇入口）和 `home_vestibule` 场景。
- **My Novel 模板：** `my_novel_town`、`my_novel_home` 和 `my_novel_bar`。酒吧场景还会播放 `bar/bar_ambient`。

同一段城镇入口，在 My Novel 模板里伴着一段叙述为游戏开场：

![My Novel 的第一个场景：城镇入口背景上显示一行「傍晚的小镇。路灯已经亮起，一阵凉风沿着石板路吹过」。](assets/reuse-my-novel.jpg)

而在 Cthangover 里，同一个画面上，另一个故事给出了自己的选项：

![Cthangover 的城镇入口：同一背景，选项为「回家」和「查看小巷」。](assets/reuse-cthangover.jpg)

Town Pack 属于两个游戏的合集，会随它们一起加载。仅安装它并不会把这些地点加进别的游戏：游戏必须在自己的场景里使用这些背景。

## 在你的游戏中使用这些背景

1. 把 `town_pack>=1` 加入内容模组的 `depends` 列表。
2. 把 `town_pack>=1` 加入游戏的合集，就像 My Novel 模板在 **Assets** 块中做的那样。
3. 按下文的名称引用资源。名称相对于 `backgrounds/` 和 `sounds/`，不带扩展名。

```jsonc
// mods/my_game/manifest.json — 添加到已有列表
"depends": ["town_pack>=1"]
```

下面这段取自模板的 `my_novel_bar` 场景，展示酒吧并播放环境音：

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

剧本也可以在对话中途切换画面：

```scenario
background town/town_entry
text "这个点，街上一个人影也没有。"
```

可用的名称如下：

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## 为你的游戏替换图片

想替换图片又不想改动 Town Pack，可以在自己的模组里放一个相对名称相同的文件（例如 `backgrounds/bar/bar.png`），并在 `depends` 里声明 `town_pack>=1`。依赖所有者的模组后加载、优先生效。替换背景时，还要附带一个同名的 `_depth` 文件：否则游戏仍会找到 Town Pack 原来的深度图，光照就会按旧图的构图分布。

没有依赖声明时，两个提供同名资源的模组加载顺序不确定；资源图谱工具会把这种情况报为错误。

## 如果有东西没显示

1. 背景变黑或缺失，多半是名称写错了。名称区分大小写，使用 `/`。
2. 确认 Town Pack 被包含在所启动的游戏里，而不只是安装了。
3. 酒吧没有声音：检查场景的 `defaultAmbient` 是否为 `bar/bar_ambient`，并确认 **Settings → Sound**（设置 → 声音）里 **Ambience** 已开启。声音播放由 Audio Engine 模组提供。
