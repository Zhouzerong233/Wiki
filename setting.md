# 游戏基础设定

## 评级方式

按照准确率计算

SSS 99.8%

SS 99%

S 97%

A 94%

B 90%

C 85%

D 60%

Failed 60%以下

## 单个Note准确率

Perfect 100%

Great 80%

Good 50%

Bad 20%

Miss 0%

### 计算测试

设*g*为Great数，*m*为Miss数，*n*为物量，*a*为精确度，则可得出以下结论

$$
\frac{m}{n}×0+\frac{g}{n}×0.8+\frac{n-g-m}{n}×1=a
$$

化简得

$$
g=5[(1-a)n-m]\\
m=-0.2g+(1-a)n
$$

#### 谱面物量1000Notes

##### 达到SSS评级的Great数量（FC）

$$
g=5(0.002*1000)=10
$$

990-10-0-0-0

##### 达到SS评级的Great数量（FC）

$$
g=5(0.01*1000)=50
$$

950-50-0-0-0

##### 达到SS评级的Great数量（5Miss）

$$
g=5(0.01*1000-5)=25
$$

970-25-0-0-5

##### 达到S评级的Great数量（FC）

$$
g=5(0.03*1000)=150
$$

850-150-0-0-0

##### 达到S评级的Great数量（10Miss）

$$
g=5(0.03*1000-10)=100
$$

890-100-0-0-10

#### 谱面物量500Notes

##### 达到S评级的Great数量（FC）

$$
g=5(0.03*500)=75
$$

425-75-0-0-0

##### 达到S评级的Great数量（5Miss）

$$
g=5(0.03*500-5)=50
$$

445-50-0-0-5

##### 达到A评级的Great数量（10Miss）

$$
g=5(0.06*500-10)=50
$$

390-100-0-0-10

##### 达到B评级的Great数量（20Miss）

$$
g=5(0.1*500-20)=150
$$

330-150-0-0-20

##### 达到C评级的Great数量（30Miss）

$$
g=5(0.15*500-30)=225
$$

245-225-0-0-30

##### Failed的Miss数量（30%Great）

$$
m>-0.2*\frac{3(500-m)}{10}+0.15*500\\
m>47\frac{41}{47}\approx48
$$

## 得分

满分100W

连击分数：Great及以上连击每100Combo得分+0.5%，Perfect每连击50Combo+0.5%，两者独立计算，最后相叠加。爆出Great后Perfect连击清空，Great连击不断；爆出Great以下的Combo后两个连击都清零。

### 测试计算

谱面物量为501Notes

设基础分数为*x*，则有

51-100Combo得分：

$$
(1+0.005)x
$$

101-150Combo得分：

$$
(1+0.015)x
$$

……

450-500Combo得分：

$$
(1+0.065)x
$$

500Combo后得分：

$$
(1+0.075)x
$$

总分：

$$
50x+50(1+0.005)x+50(1+0.015)x+...+50(1+0.065)x+(1+0.075)x\\ =1,000,000\\
\Rightarrow x \approx 1933.02
$$

算法如下

```javascript
function test (maxCombo) {
    let part = Math.floor(maxCombo / 50);
    let leftCombo = maxCombo - part * 50;
    let lastAddition = 0;
    let addition = 0;
    for (let i = 0; i <= part; i++) {
        let grAddition = Math.floor(i / 2) * 0.005;
        let pAddition = i * 0.005;
        let totalAddition = 1 + grAddition + pAddition;
        if (i === part) {
            lastAddition = totalAddition;
            break;
        }
        console.log(`from \${50*i+1} to \${50*(i+1)} addition ${totalAddition}`);
        addition += totalAddition;
    }
    console.log(addition, lastAddition);
    let score = 1e6 / (50 * addition + lastAddition * leftCombo);
    return score;
}
```

## 判定

60FPS

| Note种类                  | Perfect | Great | Good  | Bad   | Miss                                 |
| ------------------------- | ------- | ----- | ----- | ----- | ------------------------------------ |
| 单点 滑键 直滑条头尾      | -3~+3   | -6~+6 | -7~+7 | -8~+8 | 无动作或点按滑键                     |
| 直滑条尾端滑键 斜滑条头尾 | -4~+4   | -7~+7 | -8~+8 | -9~+9 | 无动作或在有滑键的情况下直接松开滑条 |
| 斜滑条尾端滑键            | 0~+6    | 无    | 无    | 无    | 无动作或直接松开滑条                 |
| 滑条节点                  | 0~+12   | 无    | 无    | 无    | 在判定轨道左右1轨以外                |

<vssue title="Vssue Demo" />