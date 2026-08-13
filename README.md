# GetPlaced

GetPlaced is a Django-based placement/job portal that connects **colleges** and **companies**. Colleges register their students, companies post jobs, and colleges can "raise a ticket" to a company to request a placement drive connection — which, once approved, opens a live chat between the two parties. It's a three-sided platform (College, Company, and a searchable public front-end) built with Python/Django and vanilla HTML/CSS/JS templates.

## Features

### Public / Home
- Landing page showcasing verified colleges and companies
- Live search (AJAX-powered) across colleges, companies, and job listings by name, location, or skills
- Browsable, filterable directory of all verified colleges and companies, sorted by rating

### College Portal
- College registration (with logo upload) and login
- Dashboard to add, edit, and delete student records (name, registration no., branch, year, skills, contact, photo)
- Browse all currently open job postings from verified companies
- Raise a "ticket" to a company to request a placement connection
- Once a company approves a ticket, chat directly with that company

### Company Portal
- Company registration (with logo upload) and login
- Dashboard to post, edit, and delete job openings (title, description, location, type, required skills, salary, last date to apply, contact email)
- View incoming tickets from colleges requesting a placement drive
- Approve ("connect") a ticket to unlock chat with that college
- Chat with connected colleges

### Admin
- Django admin site for verifying colleges/companies (`admin_verified` flag) and managing all records directly

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Django |
| Database | SQLite (Django ORM) |
| Frontend | HTML, CSS, JavaScript (Django Templates, AJAX) |
| Media | Django `ImageField` uploads for logos/photos (colleges, companies, students) |

## Project Structure

```
GetPlaced/
└── job_portal/
    ├── job_portal/                 # Django project configuration
    │   ├── settings.py
    │   ├── urls.py
    │   ├── asgi.py
    │   └── wsgi.py
    ├── portal/                     # Main application
    │   ├── models.py                # college, student, company, job, ticket, ChatMessage
    │   ├── views.py                  # Registration, login, dashboards, search, ticketing, chat
    │   ├── urls.py                    # App-level URL routes
    │   ├── admin.py                    # Django admin registrations
    │   ├── templates/                   # HTML pages (dashboards, listings, chat, etc.)
    │   ├── static/                       # CSS, JS, and image assets
    │   └── migrations/
    ├── manage.py
    └── requirements.txt
```

## Core Models

- **college** — college profile (name, location, university, logo, contact info, registration credentials, admin-verified flag, rating)
- **company** — company profile (name, location, logo, contact info, registration credentials, admin-verified flag, rating)
- **student** — student record linked to a college (name, reg. no., branch, year, skills, photo, contact)
- **job** — job posting linked to a company (title, description, location, type, required skills, salary, posting/expiry dates, contact email)
- **ticket** — a connection request from a college to a company, with a status lifecycle (`pending` → `connect` / `rejected` / `cancelled`)
- **ChatMessage** — individual chat messages tied to a `ticket`, once that ticket is connected

## Getting Started

### Prerequisites
- Python 3.x
- pip

### Installation

1. Clone the repository
   ```bash
   git clone https://github.com/Prabhat2811/GetPlaced.git
   cd GetPlaced/job_portal
   ```

2. (Optional but recommended) Create and activate a virtual environment
   ```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. Install dependencies
   ```bash
   pip install -r requirements.txt
   ```

4. Apply database migrations
   ```bash
   python manage.py migrate
   ```

5. (Optional) Create a superuser to access the Django admin and verify colleges/companies
   ```bash
   python manage.py createsuperuser
   ```

6. Run the development server
   ```bash
   python manage.py runserver
   ```

7. Open the app in your browser at `http://127.0.0.1:8000/`

## Usage

- From the home page, search for colleges, companies, or jobs, or browse the full directories.
- Register a college or company account — new accounts stay unverified until approved via `/admin/`, at which point they become visible in listings and searches.
- Once verified, log in as a **college** to add students and browse open jobs, or as a **company** to post jobs and review incoming connection tickets.
- A college can raise a ticket to a company it's interested in; once the company connects the ticket, both sides can chat.

## Roadmap / Possible Improvements

- Move authentication to Django's built-in `auth` system with hashed passwords (registration/login passwords are currently stored and compared as plain text, despite `make_password`/`check_password` being imported)
- Add CSRF protection to `raise_ticket` (currently marked `@csrf_exempt`)
- Add pagination for large college/company/job listings
- Add email notifications when a ticket is approved or a new chat message arrives
- Add automated tests (`tests.py` is currently a stub)

## Author

**Prabhat Ranjan**
- GitHub: [Prabhat2811](https://github.com/Prabhat2811)
- LinkedIn: [prabhat-ranjan-29801422a](https://linkedin.com/in/prabhat-ranjan-29801422a)
- LeetCode: [Prabhat2811](https://leetcode.com/u/Prabhat2811/)
