from flask import Flask, render_template
import urllib.request
import json
import datetime

app = Flask(__name__)

def get_weather(lat=24.8388, lon=120.9675, city="新竹"):
    url = (
        f"https://api.open-meteo.com/v1/forecast"
        f"?latitude={lat}&longitude={lon}"
        f"&current=temperature_2m,weathercode,windspeed_10m,relative_humidity_2m"
        f"&hourly=temperature_2m,weathercode,precipitation_probability"
        f"&daily=temperature_2m_max,temperature_2m_min,weathercode,precipitation_probability_max"
        f"&timezone=Asia%2FTaipei&forecast_days=2"
    )
    with urllib.request.urlopen(url) as response:
        data = json.loads(response.read())

    code = data["current"]["weathercode"]
    today = datetime.date.today().isoformat()
    current_hour = datetime.datetime.now().hour

    hourly_times = data["hourly"]["time"]
    hourly_temps = data["hourly"]["temperature_2m"]
    hourly_codes = data["hourly"]["weathercode"]
    hourly_rain  = data["hourly"]["precipitation_probability"]

    hours = []
    current_hour_index = 0
    for i, t in enumerate(hourly_times):
        if t.startswith(today):
            hour = int(t[11:13])
            if hour == current_hour:
                current_hour_index = len(hours)
            hours.append({
                "hour": f"{hour:02d}:00",
                "temp": round(hourly_temps[i], 1),
                "icon": weather_icon(hourly_codes[i]),
                "rain": hourly_rain[i],
            })

    weather = {
        "city": city,
        "temp": round(data["current"]["temperature_2m"]),
        "humidity": data["current"]["relative_humidity_2m"],
        "wind": round(data["current"]["windspeed_10m"]),
        "description": weather_description(code),
        "icon": weather_icon(code),
        "hours": hours,
        "forecast": []
    }

    days_zh = ["週一", "週二", "週三", "週四", "週五", "週六", "週日"]
    for i in range(min(5, len(data["daily"]["time"]))):
        date_str = data["daily"]["time"][i]
        d = datetime.date.fromisoformat(date_str)
        day_name = "今天" if i == 0 else days_zh[d.weekday()]
        c = data["daily"]["weathercode"][i]
        weather["forecast"].append({
            "day": day_name,
            "high": round(data["daily"]["temperature_2m_max"][i]),
            "low": round(data["daily"]["temperature_2m_min"][i]),
            "rain": data["daily"]["precipitation_probability_max"][i],
            "icon": weather_icon(c),
        })

    return weather, current_hour_index

def weather_description(code):
    if code == 0: return "晴天"
    elif code in [1, 2]: return "局部多雲"
    elif code == 3: return "多雲"
    elif code in [45, 48]: return "有霧"
    elif code in [51, 53, 55]: return "毛毛雨"
    elif code in [61, 63, 65]: return "下雨"
    elif code in [71, 73, 75]: return "下雪"
    elif code in [80, 81, 82]: return "陣雨"
    elif code in [95, 96, 99]: return "雷陣雨"
    else: return "天氣不明"

def weather_icon(code):
    if code == 0: return "☀️"
    elif code in [1, 2]: return "⛅"
    elif code == 3: return "☁️"
    elif code in [45, 48]: return "🌫️"
    elif code in [51, 53, 55, 61, 63, 65, 80, 81, 82]: return "🌧️"
    elif code in [71, 73, 75]: return "❄️"
    elif code in [95, 96, 99]: return "⛈️"
    else: return "🌤️"

@app.route("/")
def index():
    weather, current_hour_index = get_weather()
    return render_template("index.html", weather=weather, current_hour_index=current_hour_index)

if __name__ == "__main__":
    app.run(debug=True)
