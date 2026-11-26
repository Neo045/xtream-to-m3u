# GitHub → Vercel Deployment (বাংলা)

এই ZIP-টি GitHub-এ সরাসরি Project Root হিসেবে আপলোড করার জন্য প্রস্তুত করা হয়েছে। ZIP extract করার পর `xtream2m3u-main` ফোল্ডারের **ভেতরের সব ফাইল** repository root-এ রাখবে। ফোল্ডারটিকে আরেকটি nested folder হিসেবে আপলোড করবে না।

## GitHub
1. https://github.com/new খুলে নতুন repository তৈরি করো।
2. ZIP extract করো।
3. `README.md`, `index.py`, `vercel.json`, `requirements.txt`, `app/`, `frontend/` ইত্যাদি সব ফাইল ও folder repository root-এ upload করো।
4. `.python-version` ফাইলটিও upload হয়েছে নিশ্চিত করো।

## Vercel
1. https://vercel.com/new খুলে GitHub repository Import করো।
2. Root Directory `./` রাখো।
3. Framework Preset `Other` বা Flask auto-detection হলে Flask রাখো।
4. Build Command এবং Output Directory override কোরো না; ফাঁকা/default রাখো।
5. Deploy চাপো।

Vercel Flask app-কে `index.py`-এর top-level `app` WSGI object থেকে detect করবে। `requirements.txt` থেকে Python dependencies install হবে। Fluid Compute-এ function duration সর্বোচ্চ 300 seconds পর্যন্ত কনফিগার করা আছে।

## Deploy-এর পর পরীক্ষা
- প্রথমে মূল URL খুলে Frontend load হচ্ছে কি না দেখো।
- এরপর নিজের বৈধ Xtream credentials দিয়ে Category Load ও ছোট M3U export পরীক্ষা করো।
- Vercel-এর Function Logs-এ কোনো import/build/runtime error আছে কি না দেখো।

## সীমাবদ্ধতা
- Vercel serverless; দীর্ঘক্ষণ চলা Live Stream Proxy, বড় playlist, বা দীর্ঘ API request function duration / platform limits-এ আটকে যেতে পারে।
- `maxDuration: 300` Fluid Compute-এর 5 মিনিটের সীমা; এটি অনির্দিষ্ট সময়ের কাজ চালানোর নিশ্চয়তা নয়।
- কোনো credentials ZIP-এ রাখা হয়নি। Vercel environment variables প্রয়োজন হলে Project Settings → Environment Variables থেকে যোগ করতে হবে।

## Local test (ঐচ্ছিক)
Python 3.12 ইনস্টল করে:

```bash
pip install -r requirements.txt
python run.py
```

তারপর `http://127.0.0.1:5000` খুলবে। Vercel-এর কাছাকাছি local test করতে Vercel CLI-এর `vercel dev` ব্যবহার করা যায়।
