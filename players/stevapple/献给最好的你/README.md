# 献给最好的你（macOS）

前一阵子闹得沸沸扬扬的 9·27 事件过后，我校有同学就提出应该以校歌《永恒的东风》作为循环播放的背景音乐制作类似 app →_→ 没想到真的做出来了。

这道题很显然（划掉）是一道逆向题……但我使用了一种带有尝试形式的“正向”做法。

首先，进入 Android Studio，选择 Profile or debug APK，并选中题目所给的文件以打开。

观察目录结构，不难发现编写的代码应该位于 `com.hackergame/eternalEasterlyWind` 中，目前还是 smali 格式。

使用 `Run 'bestofyou'` 启动模拟器调试这一 APK，随便尝试输入，发现回车后总有形如 `pass1: ywjJzgvMzW==` 的调试输出。尝试若干不同输入，发现：

-  `pass1:` 后的字符串长度均为输入字符串的 1.5 倍
-  大部分情况下该输出字符串的结尾有 = 号
-  同一输入对应的输出一致

不难猜测这是经过 base64 编码的输入值，经验证发现确实如此。

接下来，快速浏览该目录的各 smali 文件，找到其中以 = 号结尾的字符串（因为不知道如何搜索所以我本人是肉眼观察的），定位到 `data/LoginDataSource.smali` 的第 180 行，将该字符串 `"AgfJA2vYz2fTztiWmtL3AxrOzNvUiq=="` 进行 base64 解码后得到密码，输入后得到 flag。