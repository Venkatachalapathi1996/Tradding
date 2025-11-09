# Quick Start Guide for VS Code

This guide will help you quickly get started with the Trading Assistant project in Visual Studio Code.

## Step 1: Open in VS Code

1. Open VS Code
2. Click `File` → `Open Folder`
3. Select the `Tradding` folder
4. VS Code will prompt you to install recommended extensions - click "Install All"

## Step 2: Set Up Python Virtual Environment

1. Open the integrated terminal in VS Code (`` Ctrl+` `` or `View` → `Terminal`)
2. Create and activate virtual environment:

   **Windows:**
   ```bash
   python -m venv venv
   .\venv\Scripts\activate
   ```

   **macOS/Linux:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Step 3: Select Python Interpreter

1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
2. Type "Python: Select Interpreter"
3. Choose the interpreter from `./venv/bin/python` (or `.\venv\Scripts\python.exe` on Windows)

## Step 4: Set Up Redis

Redis is required for background tasks:

**Windows:**
- Download from https://github.com/microsoftarchive/redis/releases
- Run `redis-server.exe`

**macOS:**
```bash
brew install redis
brew services start redis
```

**Linux:**
```bash
sudo apt-get install redis-server
sudo systemctl start redis
```

## Step 5: Run Migrations

1. In the VS Code terminal:
   ```bash
   python manage.py migrate
   ```

2. Create a superuser (optional):
   ```bash
   python manage.py createsuperuser
   ```

## Step 6: Run the Development Server

### Option A: Using Debug Configuration (Recommended)
1. Press `F5` or click the "Run and Debug" icon in the sidebar
2. Select "Django: Run Server" from the dropdown
3. The server will start with debugging enabled

### Option B: Using Terminal
```bash
python manage.py runserver
```

## Step 7: Access the Application

Open your browser and navigate to: `http://127.0.0.1:8000/`

## Using VS Code Features

### Running Tasks
Press `Ctrl+Shift+P` and type "Tasks: Run Task" to access quick tasks:
- Run Django Server
- Make Migrations
- Migrate Database
- Run Tests
- Start Celery Worker
- And more...

### Debugging
- Set breakpoints by clicking in the gutter (left of line numbers)
- Press `F5` to start debugging
- Use `F10` (step over), `F11` (step into), `Shift+F11` (step out)

### Django Shell
1. Press `Ctrl+Shift+P`
2. Type "Tasks: Run Task"
3. Select "Django Shell"

### Running Tests
- Press `Ctrl+Shift+P`
- Type "Tasks: Run Task"
- Select "Run Tests"

Or use the test debug configuration:
- Select "Django: Test" from the debug dropdown
- Press `F5`

## Useful Keyboard Shortcuts

- `Ctrl+Shift+P`: Command Palette
- `Ctrl+P`: Quick Open File
- `Ctrl+Shift+F`: Search across files
- `Ctrl+Shift+D`: Open Debug panel
- `F5`: Start Debugging
- `Ctrl+C`: Stop server (in terminal)
- `` Ctrl+` ``: Toggle Terminal
- `Ctrl+B`: Toggle Sidebar

## Troubleshooting

### "Module not found" errors
- Make sure you selected the correct Python interpreter
- Reinstall requirements: `pip install -r requirements.txt`

### Port 8000 already in use
- Stop other Django servers or use a different port:
  ```bash
  python manage.py runserver 8080
  ```

### Redis connection errors
- Ensure Redis server is running: `redis-cli ping` (should return `PONG`)

### Celery doesn't work on Windows
- Use the `--pool=solo` flag:
  ```bash
  celery -A trading_assistant worker --loglevel=info --pool=solo
  ```

## Next Steps

- Check out the full [README.md](README.md) for detailed documentation
- Explore the Django admin at `http://127.0.0.1:8000/admin/`
- Review the code in `marketdata/` and `dashboard/` apps
- Check the Celery tasks in `marketdata/cron.py`

## Need Help?

- Read the full README.md
- Check Django documentation: https://docs.djangoproject.com/
- Check VS Code Python docs: https://code.visualstudio.com/docs/python/python-tutorial

Happy coding! 🚀
