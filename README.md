python3 -m venv venv
source venv/bin/activate
pip install Flask
from flask import Flask
import os
import subprocess
from datetime import datetime
import pytz

app = Flask(__name__)

@app.route('/htop')
def htop():
    username = os.getenv('USER') or os.getenv('USERNAME')
    name = "Your Full Name"  # Replace with your full name
    tz = pytz.timezone('Asia/Kolkata')
    server_time = datetime.now(tz).strftime('%Y-%m-%d %H:%M:%S IST')
    top_output = subprocess.getoutput('top -bn1')

    return f"""
    <h1>System Details</h1>
    <p><strong>Name:</strong> {name}</p>
    <p><strong>Username:</strong> {username}</p>
    <p><strong>Server Time:</strong> {server_time}</p>
    <pre>{top_output}</pre>
    """
if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
python app.py
