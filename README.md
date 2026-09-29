# Smart Expense Tracker

Django-based Smart Expense Tracker with:

- 30-day free trial after account creation
- ₹99 Premium after the trial ends
- Login opens the dashboard during the active trial
- After trial expiry, login sends the user to the ₹99 Premium payment page
- Premium access is activated only after verified payment
- Dashboard, transactions, budgets, reports, EMI tracking, profile and receipt uploads
- Receipt/OCR interface included in the project

## Trial and Premium flow

1. User opens the website and selects **Start Free Trial**.
2. User creates an account. No payment is required at signup.
3. A 30-day trial starts automatically.
4. During the trial, normal login opens the dashboard.
5. After 30 days, login redirects to the ₹99 Premium page.
6. A successful Razorpay payment is verified on the server.
7. The user's Premium status becomes active and the dashboard opens.

## Local setup

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

Open http://127.0.0.1:8000/

## Payment configuration

Set these environment variables for real Razorpay payments:

- `RAZORPAY_KEY_ID`
- `RAZORPAY_KEY_SECRET`
- `REGISTRATION_FEE=99.00`
- `PAYMENT_DEMO_MODE=0`

`PAYMENT_DEMO_MODE=1` is for local testing only. Do not enable it for real payments.

## Important production notes

Before public deployment, set a strong secret key, `DEBUG=False`, a correct `ALLOWED_HOSTS`, HTTPS/secure cookie settings, and use PostgreSQL or another production database. Do not put Razorpay secret keys in source code.

The fallback static UPI QR cannot itself verify a payment. For automatic Premium activation, use the verified Razorpay flow.
