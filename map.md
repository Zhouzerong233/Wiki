# 谱面格式

## 歌曲Header

```json
{
    // 歌曲id
    "id": 1,
    // 歌曲名（仅限英文）
	"title": "kimi ni furete",
	"artist": "riko azuna",
    // Unicode歌曲名
	"titleUnicode": "君にふれて",
    // Unicode歌手
	"artistUnicode": "安月名莉子",
    // 背景图片地址
    "background": "background.jpg",
    // 歌曲封面地址
    "cover": "cover.jpg",
    // 歌曲预览区间
	"preview": [
		49.447, // 开始时间
		70.599 // 结束时间
	]
}
```

## 谱面信息

```json
{
    // 对应歌曲id
    "mid": 1,
    // 谱面作者（仅限英文）
	"author": "qing fu",
    // Unicode谱面作者
	"authorUnicode": "青芙",
    // 背景
    "backgroundFile": {
        // 背景图片（留空可使用默认背景）
        image: "background.jpg",
        // 背景视频（非必需，如填写可供用户选择）
        video: "background.mp4"
    },
    // 难度
	"difficulty": "Hard",
    // 等级
	"level": 16,
    "notes": [
        {
            // 类型为设置bpm
            "type": "BPM",
            // 开始节奏
            "beat": [0, 0, 1],
            // bpm值
			"value": 90
        },
        {
            /**
             * note类型：
             * Single 单点或滑条开端
             * Flick 单滑键或滑条结尾滑键
             * SlideTick 滑条节点
             * SlideTickEnd 滑条结尾
             */
			"type": "Single",
            /**
             * 所在节奏，用带分数表示
             * 第一个元素为整数部分，第二个元素为分子部分，第三个元素为分母部分
             * 如以下示例表示第2.5个节拍
             */
			"beat": [2, 1, 2],
            // 所在轨道 0-6
			"lane": 5
            /**
             * 有此属性的代表note属于滑条
             * 如果type为Single，则为滑条开端
             * 如果type为SlideTick，则为滑条节点
             * 如果type为Flick或SlideTickEnd，则为滑条末端
             */
            "tickStack": 0
		}
    ]
}
```

<vssue title="Vssue Demo" />