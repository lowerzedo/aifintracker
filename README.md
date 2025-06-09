# 💰 Finance Tracker Bot

> **AI-Powered Expense Tracking via Telegram with Google Sheets Integration**

A sophisticated Telegram bot that automatically tracks and categorizes your expenses using Google Gemini AI, stores data in Google Sheets, and provides rich analytics with visual charts. Designed for Malaysia timezone (GMT+8) with professional deployment support.

## ✨ Features

### 🤖 AI-Powered Expense Analysis

- **Receipt OCR**: Upload photos of receipts for automatic data extraction
- **Natural Language Processing**: Send text like "Coffee $5.50" for instant logging
- **Smart Categorization**: Automatic expense categorization into 7 categories
- **Merchant Detection**: Identifies store/company names from receipts

### 📊 Data Management & Analytics

- **Google Sheets Integration**: Real-time expense logging and monthly summaries
- **Visual Charts**: Beautiful pie charts showing expense breakdowns
- **Monthly Reports**: Detailed summaries with category-wise totals
- **Data Recalculation**: Refresh monthly totals with a single command

### 🌏 Localization

- **Malaysia Timezone (GMT+8)**: All dates and times automatically adjusted
- **Currency Support**: Displays amounts in USD format
- **Date Intelligence**: AI understands "today" in your local timezone

### 🛡️ Enterprise-Ready

- **Multiple Deployment Options**: Flask, AWS Lambda (Zappa), Heroku, Railway
- **Environment-Based Configuration**: Secure credential management
- **Comprehensive Logging**: Full audit trail for debugging
- **Error Handling**: Graceful failure with user-friendly messages

## 🚀 Quick Start

### Prerequisites

- Python 3.9+
- Telegram Bot Token
- Google Gemini API Key
- Google Sheets API credentials

### 1. Clone & Install

```bash
git clone <your-repo-url>
cd finance_chat
pip install -r requirements.txt
```

### 2. Environment Setup

Create a `.env` file:

```bash
# Required
TELEGRAM_BOT_TOKEN=your_bot_token_here
GEMINI_API_KEY=your_gemini_api_key_here
GOOGLE_SHEETS_ID=your_google_sheets_id_here
GOOGLE_CREDENTIALS_JSON={"type":"service_account",...}

# Optional
PORT=5000
DEBUG=False
```

### 3. Google Sheets Setup

1. Create a new Google Sheet
2. Share it with your service account email
3. Run `/setup` command in Telegram to initialize sheets

### 4. Deploy & Configure

```bash
# Local Development
python app.py

# Set Telegram Webhook
curl -X POST http://localhost:5000/set_webhook \
  -H "Content-Type: application/json" \
  -d '{"webhook_url": "https://your-domain.com/webhook"}'
```

## 📱 Bot Commands

| Command    | Description                          | Example    |
| ---------- | ------------------------------------ | ---------- |
| `/start`   | Welcome message and feature overview | `/start`   |
| `/summary` | Current month expense breakdown      | `/summary` |
| `/chart`   | Visual pie chart of monthly expenses | `/chart`   |
| `/setup`   | Initialize Google Sheets structure   | `/setup`   |
| `/refresh` | Recalculate monthly totals           | `/refresh` |

## 💸 Usage Examples

### Text Input

```
"Lunch at McDonald's $12.50"
"Grab ride $8"
"Groceries $45.20"
"Coffee $4.80"
```

### Receipt Photos

- Upload any receipt image
- AI automatically extracts amount, merchant, and category
- Handles multiple formats (JPEG, PNG, PDF as image)

### Expected Output

```
✅ Expense Logged!

💰 Amount: $12.50
📂 Category: Food
📝 Description: Lunch at McDonald's
📅 Date: 2025-06-09
🏪 Merchant: McDonald's
```

## 🏗️ Architecture

### Technology Stack

