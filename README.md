# 丝之歌音乐替换模组（简单版） / SilkSong Music Replacer Simple

> 版本 **v6.82** · 适用于《空洞骑士：丝之歌》(Hollow Knight: Silksong) · 基于 BepInEx 5 + HarmonyX

> Version **v6.82** · For Hollow Knight: Silksong · Built on BepInEx 5 + HarmonyX

---

## 1. 简介 / Overview

**中文** — 本模组让你把游戏内的音乐替换成自己喜欢的音频，无需修改游戏本体。面板按原声顺序列出全部可替换曲目，每首都能单独选择替换音频、试听、调整音量，并支持把整套配置保存为可移植的预设。

**English** — This plugin lets you replace the game's music with your own audio without touching the game files. The panel lists every replaceable track in original order; each track can be individually replaced, previewed, and volume-tuned, and the whole setup can be saved as a portable preset.

主要能力 / Key capabilities:

- 覆盖游戏音乐：MusicCue 曲目（区域/战斗/环境）+ 场景直接播放的长音乐。
  Covers MusicCue tracks (area/battle/ambient) plus scene-direct-played long music.
- 每曲独立替换、原曲试听、替换试听、重置回原曲。
  Per-track replace, original preview, replacement preview, and reset.
- 自动音量匹配（响度对齐）+ 手动音量倍率（0%–400%）。
  Auto volume matching (loudness alignment) + manual multiplier (0%–400%).
- 多轨叠加抑制，避免同段替换音频多通道叠加爆音。
  Multi-track ducking to prevent summed-loudness clipping.
- 排序切换（OST / 种类 / 音轨）、JSON 预设保存与加载。
  Sort toggle (OST / Type / Tracks) and JSON preset save/load.
- 界面跟随游戏语言（v6.71 / v6.72 本地化）。
  UI follows the game's language (localization added in v6.71 / v6.72).

---

## 2. 安装 / Installation

**中文**

1. 确认已安装 **BepInEx 5**（64 位 / 适用于 Unity Mono）。
2. 把 `SilkSongMusicReplacerSimple` 整个文件夹复制到游戏的 `BepInEx/plugins/` 目录下。
3. 启动游戏，等待首次原曲资源预加载完成（首次稍慢，属正常）。
4. 默认按 **F6** 打开「音乐替换」面板（热键可在 BepInEx 配置文件中修改）。

**English**

1. Make sure **BepInEx 5** (64-bit / Unity Mono) is installed.
2. Copy the whole `SilkSongMusicReplacerSimple` folder into the game's `BepInEx/plugins/` directory.
3. Launch the game and wait for the first-time original-track preload to finish (slower on first run, which is normal).
4. Press **F6** by default to open the music panel (the hotkey can be changed in the BepInEx config file).

目录结构示例 / Example layout:

```
Hollow Knight Silksong/
└─ BepInEx/
   └─ plugins/
      └─ SilkSongMusicReplacerSimple/
         ├─ SilkSongMusicReplacerSimple.dll   # 模组主体 / plugin assembly
         ├─ Music/                             # 替换音频存放文件夹 / replacement audio folder
         │  └─ README.txt
         ├─ mapping.json                       # MusicCue 曲替换映射 / MusicCue replacements
         ├─ direct_mapping.json                # 直接播放曲替换映射 / direct-play replacements
         ├─ manual_volume.txt                  # 每曲手动音量倍率 / per-track manual volume
         └─ README.md
```

---

## 3. 使用方法 / How to Use

### 3.1 打开面板 / Open the panel

**中文** — 在游戏内按 F6；面板标题为「选择替换音乐 / Choose Replacement Music」。顶部提示：游戏内正在播放的曲目无法在本界面操作。

**English** — Press F6 in-game; the panel title is "Choose Replacement Music". Note the top hint: tracks currently playing in-game cannot be edited here.

### 3.2 替换一首曲目 / Replace a track

**中文**

1. 每行左侧 ▶ 试听游戏**原曲**，右侧 ▶ 试听所选**替换文件**。
2. 点击「选择音频文件 / Select File」→ 自动打开 `Music` 文件夹 → 选中音频后自动复制并即时替换。
3. 「重置 / Reset」可恢复游戏原曲。
4. 「调整音量 / Volume」展开音量条（见 3.3）。

**English**

1. ▶ on the left of each row previews the **original** track; ▶ on the right previews the chosen **replacement**.
2. Click **Select File** → the `Music` folder opens → choosing a file copies it and replaces immediately.
3. **Reset** restores the original music.
4. **Volume** expands the volume slider (see 3.3).

