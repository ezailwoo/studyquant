# An Quantatitive trading library for crypto-assets 数字货币量化交易框架

<p align="center">
    <img src ="https://img.shields.io/badge/platform-windows|linux|macos-yellow.svg"/>
    <img src ="https://img.shields.io/badge/python-3.6-blue.svg"/>
    <img src ="https://img.shields.io/badge/python-3.7-blue.svg"/>
</p>

# 量化交易课程
[**量化课程推荐**](https://appcop3i2898823.h5.xiaoeknow.com)


# 交易所注册推荐码

- OKEX 交易所注册推荐码, 手续费返佣**20%**
  - <https://www.okex.win/join/2521074585>
- 币安交易所注册推荐码, 手续费返佣 **10%**
  - <https://www.binance.com/zh-CN/register?ref=TDBM1BYS>

- 火币交易所注册推荐码, 手续费返佣 **15%**
  - <https://www.huobi.ms/zh-cn/topic/double-reward/?invite_code=cgx22223>



# cryptoquant

CryptoQuant is an algorithmic trading library for crypto-assets written in Python. It allows trading strategies to be easily expressed and backtested against historical data (with daily and minute resolution), providing analytics and insights regarding a particular strategy's performance. cryptoquant also supportslive-trading of crypto-assets starting with many exchanges (Okex,Binance,Bitmex etc) with more being added over time.

CryptoQuant是一套基于Python的量化交易框架，帮助个人/机构量化人员进行数字货币量化交易。框架具有回测/实盘交易功能。 策略框架支持多个平台切换回测。 并提供交易所实盘交易接口（如OKEX) 。

全新的《Python数字货币量化投资实战》系列在线课程，已经在微信公众号[**StudyQuant**]上线，一整套数字货币量化解决方案。覆盖CTA等策略（已完成）等内容。



