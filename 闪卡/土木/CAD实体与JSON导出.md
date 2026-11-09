#flashcards 
# CAD 实体与 JSON 导出

把 DWG 里的实体导出成 JSON 时，为什么不必把所有属性都写上？
?
只为「画出来/展示」用时，只需要图层、类型、线型、比例、起终点等值；handle id 这类内部标识用不上。

handle 和 ObjectId 在持久性上有什么区别？
?
handle 写在 DWG 文件里，文件内唯一，可持久保存；
ObjectId 只在当前会话的数据库/内存里唯一，重开或换进程就失效。
所以只有 handle 值得存进 JSON。

用 JSON 里存的 handle 回查实体（比如改颜色），前提是什么？
?
必须是同一份 DWG，且该实体还在；换一张图纸，handle 不保证指向同一个实体。