### 3.3 音量 / Volume

**中文**

- **自动音量匹配**：检测原曲全声部真实响度与替换曲实测响度，自动把替换曲对齐到相似响度。面板右上角「音量匹配：开/关 / Auto Volume: ON/OFF」可切换，切换即时作用于正在播放/试听的替换音乐。
- **手动倍率**：每行「调整音量 / Volume」展开横向音量条，范围 **0%–400%**（默认 100%，位于 1/4 处，每 100% 一格）。该倍率叠加在自动音量匹配之后，与匹配开关互相独立；开关只改实际音量，不动音量条位置。每曲单独记忆，重启保留。

**English**

- **Auto Volume Matching**: measures the summed loudness of every original layer and the replacement, then aligns the replacement to it. The top-right **Auto Volume: ON/OFF** button toggles it; the change applies instantly to playing/previewed replacement audio.
- **Manual Multiplier**: each row's **Volume** expands a horizontal slider ranging **0%–400%** (default 100% at 1/4, ticks every 100%). This multiplier is applied after auto matching and is independent of the toggle; the toggle only changes actual volume, not the slider position. Remembered per track and kept after restart.

### 3.4 排序 / Sorting

**中文** — 面板右上角排序按钮在 **按OST排序 / 按种类排序 / 按音轨排序**（OST Order / Sort by Type / Sort by Tracks）之间循环；始终显示全部曲目，仅改变排列顺序。

**English** — The top-right sort button cycles between **OST Order / Sort by Type / Sort by Tracks**. All tracks are always shown; only the order changes.

### 3.5 顶部 / 底部按钮 / Top & bottom buttons

**中文**

- **点击穿透（顶部，音量匹配左侧）**：开关面板与下层游戏界面的鼠标点击关系，**默认开启**。开启时面板半透明（0.85）、鼠标点击会穿透到面板下层的游戏界面；关闭时**仅面板内部**不透明度调至 100%（外部满屏遮罩恒定 0.55 不变），并通过 Harmony 前缀让游戏 `EventSystem.RaycastAll` 返回空命中集，使 uGUI 按钮收不到 pointer 事件 —— 点击不再落到面板后的游戏按钮上。该拦截是**非破坏性**的：不改动 `EventSystem` 组件的任何状态，开启穿透或关闭面板时前缀直接放行，游戏 UI 立即恢复。模组面板本身是 IMGUI、不依赖 `EventSystem`，按钮 / 滑块 / 列表在两种状态下都能正常操作。
- **重置全部（底部，关闭左侧）**：对所有曲目（除正在游戏内播放的曲目外）一次性重置、恢复游戏原曲。点击后按钮文本变红为「确认重置全部」，再次点击才真正执行；任意时刻关闭面板即取消待确认状态。

**English**

- **Click-Through (top, left of Volume Match)**: toggles whether mouse clicks reach the game UI underneath the panel; **on by default**. When on, the panel is semi-transparent (0.85) and clicks pass through to the game UI below; when off, only the panel interior becomes 100% opaque (the external dimmer stays constant at 0.55) and a Harmony prefix makes the game's `EventSystem.RaycastAll` return an empty hit set, so uGUI buttons receive no pointer events and clicks no longer reach buttons behind the panel. The block is **non-destructive**: it never changes any `EventSystem` component state, and the prefix simply lets calls through when Click-Through is on or the panel is closed, so the game UI recovers instantly. The mod panel itself is IMGUI and does not depend on `EventSystem`, so its buttons / sliders / list stay fully operable in both states.
- **Reset All (bottom, left of Close)**: resets all tracks except the one currently playing in-game, restoring the game's original music. The first click turns the label red to "Confirm Reset All"; a second click performs the reset. Closing the panel at any time cancels the armed state.

### 3.6 预设 / Presets

**中文**

- **保存预设 / Save Preset**：把当前配置（音量匹配开关、已选替换文件名、每曲手动音量）保存为可编辑的 JSON 预设；会弹出保存窗口，可修改预设文件名。
- **加载预设 / Load Preset**：读取 JSON 预设并还原配置。预设中指向 `Music` 文件夹里不存在的音频会被跳过、默认不替换；未列出的曲目恢复为游戏原曲、手动音量回到 100%。
- **跨机器可移植**：替换文件统一按相对 `Music` 文件夹的路径保存（支持子文件夹），自动剥离他人机器的安装路径前缀，旧预设纯文件名会按 `Music` 目录树兜底检索。

