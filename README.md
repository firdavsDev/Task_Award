![image](https://github.com/firdavsDev/Task_Award/assets/74819987/ff73891e-bd94-4b09-8103-5f17ef56edd9)

## [2, v] Oraliqdagi tub sonlar sonini hisoblash uchun veb-service yaratish. (v > 2)

### Xizmat 2 endpoint'dan foydalanishi kerak:

1) PUT /number?v=....
      * [2, v] oraliqdagi tub sonlar sonini hisoblashni so'rash, misol:
      * curl -XPUT http://127.0.0.1:5000/number?v=10
      * Response: {}, 200 (status code)
      * Agar v parametri bo'lmasa - {} + status 400 (bad request)

2) GET /number
      * curl http://127.0.0.1:5000/number => {“v”: 10, “count”: 4}
      * curl http://127.0.0.1:5000/number => пустое тело + статус 404 (not found)
      * GET so'rovlari uchun vaqt tugashi argumentini belgilashga imkon bering: <br>
         - `curl http://127.0.0.1:5000/number?timeout=N`
         - agar queue'da tayyor natija bo'lmasa, clint keyingi natija hisoblanmaguncha yoki kutish muddati tugaguncha kutishi kerak (N - soniyalar soni). Agar natija ko'rinmasa, 404 kodini va bo'sh json {} qaytaring.
       
- Clint natijalarni tartiblangan holda olishlari kerak:
- Agar ikkita clint natijani kutayotgan bo'lsa (taymout'dan foydalangan holda), natijani queue'dagi  birinchi so'ragan clint olishi kerak.
- Service hech qanday ma'lumotni saqlab qolmaslig kerak bo'ladi, barcha process'lar (hisoblashlar va natijalar uchun so'rovlar) faqat xotirada saqlanadi. (MemoryError)
- Service kodi asinxron bo'lishi kerak. Asinxron kodni tashkil qilish uchun faqat aiohttp-dan foydalanishga ruxsat beriladi.
- Hisoblash natijalari yoziladigan Queue <b>asyncio</b> kutubxonasi asosida mustaqil ravishda yozilish zarur.
- Oddiy raqamlar sonini hisoblash uchun og'ir operatsiyalarni qanday bajarish kerakligini o'ylab ko'ring, xizmatning event loop'ni bloklanmasligi kerak (service  yangi surovlarni odatdagidek qabul qilishi kerak);
- Iloji boricha tushunarli clean code yozishga harakat qiling va yagona .py saqlashga harakat qiling.

Omad ;)
