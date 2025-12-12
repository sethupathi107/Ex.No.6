 # Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

## Name : Sethupathi K
## Register no: 212223040189
# Aim: 
To write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

# AI Tools Required:

# Explanation:
Experiment the persona pattern as a programmer for any specific applications related with your interesting area. 
Generate the outoput using more than one AI tool and based on the code generation analyse and discussing that. 



## 🏗️ Introduction

Modern software development has been revolutionized by **AI-assisted coding tools**.
Instead of manually writing large sections of code, developers now collaborate with AI models that:

* Interpret natural language instructions
* Generate functional code snippets
* Debug and optimize programs
* Provide actionable insights from data

This README illustrates a full experimental study showing how progressively improved **prompts** can transform AI-generated results from simple scripts to complex data-driven solutions.

---

## 💡 Concept: Prompt Engineering

**Prompt engineering** is the art of communicating with AI effectively.

A strong prompt typically includes:

* **Context:** The situation or background (e.g., project type, data source)
* **Role:** Defines AI’s persona (e.g., “Act as a senior Python developer.”)
* **Task:** The exact problem to solve
* **Constraints:** Conditions like performance, format, or coding standard
* **Expected Output:** Defines what the answer should look like

---

## ⚙️ Stage 1 – Basic API Interaction

### 🧾 Prompt

```
You are an expert Python developer. Write Python code to connect to two public APIs — one for weather data (OpenWeather) and another for air quality (AQICN). Fetch data for a user-given city and display both results.
```

### 💻 AI-Generated Code

```python
import requests

def get_weather(city):
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid=YOUR_WEATHER_KEY&units=metric"
    response = requests.get(url)
    return response.json()

def get_air_quality(city):
    url = f"https://api.waqi.info/feed/{city}/?token=YOUR_AQI_KEY"
    response = requests.get(url)
    return response.json()

city = input("Enter city name: ")
weather = get_weather(city)
aqi = get_air_quality(city)

print("Weather Data:", weather)
print("Air Quality Data:", aqi)
```

### 🧠 Explanation

This prompt generated a basic Python script to access two APIs and print JSON responses.
Although functional, it lacks error handling and formatted output — improved in the next stage.

---

## 🧮 Stage 2 – Improved Comparison and Formatting

### 🧾 Prompt

```
Refine the code to include error handling, and display results from both APIs in a formatted table with temperature, humidity, and AQI.
```

### 💻 AI-Generated Code

```python
import requests
from tabulate import tabulate

def get_data(city):
    try:
        weather_api = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid=YOUR_WEATHER_KEY&units=metric"
        aqi_api = f"https://api.waqi.info/feed/{city}/?token=YOUR_AQI_KEY"
        weather = requests.get(weather_api).json()
        air_quality = requests.get(aqi_api).json()

        data = [
            ["City", city],
            ["Temperature (°C)", weather['main']['temp']],
            ["Humidity (%)", weather['main']['humidity']],
            ["Air Quality Index", air_quality['data']['aqi']]
        ]
        print(tabulate(data, headers=["Parameter", "Value"], tablefmt="fancy_grid"))
    except Exception as e:
        print("Error:", e)

city = input("Enter city: ")
get_data(city)
```

### 🧠 Explanation

This stage introduces:

* **Error handling**
* **Data presentation using `tabulate`**
* Clearer readability for real-world usability

---

## 🔍 Stage 3 – Comparative API Analysis

### 🧾 Prompt

```
Write Python code that compares outputs from two APIs (OpenWeather and AQICN). If both APIs provide similar data like temperature or humidity, compare and calculate percentage difference.
```

### 💻 AI-Generated Code

```python
def compare_temperature(temp1, temp2):
    difference = abs(temp1 - temp2)
    percent_diff = (difference / ((temp1 + temp2) / 2)) * 100
    return percent_diff

temp_api1 = 30.5
temp_api2 = 31.2
print(f"Temperature difference: {compare_temperature(temp_api1, temp_api2):.2f}%")
```

### 🧠 Explanation

Here, AI introduces mathematical logic to compute differences — demonstrating analytical thinking from prompts.

---

## 📊 Stage 4 – Data Visualization (Graph)

