# 🛒 বাজার দর (BazarDor)

বাংলাদেশের নিত্যপ্রয়োজনীয় পণ্যের দৈনিক বাজারদর, দাম বাড়া-কমা এবং বিভিন্ন বাজারের মূল্য তুলনা করার একটি responsive web application। BazarDor API থেকে পণ্যের তথ্য নিয়ে ব্যবহারকারীকে সহজ বাংলায় বাজারের আপডেট দেখায়।

## ✨ Key Features

1. **Live market overview** — দাম বেড়েছে/কমেছে এমন পণ্যের তালিকা এবং infinite price ticker।
2. **Product directory** — ৮টি ক্যাটাগরি ও API-তে থাকা পণ্য responsive card grid-এ দেখা।
3. **Category sorting** — বাংলা UI-তে দাম কম থেকে বেশি বা বেশি থেকে কম; numeric price sorting।
4. **Protected product details** — লগইন করা ব্যবহারকারী বাজারভিত্তিক minimum, maximum, average এবং market table দেখতে পারবেন।
5. **Authentication** — Better Auth দিয়ে email/password, Google এবং GitHub sign-in/sign-up।
6. **Profile management** — নিজের নাম দেখা ও Better Auth `updateUser` দিয়ে আপডেট করা।
7. **Responsive UI** — mobile, tablet ও desktop layout, skeleton loading, toast feedback এবং custom 404 page।

## 🧰 Technologies

- Next.js 15 App Router + React 19
- TypeScript
- Tailwind CSS v4 (custom component styling)
- Better Auth + MongoDB adapter
- MongoDB Atlas
- React Hot Toast
- Lucide React
- BazarDor REST API

## 📁 Folder Structure

```text
src/
  app/
    api/auth/[...all]/route.ts
    category/[slug]/page.tsx
    product/[slug]/page.tsx
    signin/page.tsx
    signup/page.tsx
    profile/page.tsx
    profile/update/page.tsx
    layout.tsx
    page.tsx
    loading.tsx
    not-found.tsx
    globals.css
  components/
  lib/
```

## 🚀 Local Setup

### 1. Requirements

- Node.js 20.9+ (Node.js 22 LTS recommended)
- npm
- MongoDB Atlas database
- Google OAuth credentials (optional until Google sign-in is used)
- GitHub OAuth credentials (optional until GitHub sign-in is used)

### 2. Install

```bash
npm install
```

### 3. Environment variables

Copy `.env.example` to `.env.local` and fill in your values:

```env
BETTER_AUTH_SECRET=your-long-random-secret-at-least-32-characters
BETTER_AUTH_URL=http://localhost:3000
NEXT_PUBLIC_APP_URL=http://localhost:3000
MONGODB_URI=mongodb+srv://USERNAME:PASSWORD@CLUSTER.mongodb.net/?retryWrites=true&w=majority
MONGODB_DB_NAME=bazardor
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret
NEXT_PUBLIC_API_BASE_URL=https://api.api-store.workers.dev/api/bazardor
```

Generate a secret with `openssl rand -base64 32` or another secure random generator. Never commit `.env.local`.

### 4. OAuth callback URLs

For local development, configure these callback URLs in Google Cloud Console and GitHub OAuth App:

- `http://localhost:3000/api/auth/callback/google`
- `http://localhost:3000/api/auth/callback/github`

For production, replace the host with your deployed domain, for example `https://your-domain.vercel.app/api/auth/callback/google` and `/api/auth/callback/github`.

### 5. Run

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### 6. Production build

```bash
npm run build
npm run start
```

## 🌐 API Endpoints

Base URL: `https://api.api-store.workers.dev/api/bazardor`

- `GET /categories` — all categories
- `GET /categories/:slug` — one category
- `GET /products` — all products
- `GET /products?category=chal` — products by category
- `GET /products/:id` — product details including market prices

## ☁️ Vercel Deployment

1. Push the project to GitHub.
2. Import the repository in Vercel.
3. Add every variable from `.env.example` in **Project → Settings → Environment Variables**.
4. Set `BETTER_AUTH_URL` and `NEXT_PUBLIC_APP_URL` to the deployed origin (without a trailing slash).
5. Add production OAuth callback URLs in Google and GitHub settings.
6. Deploy. Vercel automatically uses `npm run build`; App Router dynamic routes work on direct navigation and refresh.

## 🔐 Authentication Notes

- Email verification and password reset are intentionally not implemented for this assignment.
- Product detail routes and profile routes check the Better Auth session on the server.
- Google/GitHub OAuth requires valid client IDs and secrets; the buttons are shown in the UI but will not complete OAuth until credentials and callback URLs are configured.

## ⚠️ Data Note

Prices are indicative and depend on market conditions. The application displays API-provided data; it does not claim that prices are guaranteed or real-time at every market.
