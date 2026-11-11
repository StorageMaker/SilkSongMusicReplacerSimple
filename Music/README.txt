Music Replacer —— 替换音乐存放文件夹
=====================================

把你想用来替换游戏音乐的音频文件放在这个文件夹里（或直接通过游戏内「音乐替换」面板选择文件，
面板会自动把选中的文件复制到这里）。

支持格式：mp3 / ogg / wav
（flac 多数平台无法被 Unity 实时解码，建议使用 mp3 / ogg / wav）

使用方法：
1. 启动游戏。
2. 在游戏内按 F6（可在 BepInEx 配置中修改）打开「音乐替换」面板。
3. 面板左侧按原声顺序列出全部 53 首 OST，每首右侧有「选择音频文件」按钮。
4. 点击按钮会弹出 Windows 文件选择框并自动定位到本文件夹；选中一个音频后，它会被复制到这里，
   并立即把对应曲目替换为该音频。
5. 映射关系保存在上一级的 mapping.json，下次启动自动生效。

曲目对应关系（编号 = 游戏内 MusicCue.originalMusicTrackNumber）：
 01 Enter Pharloom        02 Moss Grotto          03 Strive
 04 Bone Bottom           05 The Marrow           06 Bell Beast
 07 Repose               08 Deep Docks            09 Lace
 10 Far Fields           11 Fourth Chorus        12 Greymoor
 13 Incisive Battle      14 Bellhart             15 Widow
 16 Shellwood            17 Sister Splinter      18 Hunter's Trail
 19 Sinner's Road        20 Cut Through          21 Bilewater
 22 The Mist             23 Phantom              24 The Slab
 25 Red Maiden           26 Mount Fay            27 Blasted Steps
 28 Last Judge           29 Underworks           30 Choral Chambers
 31 Songclave            32 Cogwork Dancers      33 Cogwork Core
 34 Whispering Vaults    35 Trobbio              36 High Halls
 37 The Choir            38 Awakening            39 Dark Descent
 40 Reprieve             41 Nyleth               42 Skarrsinger Karmelita
 43 Sands of Karak       44 Crust King Khann     45 Lost Verdania
 46 Clover Dancers       47 Fleatopia            48 Tormented Trobbio
 49 Red Memory           50 Last Dive            51 Lost Lace
 52 Sister of the Void   53 Silksong
