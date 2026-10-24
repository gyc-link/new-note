#flashcards 
# Tekla 图纸 API

> 来源：2026-10-23 收件箱「Tekla OpenAPI 单零件图初始化」，2026-10-24 处理

`new SinglePartDrawing(partId, "属性文件名")` 会在模型里创建图纸、生成 `.dg` 文件吗？
?
不会。这一行只创建内存中的图纸对象。
调用 `Insert()` 才把图纸插入模型；之后 Tekla 在模型文件夹的 `drawings` 目录写 `D0000123456.dg`。
（有活动图纸时不能 Insert。）

传入一个找不到的属性文件名，`SinglePartDrawing` 构造函数会向插件抛异常吗？
?
不会（实测：插件不抛异常，Tekla 弹窗）。
属性文件的解析在 Tekla 原生/界面层，错误以弹窗或日志出现，插件的 `try/catch` 抓不到。
别把「没抛异常」当成「属性加载成功」。

`SinglePartDrawing(Identifier, string)` 的第二个参数是图纸属性对象吗？
?
不是对象，是**属性文件名**。
2026 版文档中的重载：`(Identifier)` 用标准属性；`(Identifier, int)` 标准属性 + 图幅号；`(Identifier, string)` 指定属性文件。
文档中未见接收属性对象的构造函数。