**English**

- **Save Preset**: saves the current setup (auto-volume toggle, replacement filenames, per-track manual volume) as an editable JSON preset; a save dialog opens so you can edit the filename.
- **Load Preset**: reads a JSON preset and restores the setup. Tracks whose preset audio is missing from the `Music` folder are skipped and left unreplaced; tracks not listed revert to the original music with manual volume back to 100%.
- **Portable across machines**: replacement files are stored by paths relative to the `Music` folder (subfolders supported), stripping other machines' install-path prefixes; legacy presets with bare filenames are resolved against the `Music` folder tree.

---

## 4. 支持的音频格式 / Supported Formats

**中文** — 替换音频支持 **mp3 / ogg / wav**。flac 等格式多数平台无法被 Unity 实时解码，建议使用上述三种。

**English** — Replacement audio supports **mp3 / ogg / wav**. Formats like flac generally cannot be decoded by Unity at runtime, so one of the three above is recommended.

（文件选择框的过滤器、解码器与预设索引三处均只识别 mp3/ogg/wav。）

(The file dialog filter, the decoder selection, and the preset index all accept only mp3/ogg/wav.)

---

## 5. 曲目列表 / Track List

**中文** — 面板左侧按原声顺序列出全部 53 首官方 OST，每首对应编号即游戏内 `MusicCue.originalMusicTrackNumber`：

**English** — The left side of the panel lists all 53 official OST tracks in original order; each number equals the in-game `MusicCue.originalMusicTrackNumber`:

```
 01 Enter Pharloom       02 Moss Grotto         03 Strive
 04 Bone Bottom          05 The Marrow          06 Bell Beast
 07 Repose              08 Deep Docks           09 Lace
 10 Far Fields           11 Fourth Chorus       12 Greymoor
 13 Incisive Battle      14 Bellhart            15 Widow
 16 Shellwood            17 Sister Splinter     18 Hunter's Trail
 19 Sinner's Road        20 Cut Through         21 Bilewater
 22 The Mist             23 Phantom             24 The Slab
 25 Red Maiden           26 Mount Fay           27 Blasted Steps
 28 Last Judge           29 Underworks          30 Choral Chambers
 31 Songclave            32 Cogwork Dancers     33 Cogwork Core
 34 Whispering Vaults    35 Trobbio             36 High Halls
 37 The Choir            38 Awakening           39 Dark Descent
 40 Reprieve             41 Nyleth              42 Skarrsinger Karmelita
 43 Sands of Karak       44 Crust King Khann    45 Lost Verdania
 46 Clover Dancers       47 Fleatopia           48 Tormented Trobbio
 49 Red Memory           50 Last Dive           51 Lost Lace
 52 Sister of the Void   53 Silksong
```

**中文** — 此外，面板还包含若干「直接播放」长音乐（如片尾曲、花絮等，替换走 `direct_mapping.json`），以及由 Chapel 拆分出的 **Chapel**（区域曲）与 **Chapel Action**（战斗声部）两个可独立替换的条目。

**English** — In addition, the panel also contains several direct-play long music tracks (credits, etc., replaced via `direct_mapping.json`), plus **Chapel** (area track) and **Chapel Action** (battle layer) split from Chapel as two independently replaceable entries.

---

## 6. 多语言 / Localization

**中文（v6.71 / v6.72）**

- 模组读取游戏的 `TeamCherry.Localization.Language.CurrentLanguage()`。
- **简体中文 / 繁体中文**（ZH*）：界面沿用模组原有中文文案。
- **英文及其他语言**：界面显示 `Loc.EN` 表中的英文译文。
- 在游戏内切换语言时，模组会重建全部静态文案缓存，无需重启。
- 曲目**名称（MusicCue Key）**与**通道角色**属于曲目内容，保持中文原文，由你自行决定是否翻译。
- 曲目的**运用位置**已随游戏语言切换（中文显示表内中文，其它语言显示英文）。

**English (v6.71 / v6.72)**

- The plugin reads the game's `TeamCherry.Localization.Language.CurrentLanguage()`.
- **Simplified / Traditional Chinese** (ZH*): the UI keeps the mod's original Chinese text.
- **English and other languages**: the UI shows the English translations from the `Loc.EN` table.
- Switching language in-game rebuilds all cached static text, so no restart is needed.
- Track **names (MusicCue Key)** and **channel roles** are track content and stay in Chinese; you decide whether to translate them.
- A track's **in-game usage location** already follows the game language (Chinese in ZH*, English otherwise).

