# বাজার দর — বাংলা সেটআপ গাইড

## ১. কী কী লাগবে
- Node.js 20.9 বা তার বেশি (Node 22 LTS ভালো)
- MongoDB Atlas account ও database user
- Google Cloud OAuth Client ID/Secret
- GitHub OAuth App Client ID/Secret

## ২. প্রজেক্ট চালু করুন
টার্মিনালে project folder খুলে চালান:

```bash
npm install
```

`.env.example` ফাইলটি কপি করে `.env.local` বানান। এরপর MongoDB URI, Better Auth secret এবং OAuth credentials বসান।

## ৩. MongoDB Atlas
1. MongoDB Atlas-এ একটি free cluster তৈরি করুন।
2. Database Access থেকে username/password তৈরি করুন।
3. Network Access-এ development-এর জন্য আপনার IP allow করুন।
4. Connect → Drivers থেকে connection string কপি করে `MONGODB_URI`-তে দিন।
5. URI-তে username/password-এর special character URL encode করতে হবে।

## ৪. Better Auth secret
`BETTER_AUTH_SECRET`-এ অন্তত ৩২ অক্ষরের একটি random secret দিন। উদাহরণ তৈরি:

```bash
openssl rand -base64 32
```

## ৫. Google ও GitHub OAuth

**Google:** Google Cloud Console → APIs & Services → Credentials → OAuth Client ID → Web application। Authorized redirect URI:

`http://localhost:3000/api/auth/callback/google`

**GitHub:** GitHub Settings → Developer settings → OAuth Apps → New OAuth App। Authorization callback URL:

`http://localhost:3000/api/auth/callback/github`

দুই provider-এর Client ID ও Client Secret `.env.local`-এ বসান। Production-এ deployed domain দিয়ে callback URL নতুন করে যোগ করবেন।

## ৬. Local server

```bash
npm run dev
```

Browser-এ `http://localhost:3000` খুলুন।

## ৭. Vercel deploy
1. GitHub-এ project push করুন।
2. Vercel-এ repository import করুন।
3. Settings → Environment Variables-এ `.env.example`-এর সব variable যোগ করুন।
4. `BETTER_AUTH_URL` এবং `NEXT_PUBLIC_APP_URL`-এ production URL দিন।
5. Google/GitHub OAuth callback-এ production domain যোগ করুন।
6. Deploy দিন।

## গুরুত্বপূর্ণ
- Email verification ও forgot password রাখা হয়নি — assignment requirement অনুযায়ী।
- Product details ও profile route login ছাড়া খোলা যাবে না।
- OAuth credential না দিলে Email/Password authentication ব্যবহার করা যাবে; Google/GitHub login চালাতে credentials লাগবে।
- API-র দাম সম্ভাব্য; বাজারভেদে পরিবর্তিত হতে পারে।
