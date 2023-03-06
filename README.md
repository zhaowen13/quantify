# 量化模型
##  一.多因子选股
估值，成长，质量，流动性，规模，宏观，消息面和一致性预期从沪深300中选取中优质股票
### 估值
股票估值越低评分越高，但估值低并不能保证一定能上涨，还要看市场一致性预期
JZCSYL:=FINANCE(33)/ FINANCE(34)*100;
ZCBS:=IF(JZCSYL>50,8,IF(50>JZCSYL>=14,2.2+(JZCSYL-14)*0.16, 2.2+(JZCSYL-14)* 0.15));
LTP:=CAPITAL;
LTPBS:=IF(LTP<1000000,(1000000-LTP)/1000000,0);
股价估值: FINANCE(34)*(ZCBS+LTPBS)*4,COLORRED;

### 成长
主要体现在营业收入成长性、利润成长性等相关指标，以在成长的维度反映公司的价值，对于很多科
技型企业来说便是最好的价值体现，所以也成为了选股的重要参考因子。业绩好的不一定涨，业绩差的也不一定跌，还是要参考消息面和资金面

### 质量
质量因子相当于是检验了被广泛接受的潜在质量变量，即能够解释和预测股价增长的质
量变量。可以说质量因子在 A 股的历史表现优异。基于财务数据的会计变量一直长期被广泛认可。这些
变量同时也代表着企业的质量，所以也被称为质量变量。

### 流动性
指资产在流通过程中的活动性，又或者说是大家常常听到的换
手率。通常可以听到最多的是日成交量、日换手率、日成交金额。而在量化研究中,常见的流动性因子是
近一个月换手率、近三个月换手率以及近六个月换手率及其买卖循环率。
换手率
<0.5 流动性差
0.8-1.5 流动性正常
1.5-2.5 温和放量
2.5-5 明显放量
5-10 剧烈放量

### 规模
规模小的公司一般波动率比较高，风险也比较高，规模大的公司波动率比较小，风险也比较小，风险高头寸规模小，风险低头寸多

### 宏观
利用重要的宏观经济变量来描述股价收益率的共同的行为。例如，宏观经济
变量包括  GDP 增长率、利率、美元对人民币汇率、通货膨胀率以及失业人数等。而通过宏观上的各类统计量来挖掘市场周期
性变化，可以更为精确的预测市场走势与行情分化。 

### 消息
消息面主要分为利好消息和利空消息，利好不一定涨(机构提前知道消息已经涨过了或者短期利好，拉一波就跑)，利空不一定跌（利空尽出便是利好）

### 一致性预期
投资者对对于这家公司未来的业绩表现，达成了一致。

## 二.择时
多因子选股选对优质股票，再根据技术选择入场和出场的时机
### 大趋势
典型的趋势类指标 均线 MACD 乾坤线
#### 均线
均线代表单位时间内的成本价，从下方上穿均线入场，从上方下穿均线时出场，假信号比较多，结合成交量，箱体，胜率会高一点，理论胜率会接近50%，但实际可能只有30%左右，盈亏比还可以，年华100%左右，实盘可能会有较大出入。

#### MACD 
异同移动平均线，是从双指数移动平均线发展而来的，由快的指数移动平均线（EMA12）减去慢的指数移动平均线（EMA26）得到快线DIF，再用2×（快线DIF-DIF的9日加权移动均线DEA）得到MACD柱。
计算MACD时EMA的值取第一天的收盘价，数据太多不想从头开始算，取长周期X5天前的收盘价，计算后再去掉长周期X5的数据。当快线上穿慢线时入场，快线下穿慢线时出场，结合成交量胜率会提高，或者在O轴上方买入，也能提高胜率，胜率45%，比均线好一点，但假信号也多。

#### 乾坤线
周宇的一线定乾坤,使用FORCAST(线性回归预测，没有未来函数)，回测不同周期的值取最优解。胜率46%。

### 超跌反弹
#### 灵犀一指
周宇的灵犀一指，根据ENE指标改编42周期的均线X0.85,当股价小于这个价格时入场，再结合趋势指示出场

