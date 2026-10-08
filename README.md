# Wireless-sensor-based-monitoring.python
from flask import Flask, request, jsonify
from datetime import datetime

app = Flask(__name__)

@app.route("/sensor", methods=["POST"])
def receive_data():
    data = request.get_json()

    temperature = data.get("temperature")
    humidity = data.get("humidity")
    current = data.get("current")

    print("Temperature:", temperature)
    print("Humidity:", humidity)
    print("Current:", current)

    # Save data to database here

    return jsonify({
        "status": "success",
        "time": datetime.now().isoformat()
    })

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
ESP32 sends data
import urequests
import time

url = "http://YOUR_PC_IP:5000/sensor"

data = {
    "temperature": 28.5,
    "humidity": 65,
    "current": 2.4
}

response = urequests.post(url, json=data)
print(response.text)
response.close()

time.sleep(10)
For an energy-monitoring project, you can extend this to calculate:

Power (W) = Voltage × Current

Energy (kWh) = Power (W) × Time (hours) / 1000
