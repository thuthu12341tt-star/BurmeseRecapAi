# BurmeseRecapAi — Android starter project

ဒီ project က Android Studio မှာဖွင့်ပြီး APK build လုပ်နိုင်တဲ့ starter source ဖြစ်ပါတယ်။
**ဒီ ZIP ထဲမှာ APK မပါသေးပါ** — APK ကို Android Studio မှာ build လုပ်ရပါမယ်။

## ပါဝင်တာ
- Native Android app (Kotlin + XML)
- English movie recap → Burmese narration translation
- Translate / Copy / Clear
- Backend မှတစ်ဆင့် AI API ချိတ်ဆက်ခြင်း
- API key ကို Android app ထဲမထည့်ဘဲ backend `.env` ထဲမှာထားခြင်း

## 1) AI API key ထည့်ရန် (Backend)
လိုအပ်ချက်: Node.js 18+

```bash
cd backend
npm install
cp .env.example .env
```

`.env` ကိုဖွင့်ပြီး သင့် OpenAI API key ထည့်ပါ။
`OPENAI_MODEL` ကို သင့် account မှာ အသုံးပြုခွင့်ရှိတဲ့ model နဲ့ သတ်မှတ်ပါ။

```env
OPENAI_API_KEY=your_api_key_here
OPENAI_MODEL=gpt-4.1-mini
PORT=3000
```

ပြီးရင် backend ကို run ပါ။

```bash
npm start
```

ပုံမှန်အားဖြင့် `http://localhost:3000` မှာ အလုပ်လုပ်ပါမယ်။
ဖုန်းအစစ်ကနေ စမ်းမယ်ဆိုရင် ဖုန်းနဲ့ ကွန်ပျူတာကို Wi-Fi တစ်ခုတည်းချိတ်ပြီး ကွန်ပျူတာရဲ့ LAN IP ကို Android app ရဲ့ `API_BASE_URL` မှာ ထည့်ပါ။ Production အတွက် HTTPS server တင်ပါ။

## 2) Android app ဖွင့်ရန်
1. Android Studio ကို install လုပ်ပါ။
2. ဒီ folder ကို Android Studio မှာ Open လုပ်ပါ။
3. `app/build.gradle.kts` ရဲ့ `API_BASE_URL` ကို သင့် backend URL နဲ့ ပြောင်းပါ။
   - Android Emulator အတွက်: `http://10.0.2.2:3000/`
   - ဖုန်းအစစ်အတွက်: `https://your-server-domain/` (အကြံပြု)
4. Gradle Sync လုပ်ပါ။
5. Run ခလုတ်နှိပ်ပြီး စမ်းပါ။

## 3) APK ထုတ်ရန်
Android Studio → Build → Build Bundle(s) / APK(s) → Build APK(s)

Debug APK ကို `app/build/outputs/apk/debug/app-debug.apk` မှာ ရပါမယ်။

## လုံခြုံရေး
- `OPENAI_API_KEY` ကို APK, Git repository, screenshot တို့ထဲ မထည့်ပါနှင့်။
- Backend ကို public internet ပေါ်တင်မယ်ဆိုရင် authentication, rate limiting, usage limits တို့ ထပ်ထည့်ပါ။
- API သုံးစွဲခ ကုန်ကျနိုင်ပါတယ်။ API key ရဲ့ billing/limits ကို စောင့်ကြည့်ပါ။

## မှတ်ချက်
ဒီဟာက စတင်အသုံးပြုနိုင်တဲ့ prototype ဖြစ်ပါတယ်။ Production release မလုပ်ခင် HTTPS, authentication, rate limiting, privacy policy, error handling နဲ့ device testing ထပ်လုပ်ပါ။

## ဖုန်းတစ်လုံးတည်းနဲ့ Cloud Build လုပ်ရန်
ဒီ project မှာ `.github/workflows/android-apk.yml` ပါဝင်ပါတယ်။ GitHub repository ထဲ source code တင်ပြီး Actions ကို run လုပ်လျှင် cloud က APK build လုပ်ပေးပါမယ်။

1. GitHub account ဖွင့်ပါ (မရှိသေးလျှင်)။
2. ဖုန်း browser မှ `github.com` ဝင်ပြီး repository အသစ်တစ်ခု Create လုပ်ပါ။ Private repository အဖြစ်ထားနိုင်ပါတယ်။
3. ZIP ကို ဖုန်းထဲ Extract လုပ်ပြီး project အတွင်းရှိ file/folder အားလုံးကို repository ထဲတင်ပါ။ `.github` folder ပါဝင်ရပါမယ်။
4. Repository → Actions → `Build BurmeseRecapAi APK` → `Run workflow` ကိုနှိပ်ပါ။
5. Build ပြီးလျှင် workflow run ထဲက Artifacts မှ `BurmeseRecapAi-debug-apk` ကို Download လုပ်ပြီး ZIP ဖြည်ပါ။

မှတ်ချက်: APK build အောင်မြင်ဖို့ `API_BASE_URL` ကို backend ရဲ့ HTTPS URL အဖြစ် `app/build.gradle.kts` ထဲမှာ အရင်ပြောင်းထားရပါမယ်။ Backend ကိုလည်း သီးခြား host လုပ်ပြီး `.env` မှာ API key ထည့်ရပါမယ်။ ဒီ source ZIP က backend ကို အလိုအလျောက် host မလုပ်ပေးပါ။
