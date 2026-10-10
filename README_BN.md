# বাই সেল বিডি — Marketplace Starter

এটি বাই সেল বিডিের প্রথম ধাপের starter project: Flutter Android app, Next.js website, NestJS API এবং PostgreSQL।

## গুরুত্বপূর্ণ
- এই প্যাকেজটি হলো **চালু করার উপযোগী প্রাথমিক কাঠামো**, সম্পূর্ণ production marketplace নয়।
- bKash/Nagad-এর বাস্তব পেমেন্ট চালু করতে merchant account, provider-এর অনুমোদিত API credentials এবং তাদের সর্বশেষ integration documentation লাগবে। Secret কখনো Flutter/website-এ রাখবেন না; শুধু backend `.env`-এ রাখবেন।
- মোবাইল দিয়ে কাজ করতে GitHub Codespaces বা অন্য browser-based development environment ব্যবহার করা সবচেয়ে সহজ। Android APK build করতে cloud build/CI বা Android Studio-সহ কম্পিউটার লাগতে পারে।
- production-এ deploy করার আগে authentication, rate limiting, input validation, file upload security, payment callback verification, privacy policy এবং security testing সম্পন্ন করতে হবে।

## ফোল্ডার
- `apps/api` — NestJS API
- `apps/web` — Next.js website
- `apps/mobile` — Flutter app starter
- `infra` — PostgreSQL Docker Compose
- `.env.example` — environment settings-এর নমুনা

## শুরু করার প্রস্তাবিত ধাপ (মোবাইল থেকে)
1. ZIP ফাইলটি ডাউনলোড করে GitHub-এ একটি private repository তৈরি করুন এবং ফাইলগুলো upload করুন।
2. GitHub Codespaces-এ repository খুলুন।
3. Node.js 20+ এবং Flutter SDK আছে কি না যাচাই করুন। Codespaces-এ Flutter আগে থেকে নাও থাকতে পারে।
4. `infra/docker-compose.yml`-এর PostgreSQL চালাতে Docker-enabled environment লাগবে। বিকল্প হিসেবে managed PostgreSQL ব্যবহার করুন।
5. `apps/api`-এ `.env.example` কপি করে `.env` বানান, তারপর `npm install` ও `npm run start:dev` চালান।
6. `apps/web`-এ `npm install` ও `npm run dev` চালান।
7. Flutter app চালাতে Flutter SDK এবং Android device/emulator বা cloud build দরকার।

## API endpoint
- `GET /health` — API health check
- `GET /listings` — বিজ্ঞাপনের তালিকা
- `POST /listings` — starter listing create endpoint (এখনো production authentication যুক্ত হয়নি)

## bKash/Nagad
এই starter-এ payment integration ইচ্ছাকৃতভাবে নিরাপদ placeholder হিসেবে রাখা হয়েছে। বাস্তব transaction flow যোগ করার আগে:
1. bKash ও Nagad merchant onboarding সম্পন্ন করুন।
2. provider-এর বর্তমান official API docs অনুযায়ী backend service implement করুন।
3. create-payment, execute/verify, callback/webhook signature/verification, idempotency, refund/cancel এবং transaction reconciliation যোগ করুন।
4. কোনো payment success শুধু browser redirect দেখে বিশ্বাস করবেন না; server-side verification আবশ্যক।
