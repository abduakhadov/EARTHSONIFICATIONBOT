# The Earth Information Jukebox
**Yer haqidagi ma'lumotlar jukeboksi** — NASA Space Apps Challenge

Yer haqidagi raqamlarni (harorat, dengiz sathi, CO₂ va boshqalar) kuyga aylantiruvchi veb-sayt. Qiymat qancha baland bo'lsa, nota ham shuncha baland. Foydalanuvchi trekni tanlaydi, ▶ tugmasini bosadi va sayyoramiz qanday o'zgarayotganini eshitadi.

## Fayllar

| Fayl | Vazifasi |
|---|---|
| `index.html` | Butun sayt (HTML + CSS + JS bitta faylda) |
| `README.md` | Shu qo'llanma |

## Ishga tushirish

1. `index.html` ni brauzerda oching. Server shart emas.
2. Ovoz chiqishi uchun sahifada birinchi marta ▶ tugmasini bosing (brauzerlar ovozni faqat bosishdan keyin ruxsat beradi).
3. Internetga qo'yish uchun: GitHub Pages, Netlify yoki Vercel ga `index.html` ni yuklang.

## Treklar

Harorat, dengiz sathi, CO₂, muzliklar, o'rmonlar, bo'ronlar, havo sifati, Quyosh faolligi, okean kislotaliligi, bioxilma-xillik, tungi chiroqlar.

- **Ikki trek birga:** yuqoridagi katakchani yoqing, so'ng ikkita trekni tanlang. Masalan, harorat (pianino) + CO₂ (baraban).
- **Xavf signali:** ko'rsatkich kritik darajaga yetganda past ogohlantiruvchi tovush qo'shiladi.

## Haqiqiy NASA ma'lumotlarini ulash

Hozir saytda taxminiy tayanch nuqtalar bor. Fayl ichida `const T=[...]` ro'yxatini toping. Har bir trekda `pts:[[yil, qiymat], ...]` bor. Shu qiymatlarni haqiqiy ma'lumot bilan almashtiring. Oraliq yillar avtomatik to'ldiriladi.

Manbalar:

- Harorat: NASA GISTEMP (data.giss.nasa.gov/gistemp)
- Dengiz sathi: NASA Sea Level Change (sealevel.nasa.gov)
- CO₂: NOAA Mauna Loa (gml.noaa.gov/ccgg/trends)
- Arktika muzi: NSIDC (nsidc.org)
- Quyosh dog'lari: SILSO (sidc.be/silso)
- Tirik sayyora indeksi: WWF Living Planet Index
- O'rmonlar: FAO Global Forest Resources Assessment

## Telegram bot

Sayt tepasida va chat oynasida **@EarthsonificationBOT** (https://t.me/EarthsonificationBOT) ga o'tish tugmasi bor. Havolani o'zgartirish uchun `index.html` da `t.me/EarthsonificationBOT` ni qidiring.

## Bepul AI (Gemini kaliti)

1. aistudio.google.com/apikey dan bepul kalit oling (billing ulamang).
2. `index.html` da `const GEMINI_KEY="";` qatoriga kalitni qo'ying.
3. Saytni Netlify / GitHub Pages ga yuklang.
4. Google Cloud Console da kalitni sayt manzilingiz (HTTP referrer) bilan cheklang.

Kalit brauzerda ko'rinadi, shuning uchun faqat bepul kalit ishlating va ochiq repozitoriyga yuklamang.

## AI tugmasi va botni ulash

Saytning pastki o'ng burchagida **🤖 AI bilan gaplashish** tugmasi bor. U chat oynasini ochadi.

- `BOT_URL` bo'sh bo'lsa, tugma Claude ichida ochilganda Claude'ning o'zi javob beradi (hosting qilingan sahifada ishlamaydi).
- Saytni o'z hostingingizga qo'ysangiz, o'zingizning botingizni ulang. Botni o'zingiz yaratasiz, keyin quyidagicha ulaysiz.

### 1-qadam: manzilni kiriting

`index.html` da kod boshidagi qatorni toping:

```js
const BOT_URL="";
```

Va botingiz manzilini yozing:

```js
const BOT_URL="https://sizning-botingiz.example.com/chat";
```

Manzil bo'sh qolsa, panel "Bot hali ulanmagan" deb javob beradi.

### 2-qadam: botingiz shu formatni qabul qilsin

Sayt botga **POST** so'rov yuboradi (`Content-Type: application/json`):

```json
{
  "message": "Nega harorat oshyapti?",
  "track": "temp",
  "trackName": "Global harorat",
  "year": 2016,
  "value": 1.01,
  "unit": "°C"
}
```

`track`, `year` va `value` foydalanuvchi hozir eshitayotgan trek va yilni bildiradi. Botingiz javobni shunday qaytarsin:

```json
{ "reply": "Asosiy sabab: issiqxona gazlari ko'payishi..." }
```

Sayt faqat `reply` maydonini ko'rsatadi.

### 3-qadam: CORS ni yoqing

Bot boshqa manzilda turgani uchun serveringiz saytingiz manzilidan so'rovga ruxsat berishi kerak. Javob sarlavhalariga qo'shing:

```
Access-Control-Allow-Origin: https://sizning-saytingiz.example.com
Access-Control-Allow-Methods: POST, OPTIONS
Access-Control-Allow-Headers: Content-Type
```

Sinash uchun vaqtincha `*` qo'yish mumkin, lekin tayyor loyihada aniq manzilni yozing.

### Tekshirish

Saytni oching, botga savol yozing va "Yuborish" ni bosing. Agar "Botga ulanib bo'lmadi" chiqsa:

1. `BOT_URL` to'g'ri yozilganini tekshiring.
2. Brauzer konsolida (F12) CORS xatosi bormi, qarang.
3. Bot manzili `https://` bilan boshlanishi kerak (sayt `https` da bo'lsa).

> API kalitini (masalan, Claude yoki boshqa AI kaliti) `index.html` ichiga **yozmang**. Kalit faqat bot serveringizda saqlansin.

## Litsenziya va manbalar

Ma'lumotlar NASA, NOAA, FAO, WWF va boshqa ochiq manbalardan. Loyiha NASA Space Apps Challenge uchun yaratilgan.