---

## 7. 文件与配置 / Files & Config

| 文件 / File | 说明 / Purpose |
|---|---|
| `Music/` | 替换音频存放文件夹 / replacement audio folder |
| `mapping.json` | MusicCue 曲替换映射 / MusicCue replacements |
| `direct_mapping.json` | 直接播放曲替换映射 / direct-play replacements |
| `manual_volume.txt` | 每曲手动音量倍率（曲名=倍率）/ per-track manual multiplier (TrackName=Multiplier) |
| `music_order.txt` / `ost_order.txt` | 排序参考顺序 / sort reference orders |
| `cue_clips.txt` / `cue_audio.txt` / `orig_loudness.txt` | 原曲通道与响度数据 / original clip & loudness data |
| BepInEx `config` 文件 | 热键、自动音量强度、增益微调、多轨衰减等 / hotkey, auto-volume strength, gain trim, multi-track attenuation, etc. |

部分高级参数（自动音量强度、目标响度微调 dB、多轨衰减量 dB）修改后需**重启游戏**生效；热键与匹配开关可实时切换。

Some advanced parameters (auto-volume strength, target loudness trim in dB, multi-track attenuation in dB) require a **game restart** after editing; the hotkey and the match toggle can be switched live.

---

## 8. 已知限制 / Known Limitations

- flac / m4a / wav 外的非常见格式不被识别。
  Uncommon formats beyond mp3/ogg/wav are not recognized.
- 多轨替换时，非主音轨会被压到极低音量（多轨叠加抑制），这是预期行为。
  During multi-track replacement, non-main channels are ducked to a very low volume (multi-track ducking) — by design.
- 首次启动需预加载原曲资源，面板试听略慢；进入对应区域后由游戏自行加载。
  First launch preloads original assets, so previews are slower initially; the game loads them itself once you enter the area.

---

## 9. 版本历史（要点）/ Changelog (highlights)

- **v6.54–v6.70**：性能与每帧分配优化、FSM 曲替换修复、手动音量扩展到 400% 并由音频数据层真实放大、标题曲调误放大修复、Chapel Action 替换修复、OnGUI 每帧分配优化。
  Performance & per-frame allocation optimizations, FSM-track replacement fixes, manual volume extended to 400% with real audio-data-layer amplification, Title-track mis-amplification fix, Chapel Action fix, OnGUI allocation optimizations.
- **v6.71**：界面本地化框架——UI 文本跟随游戏语言，简繁中沿用中文、其它语言显示英文。
  Localization framework — UI text follows the game language; ZH* keeps Chinese, other languages show English.
- **v6.72**：曲目运用位置本地化——`TrackInfo.Location` 更新为用户修订后的中文，并在 `Loc.EN` 新增 89 条「中文→英文」映射，运用位置随游戏语言切换。
  Track usage-location localization — `TrackInfo.Location` updated to user-revised Chinese, with 89 new Chinese→English mappings in `Loc.EN`; usage location now follows the game language.
- **v6.73**：修复「重置」按钮串曲 bug——`RestoreOriginals` 把替换曲即时切回原声时，原先按 `MR_` 前缀误判会把其它正在播放的替换曲（同属 MR_ 前缀）也改写成被重置曲的原声快照，导致被重置曲的音乐直接在游戏内播放并覆盖当前音乐；改为仅匹配被重置曲自身的替换 clip 名（MR_<曲名>）。同时把被重置曲已加载的 MusicCue 资产通道 clip 还原回原声快照，使重置对常驻/预加载资产也永久生效。
  Fixed a "Reset" button cross-track bug — when `RestoreOriginals` switched the replacement back to the original, the old `MR_`-prefix check wrongly rewrote other playing replacements (also MR_-prefixed) with the reset track's original snapshot, making the reset track play in-game and override the current music; now it only matches the reset track's own replacement clip name (MR_<track>). Also reverts the reset track's loaded MusicCue asset channels to the original snapshot so the reset sticks for resident/preloaded assets.
