# Supplier.sa

> A bilingual supplier discovery and business directory platform for Saudi Arabia.

Supplier.sa helps businesses discover, compare, and connect with suppliers, stores, manufacturers, offices, and service providers across the Kingdom. The platform combines searchable business listings, category and location filtering, interactive maps, supplier profiles, business-owner dashboards, administration tools, bilingual Arabic/English support, and ClickPay subscription integration.

**Live demo:** [supplier-rust.vercel.app](https://supplier-rust.vercel.app)

## Highlights

- **Supplier directory** with business cards, ratings, reviews, service areas, verification badges, and business types.
- **Smart search and filtering** by keyword, category, location, business type, rating, distance, and services.
- **Interactive maps** powered by Leaflet and Google Maps embeds, including supplier locations and directions.
- **Bilingual interface** with Arabic and English translations, RTL support, and persisted language selection.
- **Business onboarding** with registration, verification-code flow, profile completion, working hours, branches, services, and contact information.
- **Supplier dashboard** for business profiles, analytics, messages, settings, profile themes, and avatar customization.
- **Admin control panel** with user, employee, content, analytics, and system settings sections.
- **AI-assisted discovery UI** through the AI chat widget and AI filter bar.
- **ClickPay subscriptions** with configurable Basic, Professional, and Enterprise plans, payment creation, status queries, and refunds.
- **Responsive UI** built with Tailwind CSS, Framer Motion animations, Remix Icon, and mobile-friendly layouts.

## Technology Stack

- **Framework:** Next.js 14 App Router
- **Runtime:** React 18
- **Language:** TypeScript
- **Styling:** Tailwind CSS 3, custom CSS, Remix Icon
- **Maps:** Leaflet, MapTiler Leaflet SDK, and Google Maps embeds
- **Payments:** ClickPay API through Axios
- **Animations:** Framer Motion
- **UI utilities:** React Icons and Swiper
- **Internationalization:** Custom translation context with Arabic and English dictionaries

## Project Structure

```text
Supplier/
├── app/
│   ├── page.tsx                    # Homepage and main discovery experience
│   ├── businesses/                 # Searchable supplier directory
│   ├── business/                   # Public business profile pages
│   ├── add-business/               # Business registration form
│   ├── register/ and auth/         # Registration, sign-in, and verification flows
│   ├── complete-profile/           # Supplier profile completion flow
│   ├── dashboard/                  # Supplier dashboard
│   ├── admin/                      # Administration panel
│   ├── subscription/               # Subscription plans and checkout entry point
│   ├── api/payment/                # ClickPay create, callback, and status routes
│   ├── about/                      # About page
│   ├── business-guides/            # Business guidance content
│   ├── help-center/                # Help center
│   ├── support/                    # Support page
│   ├── privacy/, terms/, cookie-policy/ # Legal and privacy pages
│   ├── layout.tsx                  # Global metadata, fonts, RTL shell, and providers
│   └── globals.css                 # Tailwind layers and map/UI customizations
├── components/                     # Reusable UI and feature components
│   ├── SearchSection.tsx           # Search, category selection, map, and request form
│   ├── BusinessFilters.tsx         # Directory filters
│   ├── BusinessCard.tsx            # Supplier card grid/list presentation
│   ├── InteractiveMap.tsx           # Interactive supplier map
│   ├── AIChatWidget.tsx             # AI chat experience
│   ├── AIFilterBar.tsx              # AI-powered filtering interface
│   ├── Dashboard*.tsx               # Supplier dashboard modules
│   ├── Admin*.tsx                   # Administration modules
│   ├── ClickPay*.tsx                # Payment UI components
│   └── Header.tsx / Footer.tsx      # Shared site chrome
├── lib/
│   ├── LanguageContext.tsx          # Arabic/English state and translation helper
│   ├── translations.ts              # Translation dictionary
│   ├── types.ts                     # Shared business and form types
│   ├── initialData.ts                # Initial business-profile form state
│   └── clickpay/                    # ClickPay configuration, types, service, utilities
├── public/                          # Logos, icons, Saudi flag, and social preview assets
├── CLICKPAY_SETUP.md                 # ClickPay integration setup guide
├── package.json                      # Scripts and dependencies
├── tailwind.config.js                # Tailwind content paths and RTL utility
└── next.config.js                    # Next.js configuration
```

## Getting Started

### Prerequisites

- Node.js 18 or newer
- npm
- A ClickPay merchant account if subscription payments are required

### Installation

```bash
git clone https://github.com/abo3tef/Supplier.git
cd Supplier
npm install
```

### Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Production build

```bash
npm run build
npm run start
```

### Linting

```bash
npm run lint
```

## Environment Variables

Create a `.env.local` file in the project root when enabling ClickPay payments:

```env
NEXT_PUBLIC_CLICKPAY_PROFILE_ID=your_profile_id
CLICKPAY_SERVER_KEY=your_server_key
NEXT_PUBLIC_CLICKPAY_CLIENT_KEY=your_client_key
NEXT_PUBLIC_CLICKPAY_BASE_URL=https://secure.clickpay.com.sa
```

### Environment variable notes

- `CLICKPAY_SERVER_KEY` is sensitive and must remain server-side.
- The public ClickPay values may be exposed to the browser when required by the integration.
- Use sandbox credentials during development and production credentials only over HTTPS.
- See [`CLICKPAY_SETUP.md`](./CLICKPAY_SETUP.md) for the payment flow, callback URL, test cards, and production checklist.

## Main User Flows

### Discover suppliers

1. Start from the homepage search section.
2. Search by supplier name, category, or location.
3. Browse map markers or open the full `/businesses` directory.
4. Refine results using filters and sorting.
5. Open a supplier profile or contact the business.

### Register a business

1. Open `/register` or `/auth`.
2. Enter business and contact details.
3. Select phone or email verification.
4. Enter the four-digit verification code.
5. Continue to `/complete-profile` to add business details, services, hours, branches, and location.

### Manage a supplier account

Open `/dashboard` to access:

- Overview statistics
- Business profile management
- Analytics
- Messages
- Account and dashboard settings

### Manage the platform

Open `/admin` to access the administration sections for users, employees, content, analytics, and system settings.

## ClickPay Integration

The payment integration is organized around the following modules:

- `lib/clickpay/config.ts` — ClickPay configuration, subscription plans, and API endpoints.
- `lib/clickpay/service.ts` — Payment creation, transaction queries, refunds, validation, and cart IDs.
- `lib/clickpay/utils.ts` — Currency formatting, Saudi phone validation, VAT calculation, callback URLs, and payment status helpers.
- `components/ClickPayButton.tsx` and `components/ClickPayPaymentForm.tsx` — Payment UI.
- `app/api/payment/create` — Payment creation endpoint.
- `app/api/payment/callback` — Payment callback handling.
- `app/api/payment/status` — Transaction status lookup.

The configured plans are Basic, Professional, and Enterprise, with prices and features defined in `lib/clickpay/config.ts`.

## Data and Demo Status

The current application includes demo-oriented flows and sample data in several areas. For example, the directory page contains mock business records, authentication uses simulated sign-in/verification behavior, and dashboard/admin screens include representative user data. Before production use, connect these flows to a secure backend, database, real authentication provider, and server-side authorization layer.

## Security Checklist for Production

- Never expose the ClickPay server key in client-side code.
- Replace simulated authentication and hard-coded user state with real authentication and authorization.
- Store business listings, messages, subscriptions, and analytics in a persistent database.
- Validate and authorize every dashboard, admin, and payment operation on the server.
- Verify payment callbacks/webhooks before updating subscription status.
- Configure HTTPS, secure cookies, rate limiting, input validation, and error monitoring.
- Replace demo credentials and sample business data before deployment.

## Available Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Next.js development server |
| `npm run build` | Create a production build |
| `npm run start` | Start the production server |
| `npm run lint` | Run the configured Next.js lint command |

## Contributing

1. Create a feature branch from `main`.
2. Keep components and shared logic organized under `components/` and `lib/`.
3. Preserve Arabic/English translation coverage for user-facing text.
4. Run the build and lint commands before opening a pull request.
5. Document new environment variables and integration changes.

## License

No license has been declared for this repository yet. Add a `LICENSE` file before distributing or reusing the project publicly.
