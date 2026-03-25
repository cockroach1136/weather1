# 天氣網站

一個簡單的天氣網站，使用 Python + Flask，資料來自免費的 Open-Meteo API（不需要 API key）。

## 本地端執行

```bash
# 1. 安裝套件
pip install -r requirements.txt

# 2. 啟動
python app.py

# 3. 打開瀏覽器前往
http://localhost:5000
```

## 部署到 Render（讓外面的人連進來）

1. 把這個資料夾上傳到 GitHub（建一個新的 repository）
2. 到 https://render.com 註冊
3. 點「New +」→「Web Service」
4. 連結你的 GitHub repository
5. 設定：
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn app:app`
   - **Environment**: Python 3
6. 點「Create Web Service」
7. 等約 2 分鐘，就會得到一個公開網址！

## 修改城市

在 `app.py` 第 8 行，修改 `lat`、`lon` 和 `city` 的值：

```python
def get_weather(lat=24.8388, lon=120.9675, city="新竹"):
```

台北：lat=25.0330, lon=121.5654
高雄：lat=22.6273, lon=120.3014
台中：lat=24.1477, lon=120.6736