- **v6.74**：音乐界面弹出 / 关闭动画——唤出时面板从屏幕下边缘外向上移动至目标位置、大小由小变大（ease-out-cubic，约 0.25s）；关闭时反向沉回屏幕下方之外。不做淡入；满屏遮罩层不跟随变换。仅 `Plugin.cs` 局部改动，不影响替换 / 试听 / 预设 / 本地化等核心逻辑。
  Music panel open/close animation — on open the panel slides up from below the screen bottom edge into place while scaling up from small to large (ease-out-cubic, ~0.25s); on close it reverses and sinks back below the screen. No fade-in; the full-screen dimmer layer is not transformed. Localized change in `Plugin.cs` only; does not affect replacement / preview / preset / localization logic.
- **v6.75**：音乐界面两项新控件——①新增「点击穿透」开关（位于「音量匹配」左侧，默认开启）：开启时面板半透明、鼠标点击穿透到面板下层的游戏界面；关闭时仅将面板内部不透明度调至 100%（面板变实），外部遮罩不受影响、不拦截点击。右上角「音量匹配」「排序」两按钮收窄让位。②新增「重置全部」按钮（右下角「关闭」左侧）：首次点击按钮文本变红为「确认重置全部」，再次点击即对全部曲目（除正在播放的曲目外）执行重置、恢复游戏原曲。
  Two new panel controls — ① Added a "Click-Through" toggle (left of "Volume Match", on by default): when on, the panel is semi-transparent and mouse clicks pass through to the game UI underneath; when off, only the panel's own opacity is set to 100% (panel becomes solid) — the external dimmer and outside clicks are unaffected. The top-right "Volume Match" and "Sort" buttons were narrowed to make room. ② Added a "Reset All" button (left of "Close", bottom-right): first click turns the label red to "Confirm Reset All"; a second click resets all tracks except the one currently playing, restoring the game's original music.
- **v6.76**：音乐界面开 / 关动画丝滑化——① 进度推进由匀速改为 `Mathf.SmoothDamp`（临界阻尼、无过冲），起步与收尾速度趋零、中段顺滑，消除原 ease-out-cubic 的「窜出」感；② 满屏遮罩不再硬切，改为随动画进度 `0.55×e` 淡入 / 淡出（恒定 0.55，不受点击穿透开关影响），开界面渐暗、关界面渐亮；③ 面板框不透明度同样随进度淡入 / 淡出（点击穿透开启 0→0.85、关闭 0→1），消除「啪」地满不透明弹出；④ 动画时长由 0.25s 略延长至 0.30s，更从容。仅 `Plugin.cs` 局部改动，不影响替换 / 试听 / 预设 / 本地化等核心逻辑。
  Silky open/close animation — ① progress now uses `Mathf.SmoothDamp` (critically damped, no overshoot) instead of constant speed, so velocity eases to zero at both ends with a smooth mid-phase, removing the old ease-out-cubic "jolt"; ② the full-screen dimmer no longer hard-cuts but fades in/out with progress (`0.55×e`): constant 0.55 regardless of the click-through toggle; ③ the panel frame opacity also fades with progress (0→0.85 / 0→1), removing the instant full-opacity pop; ④ duration nudged from 0.25s to 0.30s for a calmer feel. Localized change in `Plugin.cs` only; does not affect replacement / preview / preset / localization logic.
- **v6.77**：修复「点击穿透关闭后无法操作 UI」——v6.75/6.76 在关闭点击穿透时把满屏遮罩设为 1.0（整屏黑屏）并在面板之上盖一层全屏隐形按钮拦截所有点击，导致面板自身按钮被一并挡死、且外部被强制黑屏。改为：① 满屏遮罩恒定 0.55，不受点击穿透开关影响（外部不再变黑、不再拦截）；② 彻底移除全屏拦截按钮，面板恢复完全可操作；③ 仅保留面板内部不透明度切换：开启 0.85（半透明、可见下层游戏）、关闭 1.0（面板变实）。仅 `Plugin.cs` 局部改动，不影响替换 / 试听 / 预设 / 本地化等核心逻辑。
  Fixed "UI becomes inoperable when Click-Through is off" — in v6.75/6.76, turning Click-Through off set the full-screen dimmer to 1.0 (whole screen black) and overlaid an invisible full-screen button that blocked all clicks, which also killed the panel's own buttons and force-blackened the outside. Now: ① the dimmer is constant 0.55 regardless of the toggle (outside no longer blackens or blocks); ② the full-screen blocking button is removed, so the panel is fully operable again; ③ only the panel's internal opacity toggles: 0.85 when on (semi-transparent, see-through to the game), 1.0 when off (panel solid). Localized change in `Plugin.cs` only; does not affect replacement / preview / preset / localization logic.