## Features
- Ease of Use: CryptoQuant tries to get out of your way so that you can focus on algorithm development. 
- **开箱即用** ： CryptoQuant提供一套量化框架帮助您专注策略开发
- **回测**：回测框架支持数据导入，自定义交易订单号，多线程回测、遗传算法寻优等功能
- **实盘交易**： 框架提供数字货币交易所接口DEMO
- **文档支持**:[**官方社区论坛**](https://docs.studyquant.com/)

## 环境准备
* 支持的系统版本：Windows 7以上/Windows Server 2008以上/Ubuntu 18.04 LTS
* 支持的Python版本：Python 3.6 64位/ 3.7+ 
## Installation

**Windows**
使用要安装Python，激活环境，进入cryptoquant/install目录下的运行install.bat 安装依赖库
安装dependencies 中的依赖库

## Quickstart

### 如何导入数据

```Python
from cryptoquant.trader.constant import Direction, Exchange, Interval, Offset, Status, Product, OptionType, OrderType
import pandas as pd
from cryptoquant.app.data_manage.data_manager import save_data_to_cryptoquant

if __name__ == '__main__':
    df = pd.read_csv('IF9999.csv')
    symbol = 'IF9999'
    save_data_to_cryptoquant(symbol, df, Exchange.CFFEX)
    
```

### 如何回测
```Python
from datetime import datetime
from cryptoquant.app.cta_backtester.engine import BacktestingEngine, OptimizationSetting
from cryptoquant.app.cta_strategy.strategies.atr_rsi_strategy import (
    AtrRsiStrategy,
)
#%%
engine = BacktestingEngine()

engine.set_parameters(
    vt_symbol="IF9999.CFFEX",
    interval="1m",
    start=datetime(2020, 1, 1),
    end=datetime(2020, 4, 30),
    rate=0.3/10000,
    slippage=0.5,
    size=300,
    pricetick=0.2,
    capital=1_000_0,
)
setting = {}
engine.add_strategy(AtrRsiStrategy,setting)
# 导入数据
engine.load_data()
# 开始回测
engine.run_backtesting()
#计算收益
df = engine.calculate_result()
# 开始统计
engine.calculate_statistics()
# 开始画图
engine.show_chart()
```


```Python

    
```

### 实盘交易
```Python

from cryptoquant.api.api_gateway.build.apigateway_v7 import get_exchange
from cryptoquant.config.config import ok_api_key, ok_seceret_key, ok_passphrase,binance_api_key,binance_secret_key



if __name__ == "__main__":
    setting ={
        'symbol':"EOS/USDT",
        'api_key':binance_api_key,
        'secret':binance_secret_key,
        'base_asset':'EOS',
        'quote_asset':'USDT',
        'sleep_time':5,
        'time_frame':'5m'
    }

    apikey = binance_api_key
    secret = binance_secret_key
    symbol = "EOS/USDT"
    time_frame = '5m'
    strategy_name = 'apidemo'

    exchange = get_exchange(symbol, apikey, secret, time_frame, strategy_name, setting)

    print('GEt Trades', exchange.GetTrades())
    print('GEt Ticker',exchange.GetTicker())
    print('GEt Depth',exchange.GetDepth())
    print('GetAccount',exchange.GetAccount())
    print('获取K线',exchange.GetKline(time_frame))
    print('get Orders',exchange.GetOrders())
    print('get open Orders',exchange.GetOpenOrders())

    # 买单
    buy_order = exchange.Buy(Price = 3,Amount = 4)
    print(f"获取订单{exchange.GetOrder(buy_order.id)}")

    # 撤单
    cancel_order = exchange.CancelOrder(buy_order.id)
    print(f"取消订单{cancel_order}")

    # 卖单
    sell_order = exchange.Sell(Price = 5,Amount = 4)
    print(f"获取订单{exchange.GetOrder(buy_order.id)}")

    # 撤单
    cancel_order = exchange.CancelOrder(sell_order.id)
    print(f"取消订单{cancel_order}")


```

## 更多示例代码和维护的交易系统

For more demo code and strategy demo, Please check the course, some homeworks may required to completed.

[**1.0 数字货币量化课程**](https://appcop3i2898823.h5.xiaoeknow.com/v1/course/column/p_5fad5331e4b0231ba88619aa?type=3)

[**2.0 Python领域开发入门**](https://appcop3i2898823.h5.xiaoeknow.com/v1/course/column/p_5faf6fb6e4b0231ba8866883?type=3)


## 捐助
如果您觉得我们的开源软件对你有所帮助，请扫下方二维码购买课程支持。

<p align="center">
    <img src ="https://images.gitee.com/uploads/images/2021/0115/114257_f54ef081_5152232.png"/>
</p>


## Questions?
- QQ社群：1032965883
- wechat:  82789754
- 如果无法解决请前往[**官方社区论坛**](https://www.yuque.com/studyquant/cryptoquant)的

  如果你有什么量化问题、python学习、课程咨询等问题，都可以咨询我。

<p align="center">
    <img src ="https://raw.githubusercontent.com/studyquant/pictures/main/82789754.jpg"/>
</p>


## 贡献代码

非常希望大牛来贡献代码，完善项目功能。 

在提交代码的时候，请遵守以下规则，以提高代码质量：
  * 使用[autopep8](https://github.com/hhatto/autopep8)格式化你的代码。运行```autopep8 --in-place --recursive . ```即可。
  * 使用[flake8](https://pypi.org/project/flake8/)检查你的代码，确保没有error和warning。在项目根目录下运行```flake8```即可。




## 开发日志

2021-12-09    v1.3

- 更新BINANCE封装好的接口

- 更新 CCXT接口教学

- 添加 定投策略示例



2021-05-07    v1.2

更改目录结构
增加文档链接
文档补充

2021-01-15    v1.1

- 添加了APIGATEWAY 模板


- 支持回测，遗传算法调优。
- 数据导入
- 自定义订单号
- 实盘交易demo

2020-08-15  v1.0
- 开源框架



## Course Links 课程链接
| Course Links | |
| ------------- |:-------------|
|[股票-Python量化投资](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad5523e4b0231ba88619cb?type=3)|[Course](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad5523e4b0231ba88619cb?type=3)|
|[Crypto-Python量化投资与数字货币CryptoQuant](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad5331e4b0231ba88619aa?type=3)|[Course](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad5331e4b0231ba88619aa?type=3)|
|[期货-量化投资程序化交易](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad53dde4b04db7c08e3ece?type=3)|[Course](https://appcop3i2898823.h5.xiaoeknow.com/v1/goods/goods_detail/p_5fad53dde4b04db7c08e3ece?type=3)|
|[量化训练营](https://appcop3i2898823.h5.xiaoeknow.com/v1/course/column/p_604312f8e4b07d825bd93bbf?type=3)|[Course](https://appcop3i2898823.h5.xiaoeknow.com/v1/course/column/p_604312f8e4b07d825bd93bbf?type=3)|
|[其他](https://appcop3i2898823.h5.xiaoeknow.com/homepage)|[Course](https://appcop3i2898823.h5.xiaoeknow.com)|

## 量化开源框架
| Quant Framework | |
| ------------- |:-------------|
|[CryptoQuant量化框架](https://github.com/studyquant/cryptoquant)|[Code](https://github.com/studyquant/cryptoquant)|

## 定制业务
**Web/APP开发**

**量化交易系统定制**
- 支持TICK、分钟及多周期回测及实盘交易
- 多品种交易

**量化策略定制**
- 趋势、网格等
- 套利

## 关注StudyQuant
- [官网](https://studyquant.com/)
- [博客](https://www.yuque.com/studyquant/)
- [课程](https://appcop3i2898823.h5.xiaoeknow.com/homepage) 
- [量化文档网站](http://docs.studyquant.com/) 
- [B站视频](https://space.bilibili.com/431803003)

### 联系方式
wechat: studyquant88