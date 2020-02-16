# 谱面格式&导入包结构

## 导入包（kirapack）结构

假设玩家在社区选取了3个谱面集进行下载，其中：

> * 3个谱面集的ID（sid）分别为10、98、191；
> * ID为10、98的谱面集调用的是音乐ID（mid）是11；
> * ID为191的谱面集调用的音乐ID是45。

- music
  - 11 <!--mid命名的文件夹-->
    - 11.ogg <!--mid命名的音乐文件-->
    - mheader.bin <!--音乐对应的header，存储音乐信息、默认预览时间-->
  - 45
    - 45.ogg
    - mheader.bin

- chart
  - 10 <!--sid命名的文件夹-->
    - cheader.bin <!--谱面集对应的header，存储调用的mid、作者、tag等-->
    - easy.bin <!--谱面文件，叫什么无所谓-->
    - expert.bin
    - bg.jpg <!--背景文件，叫什么无所谓-->
  - 98
    - ...
  - 191
    - ...

## 音乐格式

### 音乐

Ogg格式，64kbps，无封面。

### mheader

```json
{
    //MusicID，音乐ID，由服务器分配。
    "mid": 128,
    //歌曲标题。
    "title": "六兆年と一夜物語",
    //歌曲艺术家。
    "artist": "Roselia",
    //preview，预览时间，单位为秒，默认的预览区间，在chart未设定此值时会应用的默认值。
    "preview": [57.850, 78.124],
    //BPM，每分钟节拍数。用于参考的歌曲信息，值为主要BPM，由上传者填写。
    "BPM": [85, 186],
    //length，歌曲长度。单位为秒，自动生成。
    "length": 103.808
}
```

## 谱面集格式

### cheader

```json
{
    //version，谱面版本，每次更新谱面时此属性+1。
    version: 1,
    //SetID，谱面集ID，由服务器分配。
    "sid": 210,
    //MusicID，音乐ID，制谱时调用的音乐ID。
    "mid": 128,
    //author，作者用户名，是在BanGround社区注册的用户的用户名。
    "author": "Bushiroad",
    //authorNick，作者昵称，是作者对应的昵称。
    "authorNick": "ブシロード",
    //difficulty，存储对应难度的难度等级
    "difficulty": {
        "easy": 8,
        "normal": 14,
        "hard": 21,
        "expert": 29,
        "special": 29
    },
    //backgroundFile，背景文件，若设置了pic属性，则会在Select和Ingame界面显示指定的图片为背景；若设置了vid属性，则Ingame默认显示指定的视频为背景
    "backgroundFile": {
        "pic": "bg.jpg",
        "vid": "bg.mp4"
    },
    //preview，预览时间，单位为秒，会循环在Select界面播放。
    "preview": [57.850, 78.124],
    //tag，谱面标签，可以基于tag搜索谱面。
    "tag": [
        "Six",
        "trillion",
        "years",
        "and",
        "one",
        "night",
        "story"
    ]
}
```

### chart

```json
[
    {
        //type，物件的类型。type为BPM表示设定音乐的每分钟节拍数.
        "type": "BPM",
        //beat，物件的位置，是一个带分数，格式为[整数部分,分子,分母]。首物件必为[0,0,1]。
        "beat": [0,0,1],
        //value，物件的属性值，此处为BPM的数值。
        "value": 85.0,
        ]
    },
    {
        /*
        type的值为：
        Single，表明此物件为单键（亦可能为滑条起始）；
        Flick，表明此物件为滑键（亦可能为滑条结尾）；
        SlideTick，表明此物件为滑条节点；
        SlideTickEnd，表明此物件为滑条结尾。
        */
        "type": "Single",
        "beat": [2,0,1],
        //lane，轨道，范围为0≤lane≤6，对应第1至7条轨道。
        "lane": 5,
        /*
        tickStack，节点栈，拥有此属性的物件视为对应滑条的一部分。
        type的值为：
        Single，表明此物件为滑条起始；
        SlideTick，表明此物件为滑条节点；
        Flick或SlideTickEnd，表明此物件为滑条结尾。
        tickStack相等的起始、结尾和它们之间的SlideTick，均属于同一滑条。
        */
        "tickStack": 0
    }
]
```

<vssue title="Vssue Demo" />
