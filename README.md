# Clinical Analytics Dashboard

A Dash-based web application for visualizing and analyzing clinical data including patient volume, wait times, and care scores.

## Prerequisites

- Python 3.7 or higher
- pip (Python package installer)

## Setup Instructions

### 1. Install Python

**Windows:**
- Download Python from [python.org](https://www.python.org/downloads/)
- Run the installer and check "Add Python to PATH"
- Verify installation: `python --version`

**macOS:**
```bash
# Using Homebrew
brew install python3
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

### 2. Create Virtual Environment

Navigate to your project directory and create a virtual environment:

```bash
# Create virtual environment
python -m venv venv

# Or on some systems:
python3 -m venv venv
```

### 3. Activate Virtual Environment

**Windows:**
```bash
venv\Scripts\activate
```

**macOS/Linux:**
```bash
source venv/bin/activate
```

You should see `(venv)` prefix in your terminal prompt.

### 4. Install Required Packages

```bash
pip install dash plotly pandas numpy
```

If you have a `requirements.txt` file:
```bash
pip install -r requirements.txt
```

### 5. Prepare Your Data

Ensure you have the required data file(s) that the app expects. Check the script for the data loading section and place your data files in the appropriate location.

## Running the Application

### Start the App

```bash
python app.py
```

The app will start and display output similar to:
```
Dash is running on http://127.0.0.1:10030/

 * Serving Flask app 'app'
 * Debug mode: on
```

### Access the Application

You can access the dashboard using any of these methods:

#### Method 1: Local Access (Same Machine)
Open your web browser and go to:
- `http://localhost:10030`
- `http://127.0.0.1:10030`

#### Method 2: Network Access (Without Port Forwarding)

If you want to access the app from other devices on the same network:

1. **Find your local IP address:**

   **Windows:**
   ```bash
   ipconfig
   ```
   Look for "IPv4 Address" under your active network adapter (usually starts with 192.168.x.x or 10.x.x.x)

   **macOS/Linux:**
   ```bash
   ifconfig
   # or
   ip addr show
   ```
   Look for "inet" address (usually starts with 192.168.x.x or 10.x.x.x)

2. **Modify the app to listen on all network interfaces:**
   
   In your `app.py`, change the last line to:
   ```python
   app.run_server(debug=True, host='0.0.0.0', port=10030)
   ```

3. **Access from other devices on the same network:**
   ```
   http://YOUR_LOCAL_IP:10030
   ```
   
   Example: `http://192.168.1.100:10030`

4. **Firewall Configuration (if needed):**
   
   **Windows:**
   - Open Windows Defender Firewall
   - Click "Advanced settings"
   - Add new Inbound Rule for port 10030
   
   **macOS:**
   ```bash
   sudo /usr/libexec/ApplicationFirewall/socketfilterfw --add /path/to/python
   ```
   
   **Linux (Ubuntu):**
   ```bash
   sudo ufw allow 10030/tcp
   ```

## Stopping the Application

Press `Ctrl + C` in the terminal where the app is running.

## Deactivating Virtual Environment

When you're done working:
```bash
deactivate
```

## Troubleshooting

### Port Already in Use
If port 10030 is already in use:
```bash
# Windows
netstat -ano | findstr :10030

# macOS/Linux
lsof -i :10030
```

Change the port number in the app or kill the process using that port.

### Module Not Found Errors
Make sure your virtual environment is activated and all packages are installed:
```bash
pip list  # Check installed packages
pip install -r requirements.txt  # Reinstall if needed
```

### Cannot Access from Other Devices
- Verify `host='0.0.0.0'` is set in `app.run_server()`
- Check firewall settings
- Ensure both devices are on the same network
- Verify the correct local IP address is being used

### Data File Not Found
Check the data file path in your script and ensure the data file exists in the correct location.

## Project Structure

```
project/
├── venv/                 # Virtual environment (not committed to git)
├── app.py               # Main application file
├── requirements.txt     # Python dependencies
├── data/               # Data files (if applicable)
└── README.md           # This file
```

## Additional Notes

- The app runs in debug mode by default, which provides helpful error messages and auto-reload on code changes
- For production deployment, set `debug=False`
- Always keep your virtual environment activated when working on the project
- Add `venv/` to your `.gitignore` file if using version control
