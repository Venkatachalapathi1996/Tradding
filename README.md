# Trading Assistant

A Django-based trading assistant application for analyzing market data, tracking stocks, and generating trading insights.

## Features

- Real-time market data tracking
- Trading analysis and insights
- Dashboard for viewing market trends
- Automated daily plan generation
- WebSocket support for live updates
- Celery-based background tasks
- Integration with Groww API for trading data

## Prerequisites

Before you begin, ensure you have the following installed:
- Python 3.8 or higher
- pip (Python package manager)
- Redis server (for Celery and Channels)
- Git

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Venkatachalapathi1996/Tradding.git
cd Tradding
```

### 2. Create a Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Start Redis Server

The application requires Redis for Celery task queue and Django Channels.

**Windows:**
- Download Redis from https://github.com/microsoftarchive/redis/releases
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

### 5. Run Database Migrations

```bash
python manage.py migrate
```

### 6. Create a Superuser (Optional)

```bash
python manage.py createsuperuser
```

### 7. Start the Development Server

```bash
python manage.py runserver
```

The application will be available at `http://127.0.0.1:8000/`

### 8. Start Celery Worker (Optional)

In a separate terminal, activate the virtual environment and run:

**Windows:**
```bash
celery -A trading_assistant worker --loglevel=info --pool=solo
```

**macOS/Linux:**
```bash
celery -A trading_assistant worker --loglevel=info
```

### 9. Start Celery Beat (Optional)

For scheduled tasks, in another terminal:

```bash
celery -A trading_assistant beat --loglevel=info
```

## Using with VS Code

This project includes VS Code configuration files in the `.vscode` directory:

- **settings.json**: Python and Django-specific settings
- **launch.json**: Debug configurations for Django server and tests
- **tasks.json**: Quick tasks for common operations
- **extensions.json**: Recommended extensions

### Recommended VS Code Extensions

The following extensions will enhance your development experience:
- Python (Microsoft)
- Pylance (Microsoft)
- Django (Baptiste Darthenay)
- Python Indent
- Git Graph
- GitLens

### Running the Project in VS Code

1. Open the project folder in VS Code
2. Install recommended extensions when prompted
3. Select the Python interpreter from your virtual environment (Ctrl+Shift+P → "Python: Select Interpreter")
4. Press F5 to start debugging the Django server
5. Use the built-in terminal to run management commands

## Project Structure

```
Tradding/
├── dashboard/              # Dashboard app for UI
├── marketdata/            # Market data tracking and analysis
├── trading_assistant/     # Main Django project settings
├── manage.py             # Django management script
├── requirements.txt      # Python dependencies
└── db.sqlite3           # SQLite database
```

## Configuration

### Environment Variables

You may want to create a `.env` file for sensitive configuration:

```env
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
GROWW_API_KEY=your-api-key
NEWS_API_KEY=your-news-api-key
```

**Note:** Remember to update `settings.py` to read from environment variables for production use.

## Running Tests

```bash
python manage.py test
```

## Common Issues

### Redis Connection Error
If you see "Error connecting to Redis", ensure Redis server is running:
```bash
redis-cli ping
```
Should return: `PONG`

### Port Already in Use
If port 8000 is already in use, specify a different port:
```bash
python manage.py runserver 8080
```

### Celery on Windows
Windows requires the `--pool=solo` flag:
```bash
celery -A trading_assistant worker --loglevel=info --pool=solo
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is for educational and personal use.

## Support

For issues and questions, please open an issue on GitHub.
