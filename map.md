# 目录结构&谱面格式

## 目录结构

* ChartSet

  * Music
  
    * 1.ogg <音乐文件>
    * 1.bin <音乐header文件>
    
    * 2.ogg
    * 2.bin
    
    * 3.ogg
    * 3.bin
    * ...

  * Chart

    * 1
      * easy.bin <谱面文件>
      * normal.bin
      * hard.bin
      * expert.bin
      * special.bin
      
      * bg.jpg <背景图片文件>
      * bg.mp4 <视频文件>

    * 2
      * easy.bin
      * normal.bin
      * hard.bin
      * expert.bin
      * special.bin
      
      * bg1.jpg
      * bg2.jpg
      * bg.mp4
      
    * ...

## 谱面格式

### 歌曲Header

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
}
```

### 谱面信息

```json
{
    //version，谱面格式版本，用于区分不同版本的谱面格式。
    "version": 1,
    //ChartID，谱面ID，由服务器分配。
    "cid": 512,
    //MusicID，音乐ID，制谱时调用的音乐ID。
    "mid": 128,
    //author，作者用户名，是在BanGround社区注册的用户的用户名。
    "author": "Bushiroad",
    //authorNick，作者昵称，是作者对应的昵称。
    "authorNick": "ブシロード",
    //difficulty，难度名，目前只支持Easy、Normal、Hard、Expert、Special。
    "difficulty": "Expert",
    //level，难度等级，由谱师自行设定。（也有可能会被Verifier改掉？）
    "level": 29,
    //backgroundFile，背景文件，若设置了pic属性，则会在Select和Ingame界面显示指定的图片为背景；若设置了vid属性，则Ingame默认显示指定的视频为背景。
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
    //notes，谱面物件。
    "notes": [
        {
            //type，物件的类型。type为BPM表示设定音乐的每分钟节拍数.
            "type": "BPM",
            //beat，物件的位置，是一个带分数，格式为[整数部分,分子,分母]。首物件必为[0,0,1]。
            "beat": [0,0,1],
            //value，物件的属性值，此处为BPM的数值。
            "value": 85.0,
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
}
```

<vssue title="Vssue Demo" />
