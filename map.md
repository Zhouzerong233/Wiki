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
    - easy.bin <!--谱面文件，用难度命名-->
    - expert.bin
    - bg.jpg <!--背景文件，叫什么无所谓-->
  - 98
    - ...
  - 191
    - ...

## 音乐格式

### 音乐

Ogg格式，96kbps，无封面。

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

## 谱面格式

### cheader

```json
{
    //version，谱面版本，每次更新谱面时此属性+1。
    "version": 1,
    //SetID，谱面ID，由服务器分配。
    "sid": 210,
    //MusicID，音乐ID，制谱时调用的音乐ID。
    "mid": 128,
    //author，作者用户名，是在BanGround社区注册的用户的用户名。
    "author": "Bushiroad",
    //authorNick，作者昵称，是作者对应的昵称。
    "authorNick": "ブシロード",
    //difficulty，存储对应难度的难度等级，前端专用。
    "difficulty": {
        "easy": 8,
        "normal": 14,
        "hard": 21,
        "expert": 29,
        "special": 29
    },
    //noteNum，存储对应难度的击打物件数量，前端专用。
    "noteNum": {
        "easy":157,
        "normal":286,
        "hard":501,
        "expert":895,
        "special":935
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
{
    //difficulty，存储当前难度对应的难度名。
    "difficulty": "Expert",
    //level，存储当前难度对应的难度等级。
    "level": 29,
    //offset，存储当前难度的前黑时长，单位为毫秒。
    "offset": 0,
    "notes": [
        {
            //type，物件的类型。type为BPM表示设定音乐的每分钟节拍数.
            "type": "BPM",
            //beat，拍数，物件的所处的拍子。此为一个整数数组储存的带分数，格式为[整数部分,分子,分母]。首物件必为[0,0,1]。
            "beat": [0, 0, 1],
            //value，物件的属性值，此处为BPM的数值。
            "value": 85.0,
            //anims，变速属性，为一个对象数组。此处指定的属性将对整个谱面生效。
            "anims": [{
                //beat，变速的位置，表示速度变化从指定的拍子位置开始。
                "beat": [2, 0, 1],
                //speed，变速的倍率，指定下落速度为正常的多少倍。可以指定为负数，指定为负数时谱面会倒退。
                "speed": 0.75
            }]
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
	    //同上
            "beat": [2, 0, 1],
            //lane，轨道。0≤lane≤6时，表示为普通note，对应第1-7条轨道；lane=-1时，表示为fuwafuwa note，此时将根据x、y属性指定note的位置。
            "lane": 5,
            /*
        		tickStack，节点栈，拥有此属性的物件视为对应滑条的一部分。
	        	tickStack相等的起始、结尾和它们之间的SlideTick，均属于同一滑条。
			也就是每个滑条的唯一编号。
	        	*/
            "tickStack": 0,
            //anims，变速属性，为一个对象数组。此处指定的属性将对单独的note生效。
            "anims": [{
                //beat，指定从哪一拍子开始音符开始变速。注意，此属性大于音符本身的beat时无效。
                "beat": [1, 0, 1],
                //speed，变速的倍率，指定音符下落速度为正常的多少倍。可以指定为负数，指定为负数时音符会倒退。
                "speed": 1.25,
                //lane，目标轨道，表示音符到达的目标轨道，lane为浮点数且0≤lane≤6。使用此属性时请务必注意，此属性仅影响视觉效果，不影响实际判定。
                "lane": 1.5,
                //y，目标高度，表示音符到达的目标高度，y为浮点数且0≤y≤1。使用此属性时请务必注意，此属性仅影响视觉效果，不影响实际判定。
                "y": 1.0
            }],
            //x，仅当lane=-1时生效，指定note的横向位置。x为浮点数且0≤x≤6。
            "x": 0.0,
            //y，仅当lane=-1时生效，指定note的纵向位置。y为浮点数且0≤y≤1。
            "y": 1.0
        }
    ]
}
```

<vssue title="Vssue Demo" />