- **v6.78**：修正「点击穿透关闭后仍能点到屏幕后内容 / 面板不透明度不为 100%」——① 根因：Unity 默认 `GUI.Box` 背景纹理自带半透明，旧实现即使 alpha 设 1.0 面板仍透出下层游戏，故改用**实心填充矩形**作面板背景，其 alpha 由开关控制（关闭 = 1.0 真·100% 不透明、开启 = 0.85 半透明可透出下层），外部遮罩仍恒定 0.55 不受影响；② 拦截范围由「全屏」收紧为**仅面板矩形内**的隐形按钮（关闭时面板区域内拦截点击、不再穿透到游戏内按钮，但面板自身按钮绘制其上仍可操作，面板外点击依旧穿透到游戏）；③ 同步修正配置项 / 状态提示 / 本地化英文里遗留的「拦截全部点击（模态）」措辞。仅 `Plugin.cs` + `Loc.cs` 改动，不影响替换 / 试听 / 预设 / 本地化等核心逻辑。
  Fixed "clicks still reach behind the panel / panel not 100% opaque when Click-Through is off" — ① root cause: Unity's default `GUI.Box` background texture is inherently semi-transparent, so the old panel stayed see-through even at alpha 1.0; now the panel background is a solid filled rectangle whose alpha is controlled by the toggle (off = 1.0 true 100% opaque, on = 0.85 translucent so the game shows through), while the external dimmer stays constant 0.55; ② the click-blocker is narrowed from full-screen to the panel rectangle only; ③ the stale "all clicks captured (modal)" wording in the config description / status message / English localization is corrected. Only `Plugin.cs` + `Loc.cs` changed; does not affect replacement / preview / preset / localization logic.
- **v6.79**：修正「v6.78 关闭点击穿透后面板内按钮仍点不动」——根因：v6.78 把全面板拦截 `GUI.Button` 画在了**所有内容控件之前（底层）**，而 `GUI.Button` 在 `MouseDown` 会抢占 `GUIUtility.hotControl` 并 `Use()` 掉事件，导致后面的面板按钮永远拿不到 `hotControl`、点击无效。修复：把拦截按钮**移到全部内容控件之后（最上层）**再绘制——此时内容按钮已在 `MouseDown` 先抢到 `hotControl`，拦截按钮见 `hotControl` 已被占便跳过，面板内按钮恢复可用；仅当点击落在面板空白区（内容均未被命中）时拦截按钮才接管，从而拦住向游戏下层界面的点击穿透。同时**降低面板边框亮度**（由 `0.55,0.65,0.85` 调至 `0.30,0.36,0.46`）。仅 `Plugin.cs` 局部改动。
  Fixed "panel buttons still unresponsive when Click-Through is off (v6.78 regression)" — root cause: v6.78 drew the full-panel blocking `GUI.Button` *before* (underneath) all content controls, and because `GUI.Button` claims `GUIUtility.hotControl` and consumes the event on `MouseDown`, the panel's own buttons drawn afterwards could never become hot and were dead. Fix: move the blocking button to be drawn *after* (on top of) all content controls — now content buttons claim `hotControl` first, the blocker sees it already taken and skips, so in-panel buttons work again; only clicks on empty panel areas (no content hit) are captured by the blocker, stopping pass-through to the game underneath. Also lowered the panel border brightness (`0.55,0.65,0.85` → `0.30,0.36,0.46`). Localized change in `Plugin.cs` only.

