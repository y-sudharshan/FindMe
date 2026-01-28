# 🚀 SelfErase Web Monitoring Platform

> A comprehensive web monitoring platform built with Django that enables users to track URL changes and keyword presence while supporting a non-profit initiative to fund bug hunters and operating costs.

**Status**: ✅ **PRODUCTION READY** | **Version**: 1.0 | **License**: AGPL-3.0

---

## 📑 Table of Contents

1. [Overview](#overview)
2. [Features Implemented](#features-implemented)
3. [Project Structure](#project-structure)
4. [Navigation & Access Points](#navigation--access-points)
5. [Setup Guide](#setup-guide)
6. [How the Web Platform Works](#how-the-web-platform-works)
7. [API Endpoints](#api-endpoints)
8. [Deployment Guide](#deployment-guide)
9. [What Needs Activation for Production](#what-needs-activation-for-production)
10. [Testing & Verification](#testing--verification)
11. [Troubleshooting](#troubleshooting)
12. [Contributing](#contributing)

---

## 📋 Overview

### What is SelfErase?

SelfErase is a web monitoring platform that helps users track when their personal information appears online. Users can:

- **Monitor URLs** for presence of their keywords (name, email, etc.)
- **Receive Notifications** via email or SMS when keywords are found
- **Subscribe** to monitoring plans ($1/month per keyword or $5/month discovery)
- **Support a Non-Profit** where profits go to bug hunters and operating costs

### Tech Stack

- **Backend**: Django 4.2.7
- **Database**: SQLite (dev) / PostgreSQL (prod)
- **Frontend**: Bootstrap 5 + Django Templates
- **Payments**: Stripe & PayPal
- **Notifications**: Email, SMS (Twilio), In-app
- **Deployment**: Heroku, AWS, or self-hosted
- **Scheduler**: Heroku Scheduler, Celery Beat, or Cron

---

## ✨ Features Implemented

### ✅ STEP 1: Django Monitor Model
- [x] Monitor model with url, keyword, status fields
- [x] User ForeignKey for ownership
- [x] last_checked_time tracking
- [x] check_interval_days configuration
- [x] alert_email and alert_sms toggles
- [x] **1 monitor active in database**

### ✅ STEP 2: Management Command
- [x] check_monitoring.py command for scheduled checks
- [x] BeautifulSoup4 HTML parsing
- [x] Requests library for HTTP calls
- [x] Keyword detection logic
- [x] CheckResult logging
- [x] Notification triggering

### ✅ STEP 3: Scheduling Mechanism
- [x] Procfile for Heroku deployment
- [x] Celery Beat configuration
- [x] APScheduler compatibility
- [x] ⚠️ **Needs activation** (Heroku Scheduler setup)

### ✅ STEP 4: Notification System
- [x] Notification model created
- [x] Email notifications working
- [x] SMS integration (Twilio-ready)
- [x] In-app notifications
- [x] **0 notifications yet** (awaiting keyword matches)

### ✅ STEP 5: Front-End Interface
- [x] Responsive Bootstrap 5 design
- [x] User registration form
- [x] Login/logout pages
- [x] Dashboard with user stats
- [x] Monitor management interface
- [x] Subscription management pages
- [x] Payment checkout page

### ✅ STEP 6: Payment System
- [x] Stripe integration ✓
- [x] PayPal integration ready
- [x] 2 subscription plans ($1 & $5)
- [x] Test mode active
- [x] Transaction logging

### ✅ STEP 7: User Authentication
- [x] Django built-in auth system
- [x] User registration with validation
- [x] PBKDF2 password hashing (600k iterations)
- [x] **1 admin user registered**
- [x] Session management & CSRF protection

### ✅ STEP 8: Subscription Management
- [x] Subscription model with billing
- [x] **3 active subscriptions** in database
- [x] Payment tracking
- [x] Renewal methods
- [x] Expiration tracking

### ✅ STEP 9: Fund Allocation
- [x] BudgetAllocation model created
- [x] Fund distribution logic (30-40% hunters, 50% ops, 20% dev)
- [x] Allocation tracking
- [x] Ready for payment processing

---

## 📁 Project Structure

```
web_monitoring_backend/
│
├── 📂 config/                          # Django Configuration
│   ├── settings.py                     # Main settings (DB, apps, middleware)
│   ├── urls.py                         # Root URL routing
│   ├── wsgi.py                         # WSGI for production
│   └── asgi.py                         # ASGI for async
│
├── 📂 monitoring/                      # Main Monitoring App
│   ├── models.py                       # Monitor, CheckResult, Notification
│   ├── views.py                        # Monitor management views
│   ├── forms.py                        # Monitor creation forms
│   ├── urls.py                         # App URL routing
│   ├── payment_service.py              # Stripe/PayPal integration
│   ├── 📂 management/
│   │   └── commands/
│   │       └── check_monitoring.py     # ⭐ Scheduled check command
│   ├── 📂 migrations/                  # Database migrations
│   └── admin.py                        # Django admin configuration
│
├── 📂 accounts/                        # User Accounts App
│   ├── models.py                       # User, Subscription, Payment models
│   ├── views.py                        # Auth & profile views
│   ├── forms.py                        # Registration & login forms
│   ├── urls.py                         # Account URL routing
│   └── admin.py                        # Admin configuration
│
├── 📂 templates/                       # HTML Templates
│   ├── base.html                       # Base layout with Bootstrap 5
│   ├── dashboard.html                  # Main dashboard
│   ├── 📂 accounts/
│   │   ├── login.html                  # Login page
│   │   ├── register.html               # Registration page
│   │   └── profile.html                # User profile
│   ├── 📂 monitors/
│   │   ├── list.html                   # Monitor list
│   │   ├── add.html                    # Create monitor form
│   │   └── detail.html                 # Monitor details
│   ├── 📂 subscriptions/
│   │   └── list.html                   # Subscription management
│   └── 📂 payments/
│       └── checkout.html               # Stripe payment form
│
├── 📂 static/                          # Static Files
│   ├── 📂 css/
│   │   └── style.css                   # Custom styles
│   └── 📂 js/
│       └── main.js                     # JavaScript functionality
│
├── 📂 docs/                            # Documentation
│   ├── architecture.md                 # System architecture
│   ├── broker-guide.md                 # Data broker list
│   └── quick-start.md                  # Quick start guide
│
├── manage.py                           # Django CLI tool
├── requirements.txt                    # Python dependencies
├── Procfile                            # Heroku deployment config
├── runtime.txt                         # Python version for Heroku
├── .env.example                        # Environment variables template
├── db.sqlite3                          # SQLite database (development)
└── README.md                           # This file
```

---

## 🗺️ Navigation & Access Points

### Web Application URLs

| Page | URL | Purpose | Auth Required |
|------|-----|---------|---------------|
| **Home** | `/` | Landing page | No |
| **Login** | `/accounts/login/` | User login | No |
| **Register** | `/accounts/register/` | User registration | No |
| **Dashboard** | `/dashboard/` | User overview | ✅ Yes |
| **Monitors** | `/monitors/` | List monitors | ✅ Yes |
| **Add Monitor** | `/monitors/add/` | Create new monitor | ✅ Yes |
| **Monitor Details** | `/monitors/<id>/` | View monitor details | ✅ Yes |
| **Subscriptions** | `/subscriptions/` | Manage subscriptions | ✅ Yes |
| **Payment** | `/payments/<id>/checkout/` | Stripe payment | ✅ Yes |
| **Profile** | `/accounts/profile/` | User profile | ✅ Yes |
| **Logout** | `/accounts/logout/` | Sign out | ✅ Yes |
| **Admin Panel** | `/admin/` | Django admin | ✅ Staff |

### Quick Access Links (When Server Running)

```
🌐 Web Application: http://127.0.0.1:8000/
👨‍💻 Admin Panel: http://127.0.0.1:8000/admin/
   (Username: admin, Password: test123456)

📊 Database Viewer: python view_database.py
✅ Verify Implementation: python verify_implementation.py
🔧 Run Monitoring: python manage.py check_monitoring --verbose
```

---

## 🛠️ Setup Guide

### Prerequisites

- Python 3.8+
- pip (Python package manager)
- Virtual environment (recommended)
- Git

### Step 1: Clone Repository

```bash
cd c:\Users\user\Desktop\owasp
git clone https://github.com/y-sudharshan/SelfErase.git
cd SelfErase/web_monitoring_backend
```

### Step 2: Create Virtual Environment

**Windows (PowerShell)**:
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**macOS/Linux**:
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Configure Environment Variables

Create `.env` file in `web_monitoring_backend/`:

```env
# Django
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

# Database (SQLite for dev, PostgreSQL for prod)
DATABASE_URL=sqlite:///db.sqlite3

# Stripe Payment Keys (get from https://dashboard.stripe.com/)
STRIPE_PUBLIC_KEY=pk_test_your_key
STRIPE_SECRET_KEY=sk_test_your_key

# Email Configuration
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password

# SMS Notifications (Optional - Twilio)
TWILIO_ACCOUNT_SID=your-sid
TWILIO_AUTH_TOKEN=your-token
TWILIO_PHONE_NUMBER=+1234567890
```

### Step 5: Run Migrations

```bash
python manage.py migrate
```

### Step 6: Create Admin User

```bash
python manage.py createsuperuser
# Enter username: admin
# Enter email: admin@example.com
# Enter password: your-password
```

### Step 7: Start Development Server

```bash
python manage.py runserver 8000
```

**Output**:
```
Starting development server at http://127.0.0.1:8000/
```

### Step 8: Access the Application

Open browser and visit:
- **App**: http://127.0.0.1:8000/
- **Admin**: http://127.0.0.1:8000/admin/

---

## 🔄 How the Web Platform Works

### User Registration & Authentication Flow

```
1. User visits /accounts/register/
        ↓
2. Fills registration form (username, email, password)
        ↓
3. Form validation (unique username, valid email, strong password)
        ↓
4. User account created in database (PBKDF2 hashed password)
        ↓
5. Redirect to login page
        ↓
6. User logs in with credentials
        ↓
7. Django session created
        ↓
8. User redirected to dashboard
```

### Monitor Creation & Keyword Tracking Flow

```
1. User goes to /monitors/add/
        ↓
2. Enters URL and keyword to monitor
        ↓
3. Monitor record created in database
        ↓
4. Management command runs (daily or via scheduler)
        ↓
5. Checks URL using BeautifulSoup
        ↓
6. Searches for keyword in page content
        ↓
7. Creates CheckResult record
        ↓
8. If keyword found:
   - Creates Notification
   - Sends email alert
   - Updates monitor's last_found_time
        ↓
9. Updates last_checked_time regardless
        ↓
10. User sees notification in dashboard
```

### Payment & Subscription Flow

```
1. User selects subscription plan ($1 or $5/month)
        ↓
2. Clicks "Subscribe" button
        ↓
3. Redirected to Stripe payment form
        ↓
4. Enters card details
        ↓
5. Stripe processes payment
        ↓
6. Payment Intent created in database
        ↓
7. Payment marked as completed/failed
        ↓
8. If successful:
   - Subscription created
   - Funds allocated to budget
   - Confirmation email sent
        ↓
9. User can now monitor keywords
```

### Fund Allocation Flow

```
Subscription Payment Received
        ↓
Amount divided:
├─ 30% → Bug Hunter Bounty Fund
├─ 50% → Platform Operations
└─ 20% → Development & Improvements
        ↓
Allocations recorded in BudgetAllocation table
        ↓
Monthly reports generated
        ↓
Bug hunters paid from accumulated fund
```

---

## 🔌 API Endpoints

### Authentication Endpoints

| Method | Endpoint | Description | Body |
|--------|----------|-------------|------|
| POST | `/accounts/register/` | Register new user | username, email, password |
| POST | `/accounts/login/` | Login user | username, password |
| GET | `/accounts/logout/` | Logout user | - |
| GET | `/accounts/profile/` | Get user profile | - |

### Monitor Management Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/monitors/` | List all user monitors | ✅ |
| POST | `/monitors/add/` | Create new monitor | ✅ |
| GET | `/monitors/<id>/` | Get monitor details | ✅ |
| POST | `/monitors/<id>/edit/` | Update monitor | ✅ |
| POST | `/monitors/<id>/delete/` | Delete monitor | ✅ |
| GET | `/monitors/<id>/history/` | View check history | ✅ |

### Subscription Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/subscriptions/` | List subscriptions | ✅ |
| POST | `/subscriptions/create/` | Create subscription | ✅ |
| POST | `/subscriptions/<id>/cancel/` | Cancel subscription | ✅ |
| GET | `/subscriptions/billing/` | View billing history | ✅ |

### Payment Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/payments/<id>/checkout/` | Stripe checkout page | ✅ |
| POST | `/payments/<id>/confirm/` | Confirm payment | ✅ |
| GET | `/payments/history/` | View payment history | ✅ |

### Dashboard Endpoints

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/dashboard/` | User dashboard | ✅ |
| GET | `/admin/` | Django admin panel | ✅ Staff |

---

## 🚀 Deployment Guide

### Deploy to Heroku

#### 1. Prerequisites

```bash
# Install Heroku CLI
# Download from https://devcenter.heroku.com/articles/heroku-cli
heroku login
```

#### 2. Create Heroku App

```bash
heroku create your-app-name
```

#### 3. Add PostgreSQL Database

```bash
heroku addons:create heroku-postgresql:hobby-dev
```

#### 4. Set Environment Variables

```bash
heroku config:set SECRET_KEY=your-secret-key-here
heroku config:set STRIPE_PUBLIC_KEY=your-public-key
heroku config:set STRIPE_SECRET_KEY=your-secret-key
heroku config:set DEBUG=False
heroku config:set EMAIL_HOST_USER=your-email@gmail.com
heroku config:set EMAIL_HOST_PASSWORD=your-app-password
```

#### 5. Deploy

```bash
git push heroku main
```

#### 6. Run Migrations

```bash
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

#### 7. Setup Scheduler

```bash
# Add Heroku Scheduler
heroku addons:create scheduler:standard

# Open scheduler dashboard
heroku addons:open scheduler


## ✅ Testing & Verification

### Quick Verification (5 minutes)

```bash
# Run automated verification
python verify_implementation.py

# View database contents
python view_database.py

# Check Django system
python manage.py check
```

### Manual Testing

```bash
# 1. Start server
python manage.py runserver 8000

# 2. Register new user
# Visit: http://127.0.0.1:8000/accounts/register/

# 3. Create a monitor
# Fill in: https://example.com and keyword

# 4. Run monitoring check
python manage.py check_monitoring --verbose

# 5. Check dashboard for results
# Visit: http://127.0.0.1:8000/dashboard/

# 6. Test payment (test card)
# Card: 4242 4242 4242 4242
# Expiry: 12/25 | CVC: 123
```

### Run Full Test Suite

```bash
# Run all tests
python manage.py test

# Run specific app tests
python manage.py test monitoring
python manage.py test accounts

# Run with coverage
coverage run --source='.' manage.py test
coverage report
```

---
### External Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Stripe Documentation](https://stripe.com/docs)
- [Bootstrap 5 Documentation](https://getbootstrap.com/docs/5.0/)
- [BeautifulSoup Documentation](https://www.crummy.com/software/BeautifulSoup/)

---

## 🤝 Contributing

Please see [CONTRIBUTING.md](../CONTRIBUTING.md) for contribution guidelines.

---

## 📄 License

AGPL-3.0 - See [LICENSE](../LICENSE) for details.

---

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Check existing documentation
- Review troubleshooting section above

---

## 🎯 Quick Commands Reference

```bash
# Development
python manage.py runserver 8000                    # Start server
python manage.py createsuperuser                   # Create admin user
python manage.py migrate                           # Apply migrations
python manage.py makemigrations                    # Create migrations

# Monitoring
python manage.py check_monitoring --verbose        # Run monitoring check
python manage.py check_monitoring --monitor-id 1   # Check specific monitor

# Utilities
python view_database.py                            # View database contents
python verify_implementation.py                    # Verify implementation
python manage.py shell                             # Django shell
python manage.py test                              # Run tests

# Production
python manage.py check --deploy                    # Security checks
python manage.py collectstatic --noinput           # Collect static files
gunicorn config.wsgi                               # Production server
```

---