### 🧾 Prompt

```
Add code to visualize temperature, humidity, and AQI values using Matplotlib in a bar chart.
```

### 💻 AI-Generated Code

```python
import matplotlib.pyplot as plt

def plot_data(city, temp, humidity, aqi):
    parameters = ['Temperature', 'Humidity', 'AQI']
    values = [temp, humidity, aqi]
    plt.bar(parameters, values, color=['orange', 'blue', 'green'])
    plt.title(f'Weather & AQI Data for {city}')
    plt.xlabel('Parameter')
    plt.ylabel('Value')
    plt.show()

plot_data('Chennai', 32, 70, 140)
```

### 🧠 Explanation

Visual representation enhances understanding of environmental conditions — a crucial improvement for usability.

---

## 🧾 Stage 5 – AI-Generated Insights

### 🧾 Prompt

```
Generate AI insights based on API outputs. For instance, if AQI > 100, suggest staying indoors, else recommend outdoor activity. Output text-based suggestions.
```

### 💻 AI-Generated Code

```python
def generate_insights(temp, humidity, aqi):
    insights = []
    if aqi > 100:
        insights.append("Air quality is poor. Avoid outdoor activity.")
    else:
        insights.append("Air quality is good. Safe for outdoor activity.")

    if humidity > 80:
        insights.append("High humidity detected — stay hydrated.")
    elif temp > 35:
        insights.append("High temperature — avoid peak afternoon hours.")
    else:
        insights.append("Weather conditions are normal.")

    return "\n".join(insights)

print(generate_insights(33, 75, 120))
```

### 🧠 Explanation

The prompt produced meaningful **textual recommendations**, showing how AI-generated data can assist users in daily planning.

---

## 💾 Stage 6 – Data Logging and Automation

### 🧾 Prompt

```
Modify the previous code to save all API data and insights to a JSON file with timestamps. Automate this every 2 hours using a scheduler.
```

### 💻 AI-Generated Code

```python
import json
import time
from datetime import datetime

def save_data(city, weather, air_quality, insights):
    record = {
        "timestamp": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
        "city": city,
        "weather": weather,
        "air_quality": air_quality,
        "insights": insights
    }
    with open("daily_log.json", "a") as file:
        file.write(json.dumps(record) + "\n")

while True:
    city = "Chennai"
    weather = {"temp": 33, "humidity": 72}
    air_quality = {"aqi": 140}
    insights = generate_insights(33, 72, 140)
    save_data(city, weather, air_quality, insights)
    print("Data logged successfully.")
    time.sleep(7200)  # Runs every 2 hours
```

### 🧠 Explanation

This demonstrates how prompt-based coding can evolve into automation and data persistence — aligning with professional use cases.

---

## 📦 Summary Table

| Stage | Description          | Key Learning                  | AI Role            |
| ----- | -------------------- | ----------------------------- | ------------------ |
| 1     | Fetch data from APIs | Basic API integration         | Code generator     |
| 2     | Compare data         | Error handling + formatting   | Code improver      |
| 3     | Analyze outputs      | Calculation + logic building  | Analyst            |
| 4     | Visualize            | Matplotlib graph creation     | Visual assistant   |
| 5     | Generate insights    | Text interpretation           | Advisor            |
| 6     | Automate logging     | Data persistence + scheduling | Automation partner |

---

## ✍️ Reflection

This 6-stage workflow revealed how **AI prompt refinement** directly affects code quality and output precision.

* Early prompts = Generic code
* Later prompts = Professional-grade automation
  **Lesson learned:** Precise prompts yield purposeful code.

Future improvement ideas:

* Add API key management via `.env` files
* Include multiple city comparisons
* Integrate notification systems (email or Telegram bot)

---



# Conclusion:
Prompt engineering transforms AI from a text generator into a collaborative coding partner.
Through this experiment, it is evident that:

Specific and contextual prompts yield better program logic.

Structured output requests enhance readability.

AI can support coding, comparison, and insight generation when guided properly.

Thus, the experiment “Framing Prompts for AI-Assisted Project Coding” successfully demonstrates the evolution of effective prompts and their impact on AI performance.

# Result: 
The corresponding Prompt is executed successfully.
