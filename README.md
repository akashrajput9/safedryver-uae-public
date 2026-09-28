# SafeDryver

SafeDryver is a Dubai-based mobility platform. One Laravel 12 codebase serves a public customer website, an admin
dashboard, and the REST APIs behind five mobile apps (customer, chauffeur driver, driver-only driver, PD driver and
vendor).

## What the platform does

| Vertical | Description |
|---|---|
| Chauffeur rides | A car with a professional driver: trips, hourly, daily, weekly or monthly bookings |
| Driver-only | A driver for the customer's own car (trip, hourly or daily) |
| PD assignments | Driver-only bookings offered to personal (PD) drivers, who accept or decline within a time limit |
| Car rental | Self-drive rentals from vendor fleets, with add-ons and insurance |
| Marketplace | Buying and selling cars, with favourites and comparison |
| Private jets | Charter quote requests and bookings |
| Yachts | Yacht trips with catering and water-sports options |
| Packages | Subscription packages across the verticals |

The admin dashboard also covers customers, drivers, vendors, support tickets, customer chat, WhatsApp chats,
customer contracts (with PDF export), CMS pages, FAQs and feedback.

## Tech stack

- **Backend:** PHP 8.4, Laravel 12, Laravel Passport (OAuth2 API auth), Laravel Reverb (WebSockets)
- **Frontend:** Inertia.js v2 + React 18 + TypeScript, Tailwind CSS v3, shadcn/Radix UI components
- **Payments:** Stripe (cards, Apple Pay, Google Pay) plus an in-app wallet
- **Integrations:** Firebase Cloud Messaging (push), Meta WhatsApp Cloud API, OpenTok (voice/video calls),
  Sign in with Apple, Discord (booking notifications), DomPDF (contract PDFs)
- **Tests:** PHPUnit 11

## How it's organised

**Six separate user types.** There is no single `User` model. Each persona has its own model, Passport guard and route
file:

| Guard | Model | Routes | Used by |
|---|---|---|---|
| `api-customer` | `Customer` | `routes/customer.php` | Customer app |
| `api-driver` | `Driver` | `routes/driver.php` | Chauffeur driver app |
| `api-driver-only` | `DriverOnlyDriver` | `routes/driver_only.php` | Driver-only app |
| `api-pd-driver` | `PDDriver` | `routes/pd.php` | PD driver app |
| `api-vendor` | `Vendor` | `routes/vendor.php` | Vendor app |
| `api-admin` | `Admin` | `routes/api-admin.php` | Admin API / MCP server |
| `customer_web` / `admin_web` | `Customer` / `Admin` | `routes/web.php` / `routes/admin.php` | Website / admin dashboard (session) |
