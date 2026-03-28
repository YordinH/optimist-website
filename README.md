# Optimist Website

Official website for [Optimist PCs](https://optimist.gg)

---

## Tech Stack

| Layer | Tool |
|---|---|
| Framework | SvelteKit 2 (Svelte 5) |
| Language | TypeScript |
| Styling | Tailwind CSS + Typography plugin |
| Components | shadcn-svelte |
| Animation | GSAP + ScrollTrigger + Lenis |
| Images | Cloudinary (svelte-cloudinary) |
| Database | Supabase |
| Auth | Supabase Auth |
| Payments | Stripe |
| Email (transactional) | Resend |
| Email (marketing) | Klaviyo (maybe?) |
| Shipping | Shippo API |
| Analytics | Supabase custom + Google Analytics 4 |
| Package Manager | npm |
| Hosting | Vercel |

---

## Project Structure

```
optimist-website/
├── src/
│   ├── lib/
│   │   ├── components/     # Shared UI components
│   │   ├── server/         # Server-only utilities (Supabase admin, Stripe, Resend)
│   │   ├── stores/         # Svelte stores
│   │   ├── types/          # TypeScript types + Supabase generated types
│   │   └── utils/          # Helper functions
│   ├── routes/
│   │   ├── (public)/       # Public-facing pages
│   │   ├── (admin)/        # Admin dashboard (protected)
│   │   └── api/            # API endpoints
│   └── app.html            # Root HTML (GA4 script tag goes here, check for permissions!)
├── static/                 # Static assets (fonts, icons)
├── .env                    # Environment variables (never commit)
├── .env.example            # Example env file (safe to commit)
└── svelte.config.js
```

---

## Getting Started

### Prerequisites

- Node.js (nvm use 22)
- npm

### Installation

bash
# Clone the repo
git clone https://github.com/YordinH/optimist-website.git
cd optimist-website

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env
# Fill in your keys in .env

# Start dev server
npm run dev

---

## Environment Variables

Create a `.env` file in the root. Never commit this file.

```bash
# Supabase
PUBLIC_SUPABASE_URL=
PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Stripe
PUBLIC_STRIPE_PUBLISHABLE_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

# Resend
RESEND_API_KEY=

# Cloudinary
PUBLIC_CLOUDINARY_CLOUD_NAME=

# Shippo
SHIPPO_API_KEY=
```


---

## Development Notes

### Supabase Type Generation

After any database schema changes, regenerate TypeScript types:

```bash
npx supabase gen types typescript --project-id your-project-id > src/lib/types/database.types.ts
```

### Adding shadcn-svelte Components

```bash
npx shadcn-svelte@latest add [component-name]
```

### GSAP + Lenis

GSAP and Lenis are initialized globally. ScrollTrigger is registered in the root layout. Always respect `prefers-reduced-motion` when building animations.

### Stripe Webhooks (local dev)

Use the Stripe CLI to forward webhooks locally:

```bash
stripe listen --forward-to localhost:5173/api/webhooks/stripe
```

---

## Deployment

Deployed on Vercel via the official SvelteKit Vercel adapter. Pushes to `main` trigger automatic production deployments.

```bash
npm run build    # Build for production
npm run preview  # Preview production build locally
```