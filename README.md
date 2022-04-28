# NCKU_DL

成大製造所 110(下) 深度學習網路基礎: 理論與產業實務

---

## Description

此課程目標為學習深度學習模型與數學理論基礎，並透過Deep Learing預測股票價格作為期末專案。

* 下單交易開放時間      ：`16:00 ~ 隔日08:59`
* 台股盤中(不開放交易)  ：`09:00 ~ 14:59`

---

## Stock Price

### 獲取股票資訊

課程本身有提供基本的成交價、開盤價、收盤價等。

也可以自己抓資料，目前(20220322)是打算使用`twstock`這個別人寫好的套件來抓。

---

## Models

### 1. Prophet 預言家

為Facebook在2017所開發之模型，Prophet可以預測一些週期性的時間序列資料。

主要概念是透過多則Fourier Series來Fit時間序列：

    f(t) = year(t) + season(t) + week(t) + trend(t)

相較於自行訓練時間序列預測模型，Prophet 的一些優點如下：‌
1. 改善模型選擇和調參的時間成本：時間序列有許多經典算法如 AR, VAR, ARMA, ARIMA, 指數平滑法等，選擇模型和調參的過程可被自動化。
2. 提供讓分析師、領域專家能根據經驗法則設定的參數：例如歷史週期、特殊節日的日期等，不會因為寫成制式套件就失去自己手刻的好處。


---
## 交易API

```python
import requests

data = {
    'uname'     :<使用者名稱>,
    'pass'      :<使用者密碼>,
    'scode'     :<股票代號>,
    'svol'      :<買/賣張數>,
    'sprice'    :<買進價格>,
    'sell_price':<賣出價格>
}

r = requests.post("http://140.116.86.241:8800/api/buy", data=data)
```