- **Backend**: Flask (Python 3.9+)
- **AI Engine**: Google Gemini 2.5 Flash
- **Database**: Google Sheets API
- **Messaging**: Telegram Bot API
- **Charts**: Matplotlib with custom styling
- **Deployment**: AWS Lambda, Heroku, Railway compatible

### Data Flow

```
User Input → Telegram → Webhook → AI Processing → Google Sheets → Response
```

### Expense Categories

1. 🍔 **Food** - Restaurants, groceries, dining
2. 🚗 **Transport** - Fuel, public transport, ride-sharing
3. ⚡ **Utilities** - Bills, internet, phone, electricity
4. 🛍️ **Shopping** - Retail, online purchases, clothing
5. 🎬 **Entertainment** - Movies, games, subscriptions
6. 🏥 **Healthcare** - Medical, pharmacy, insurance
7. 📋 **Other** - Everything else

## 🚀 Deployment Options

### AWS Lambda (Recommended)

```bash
# Install Zappa
pip install zappa

# Deploy
zappa deploy dev
zappa update dev
```

### Heroku

```bash
git add .
git commit -m "Deploy to Heroku"
git push heroku main
```

### Railway/Render

1. Connect GitHub repository
2. Set environment variables
3. Auto-deploy on push

### Docker

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "app:app"]
```

## 📋 API Endpoints

| Endpoint       | Method | Description                |
| -------------- | ------ | -------------------------- |
| `/`            | GET    | Health check               |
| `/webhook`     | POST   | Telegram webhook handler   |
| `/set_webhook` | POST   | Configure Telegram webhook |

## 🔧 Configuration

### Environment Variables

```bash
# Core Configuration
TELEGRAM_BOT_TOKEN=       # Required: Bot token from @BotFather
GEMINI_API_KEY=          # Required: Google AI Studio API key
GOOGLE_SHEETS_ID=        # Required: Google Sheets document ID
GOOGLE_CREDENTIALS_JSON= # Required: Service account JSON

# Optional Settings
PORT=5000               # Server port (default: 5000)
DEBUG=False            # Debug mode (default: False)
```

### Google Sheets Structure

The bot automatically creates two sheets:

#### Expenses Sheet

| Date | Amount | Category | Description | Merchant | Month |
| ---- | ------ | -------- | ----------- | -------- | ----- |

#### Monthly_Totals Sheet

| Month | Total_Amount | Food | Transport | Utilities | Shopping | Entertainment | Healthcare | Other |
| ----- | ------------ | ---- | --------- | --------- | -------- | ------------- | ---------- | ----- |

## 🛠️ Development

### Local Testing

```bash
# Install dependencies
pip install -r requirements.txt

# Run development server
python app.py

# Test webhook locally (use ngrok)
ngrok http 5000
```

### Adding New Features

1. **New Commands**: Add handlers in `telegram_webhook()` function
2. **New Categories**: Update category lists in both files
3. **New Charts**: Extend `create_monthly_chart()` method
4. **New Integrations**: Extend `SheetsManager` class

## 📊 Sample Outputs

### Monthly Summary

```
📊 Monthly Summary (2025-06)

💰 Total: $1,234.56

By Category:
🍔 Food: $456.78
🚗 Transport: $123.45
⚡ Utilities: $234.56
🛍️ Shopping: $234.56
🎬 Entertainment: $89.12
🏥 Healthcare: $67.89
📋 Other: $28.20
```

### Visual Chart

The `/chart` command generates a professional pie chart with:

- Color-coded categories
- Percentage breakdowns
- Amount labels
- Clean, modern design

## 🔒 Security & Privacy

- **No local data storage**: All data stored in your Google Sheets
- **Secure credentials**: Environment-based configuration
- **Encrypted communication**: HTTPS for all API calls
- **Access control**: Only you can access your bot and data

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support

- **Issues**: GitHub Issues for bug reports
- **Features**: GitHub Discussions for feature requests
- **Documentation**: Check the README and code comments

---

<div align="center">
  <strong>Built with ❤️ for smart expense tracking</strong>
</div>