- **v6.80**（该版停用 EventSystem 的做法已在 v6.81 撤销，保留作历史记录）：尝试修复「点击穿透关闭后仍可以点到面板后的游戏按钮」——**根因**：游戏 UI 是 uGUI（Canvas / `EventSystem`），而本模组面板是 IMGUI（`OnGUI` / `GUI.Button`），这是两套互相独立的输入系统；此前 v6.78/6.79 用 IMGUI 的 `GUI.Button` 在面板上铺拦截层，只能影响 IMGUI 事件队列（还因此误伤了面板自身按钮），**根本拦不住 uGUI 的游戏按钮**。修复：删掉这层无效的 IMGUI 拦截按钮，改为在「面板打开 且 点击穿透关闭」时于 `Update` 中停用游戏 `EventSystem.current`（uGUI 输入总闸）——游戏 uGUI 收不到任何指针输入，面板后的按钮自然点不到；模组面板走 IMGUI、不依赖 `EventSystem`，按钮 / 滑块 / 列表照常可用。开启点击穿透或关闭面板时自动恢复：因 `EventSystem.OnDisable()` 会把静态 `EventSystem.current` 置为 `null`，故缓存被禁用实例的引用 `esDisabledRef` 来恢复（而非再取 `current`）；只恢复自己禁用过的实例（不干扰游戏自身主动禁用、兼容场景切换后新实例，游戏若自行重新启用则再次禁用），`OnDestroy` 兜底恢复避免插件卸载后游戏界面永久失灵。配套：两工程 `.csproj` 新增 `UnityEngine.UI.dll` 引用（`EventSystem` 所在程序集）；配置项说明 / 状态提示 / 英文本地化文案同步改为「停用游戏界面输入」。仅影响点击拦截链路，不改动替换 / 试听 / 预设 / 音量逻辑。
  Attempted fix (the EventSystem-disabling approach was reverted in v6.81; kept for history) for "game buttons behind the panel are still clickable when Click-Through is off" — **root cause**: the game UI is uGUI (Canvas / `EventSystem`) while the mod panel is IMGUI (`OnGUI` / `GUI.Button`), two independent input systems; the v6.78/6.79 approach of laying an IMGUI `GUI.Button` blocker over the panel only affected the IMGUI event queue (and even broke the panel's own buttons) and could never stop uGUI game buttons. Fix: removed that ineffective IMGUI blocker; instead, while the panel is open and Click-Through is off, `Update` disables the game's `EventSystem.current` (the uGUI input gate) — game uGUI receives no pointer input, so buttons behind the panel cannot be clicked, while the IMGUI mod panel stays fully operable. It is automatically restored when Click-Through is turned back on or the panel closes; since `EventSystem.OnDisable()` sets the static `EventSystem.current` to `null`, the disabled instance is cached in `esDisabledRef` and restored from that reference (not from `current`). Only instances disabled by the mod are restored (no interference with the game's own disabling, robust to new `EventSystem` objects after scene changes; re-disabled if the game re-enables it), and `OnDestroy` restores it as a fallback so the game UI is never left dead after plugin unload. Also: both `.csproj` files now reference `UnityEngine.UI.dll` (the assembly containing `EventSystem`), and the config description / status messages / English localization were updated accordingly. Only the click-blocking path changed; replacement / preview / preset / volume logic is untouched.

- **v6.81**：修复「v6.80 点击穿透开启后仍点不到下层按钮 / 关闭面板后游戏完全无法操作」——**根因**：v6.80 用 `EventSystem.enabled=false` 来拦截点击，这是**破坏性**的：`enabled=false` 会触发 `OnDisable() → DeactivateModule()`，而重新 `enabled=true` 后输入模块**不会自动重新激活**，于是即便恢复组件开关，游戏 UI 依然失灵；这既影响了「点击穿透开启」状态，也让关闭面板后游戏永久无法操作。修复：**彻底移除**所有 EventSystem 状态操作（删除 `esDisabledRef` 字段、`Update` 中的停用/恢复块、`OnDestroy` 兜底），改为**非破坏性的 Harmony 前缀拦截** —— 新增 `Patch_UiRaycastBlock`，在 `Awake` 里手动挂载到 `EventSystem.RaycastAll(PointerEventData, List<RaycastResult>)`（单独 try/catch，签名差异不影响其它补丁）；仅当「面板打开 且 点击穿透关闭」时把命中集清空并返回 `false` 跳过射线检测，uGUI 按钮收不到 pointer 事件即点不到。**全程不触碰 EventSystem 组件的任何状态**，开启穿透或关闭面板时前缀直接 `return true` 放行，游戏 UI 立即恢复正常，压根不存在「恢复」环节。已验证 `RaycastAll` 是旧 `StandaloneInputModule` 与新 `InputSystemUIInputModule` 共用的命中检测入口（`UnityEngine.UI.dll` 定义、`Assembly-CSharp.dll` 10 处调用、`Unity.InputSystem.dll` 1 处调用），故两条输入路径一并覆盖；模组面板是 IMGUI、不经过 RaycastAll，按钮/滑块/列表始终可用。配套：配置项说明 / 状态提示 / 英文本地化文案同步改为「拦截游戏界面点击」。仅影响点击拦截链路，不改动替换 / 试听 / 预设 / 音量逻辑；`UnityEngine.UI.dll` 引用保留（`EventSystem` / `PointerEventData` / `RaycastResult` 类型所需）。
  Fixed "with Click-Through ON the buttons below the panel are still unclickable / after closing the panel the game becomes completely inoperable" (v6.80 regression) — **root cause**: v6.80 blocked clicks by setting `EventSystem.enabled=false`, which is destructive: it fires `OnDisable() → DeactivateModule()`, and setting `enabled=true` back does **not** automatically reactivate the input module, so the game UI stays dead even though the component is re-enabled. That broke both the Click-Through ON state and the game after the panel was closed. Fix: **removed all EventSystem state manipulation** (deleted the `esDisabledRef` field, the disable/restore block in `Update`, and the `OnDestroy` fallback) and replaced it with a **non-destructive Harmony prefix** — new `Patch_UiRaycastBlock`, manually attached in `Awake` to `EventSystem.RaycastAll(PointerEventData, List<RaycastResult>)` with its own try/catch so a signature mismatch cannot affect the other patches. Only while the panel is open and Click-Through is off does it clear the hit list and return `false` to skip the raycast, so uGUI buttons receive no pointer events. **No `EventSystem` component state is ever modified**; when Click-Through is turned on or the panel closes the prefix simply returns `true` and the game UI works again immediately — there is no "restore" step at all. Verified that `RaycastAll` is the shared hit-test entry for both the legacy `StandaloneInputModule` and the new `InputSystemUIInputModule` (defined in `UnityEngine.UI.dll`, 10 call sites in `Assembly-CSharp.dll`, 1 in `Unity.InputSystem.dll`), so both input paths are covered; the IMGUI mod panel never goes through RaycastAll and its buttons / sliders / list remain fully operable. Also updated the config description / status messages / English localization to "game UI clicks are blocked". Only the click-blocking path changed; replacement / preview / preset / volume logic is untouched. The `UnityEngine.UI.dll` reference is kept (needed for `EventSystem` / `PointerEventData` / `RaycastResult`).

- **v6.82**：曲目拆分 —— 将组合曲「猎者小径区域曲+战斗曲」（游戏内 Cue `Hunters Trail`，含区域 Main 与战斗 Action 两条声道）按用户要求拆成两个可独立替换的单轨条目：①「猎者小径」（沿用原顺序位，对应通道 0 = `H82 Hunters Trail v4-47 MAIN` 区域曲）；②「猎者小径遭遇战」（紧接其后并排，对应通道 1 = `H82 Hunters Trail v4-47 ACTION` 战斗声部）。复用 v6.59 的 Chapel 拆分范式：`SplitTracks` 增加 `{ "Hunters Trail", Channel=0 }` 与 `{ "Hunters Trail Battle", Channel=1 }`，`SplitParents` 保持为空使父曲仍显示在列表原位（两行互不覆盖）；`TrackInfo.cs` 的 `Location` 把父曲改名为「猎者小径」并新增「猎者小径遭遇战」，`Category` 为后者补 `BattleNonBoss`，并按 Chapel 先例将 `ChannelCount`/`ChannelRoles` 中 Hunters Trail 的多轨标注移除；`Loc.cs` 中英键同步更新。两份 `music_order.txt`（主程序 + Steam 1.03）均在 `Hunters Trail` 后插入 `Hunters Trail Battle` 使其并排。替换 / 试听 / 预设逻辑不变，不影响点击穿透等其它功能。
  Split a combined track — "Hunters Trail" (game Cue `Hunters Trail`, containing an area "Main" channel and a battle "Action" channel) is now split into two independently replaceable single-track entries per user request: ① "猎者小径" (area, channel 0, stays at the original order slot) and ② "猎者小径遭遇战" (battle, channel 1, inserted right after it). Reuses the v6.59 Chapel split pattern: `SplitTracks` gains `{ "Hunters Trail", Channel=0 }` and `{ "Hunters Trail Battle", Channel=1 }`, with `SplitParents` left empty so the parent cue still shows at its original slot; `TrackInfo.cs` renames the parent to "猎者小径" and adds "猎者小径遭遇战" in `Location`, adds `BattleNonBoss` for the battle entry in `Category`, and (following the Chapel precedent) removes Hunters Trail's multi-track annotations from `ChannelCount`/`ChannelRoles`; `Loc.cs` EN/CH keys updated. Both deployed `music_order.txt` files insert `Hunters Trail Battle` right after `Hunters Trail`. Replacement / preview / preset logic unchanged; other features (e.g. Click-Through) unaffected.

完整变更记录见游戏内启动日志（含 `[MusicReplacer build=v6.82]` 标记）。
Full history is in the in-game startup log (tagged `[MusicReplacer build=v6.82]`).
