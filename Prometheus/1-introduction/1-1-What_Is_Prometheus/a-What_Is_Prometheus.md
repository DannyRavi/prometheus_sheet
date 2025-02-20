![image](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Prometheus_software_logo.svg/220px-Prometheus_software_logo.svg.png)

---
## پرومتئوس چیست؟

**پرومتئوس** یک نرم‌افزار آزاد است که برای monitoring بر رویدادها و alerting استفاده می‌شود. این نرم‌افزار، متریک‌ها را در یک پایگاه داده سری زمانی با ابعاد بالا، با استفاده از مدل HTTP pull و با کوئری‌های انعطاف‌پذیر و alerting بلادرنگ، ثبت می‌کند. این پروژه با زبان Go نوشته شده است و تحت مجوز Apache 2 منتشر شده است، با کد منبع در دسترس در [GitHub](https://en.wikipedia.org/wiki/GitHub "GitHub")، و یک پروژه تایید شده از Cloud Native Computing Foundation (CNCF) همراه با Kubernetes و Envoy است.

---

![[tsdbKind.png]]

---
### تاریخچه
پرومتئوس در سال 2012 در SoundCloud توسعه یافت، زمانی که این شرکت متوجه شد ابزارهای نظارت و متریک‌های موجود (با استفاده از StatsD و Graphite) برای نیازهای آن‌ها کافی نیست. به طور خاص، آن‌ها نیازهایی را شناسایی کردند که پرومتئوس برای برآوردن آن‌ها ساخته شده بود، از جمله یک مدل داده چند بعدی، سادگی عملیاتی، جمع‌آوری داده‌های مقیاس‌پذیر و یک زبان کوئری قدرتمند، همه در یک ابزار واحد. این پروژه از ابتدا متن‌باز بود و شروع به استفاده توسط کاربران Boxever و Docker نیز کرد، علی‌رغم اینکه به طور رسمی اعلام نشده بود.

---
 پرومتئوس از ابزار مانیتورینگ Borgmon استفاده شده در گوگل الهام گرفته شده بود.
تا سال 2013، پرومتئوس برای مانیتورینگ بر تولید در SoundCloud معرفی شد. اعلام عمومی رسمی در ژانویه 2015 انجام شد.
در ماه مه 2016، بنیاد محاسبات ابری Native، پرومتئوس را به عنوان دومین پروژه در حال بررسی شده خود، پس از Kubernetes، پذیرفت. پست وبلاگی که این موضوع را اعلام کرد، بیان می‌کرد که این ابزار در بسیاری از شرکت‌ها از جمله DigitalOcean، Ericsson، CoreOS، Weaveworks، Red Hat و Google در حال استفاده است.

---
#### چرا Prometheus ؟
- **جمع‌آوری داده‌های دقیق و زمان‌بندی شده:** پرومتئوس داده‌ها را به صورت سری‌های زمانی (Time Series) جمع‌آوری می‌کند. این بدان معناست که شما می‌توانید تغییرات عملکرد سیستم را در طول زمان مشاهده کرده و روندها را شناسایی کنید.
- **هشدارهای به‌موقع:** با تعریف آستانه‌های مشخص برای متریک‌های مختلف، پرومتئوس می‌تواند در صورت بروز هرگونه مشکل یا انحراف از حالت نرمال، هشدارهایی را برای شما ارسال کند. این امر به شما امکان می‌دهد تا قبل از وقوع مشکلات جدی، اقدامات لازم را انجام دهید.
- ---
- **انعطاف‌پذیری بالا:** پرومتئوس یک سیستم بسیار انعطاف‌پذیر است و می‌توان آن را برای مانیتورینگ طیف گسترده‌ای از سیستم‌ها و اپلیکیشن‌ها، از جمله زیرساخت‌های ابری، پایگاه‌های داده، سیستم‌های توزیع‌شده و ... پیکربندی کرد.
- **جامعه بزرگ و فعال:** پرومتئوس یک پروژه متن‌باز است و یک جامعه بزرگ از توسعه‌دهندگان و کاربران آن را پشتیبانی می‌کنند. این بدان معناست که شما به راحتی می‌توانید به منابع و اطلاعات مورد نیاز خود دسترسی پیدا کنید.
---
#### چه داده‌هایی را می‌توان با Prometheus مانیتور کرد؟

- **مصرف منابع سیستمی:** CPU، حافظه، دیسک، شبکه و ...
- **عملکرد اپلیکیشن‌ها:** زمان پاسخگویی، تعداد درخواست‌ها، خطاها و ...
- **سلامت سرویس‌ها:** وضعیت سرویس‌ها، زمان آپتایم، زمان داون‌تایم و ...
- **متریک‌های سفارشی:** شما می‌توانید متریک‌های سفارشی خود را تعریف کرده و آن‌ها را مانیتور کنید.
---
 ### چه زمانی از پرومتئوس استفاده کنیم؟
اگر به دنبال یک سیستم مانیتورینگ قدرتمند، انعطاف‌پذیر و متن‌باز هستید، پرومتئوس انتخاب بسیار مناسبی برای شما خواهد بود. پرومتئوس به ویژه برای محیط‌های ابری و میکروسرویس‌ها بسیار مناسب است.
**در کل، پرومتئوس ابزاری است که به شما کمک می‌کند تا از عملکرد صحیح و بهینه سیستم‌های خود اطمینان حاصل کرده و در صورت بروز هرگونه مشکل، به سرعت آن را شناسایی و برطرف کنید.**

---
![[3Observability.png]]

---
#### سری‌های زمانی (Time Series) چیست؟
**سری‌های زمانی** مجموعه‌ای از داده‌ها هستند که در بازه‌های زمانی مشخص جمع‌آوری شده‌اند. به عبارت ساده‌تر، هر داده‌ای که در طول زمان تغییر می‌کند و با یک برچسب زمانی همراه است، یک سری زمانی تشکیل می‌دهد.

---
![[time_series.png]]

---
**مثال‌های سری‌های زمانی:**
- **داده‌های مالی:** قیمت سهام، نرخ ارز، حجم معاملات
- **داده‌های حسگرها:** دما، رطوبت، فشار
- **داده‌های شبکه:** ترافیک شبکه، تعداد درخواست‌ها
- **داده‌های عملکرد سیستم:** مصرف CPU، حافظه، دیسک
- **داده‌های فروش:** میزان فروش محصولات در طول زمان
---
**چرا سری‌های زمانی مهم هستند؟**
- **تشخیص الگوها و روندها:** با تحلیل سری‌های زمانی می‌توان الگوهای تکراری، روندهای صعودی یا نزولی و تغییرات فصلی را شناسایی کرد.
- **پیش‌بینی آینده:** با استفاده از مدل‌های پیش‌بینی، می‌توان بر اساس داده‌های گذشته، مقادیر آینده یک سری زمانی را تخمین زد.
- **آشکارسازی ناهنجاری‌ها:** می‌توان از سری‌های زمانی برای تشخیص رویدادهای غیرعادی و ناهنجاری‌ها استفاده کرد.
- **بهینه‌سازی فرآیندها:** با تحلیل سری‌های زمانی می‌توان فرآیندهای مختلف را بهبود بخشید و عملکرد سیستم‌ها را افزایش داد.
---
**ویژگی‌های کلیدی سری‌های زمانی:**
- **ترتیب زمانی:** داده‌ها به ترتیب زمانی مرتب شده‌اند.
- **برچسب زمانی:** هر داده با یک برچسب زمانی مشخص همراه است.
- **وابستگی:** داده‌های مجاور در زمان معمولاً با هم همبستگی دارند.
- **نویز:** داده‌های سری زمانی ممکن است حاوی نویز و خطا باشند.
---
**کاربردهای سری‌های زمانی در پرومتئوس**
در نرم‌افزار پرومتئوس، سری‌های زمانی برای ذخیره و نمایش داده‌های مانیتورینگ استفاده می‌شوند. هر متریک که توسط پرومتئوس جمع‌آوری می‌شود، در واقع یک سری زمانی است که شامل مقدار متریک و برچسب زمانی آن است. با استفاده از زبان پرس‌وجوی قدرتمند PromQL، می‌توان به راحتی سری‌های زمانی را فیلتر، تجزیه و تحلیل و نمایش داد.

---
## متریک (Metric) چیست؟
**متریک** در دنیای مانیتورینگ و به خصوص در ابزارهایی مانند پرومتئوس، به هر عددی گفته می‌شود که یک جنبه قابل اندازه‌گیری از یک سیستم، اپلیکیشن یا سرویس را نشان می‌دهد. این اعداد می‌توانند هر چیزی از میزان مصرف CPU و حافظه گرفته تا تعداد درخواست‌های HTTP و زمان پاسخگویی یک سرویس را شامل شوند.
**به عبارت ساده‌تر، متریک یک عدد است که به شما می‌گوید یک سیستم در حال حاضر چه کار می‌کند.**

---
#### چرا متریک‌ها مهم هستند؟
- **مانیتورینگ عملکرد:** با استفاده از متریک‌ها می‌توانید عملکرد سیستم خود را به صورت لحظه‌ای و تاریخی زیر نظر داشته باشید.
- **تشخیص مشکلات:** متریک‌ها به شما کمک می‌کنند تا مشکلات و ناهنجاری‌ها را در سیستم خود شناسایی کنید.
- **بهینه‌سازی performance:** با تحلیل متریک‌ها می‌توانید نقاط ضعف سیستم خود را شناسایی کرده و برای بهبود performance آن اقدام کنید.
- **گزارش‌ و لاگ گیری:** می‌توانید از متریک‌ها برای ایجاد گزارش‌ها و لاگ‌های مختلف و تحلیل روندهای تغییرات استفاده کنید.
---
### مثال‌هایی از متریک‌ها:
- **متریک‌های سیستم:** مصرف CPU، میزان حافظه آزاد، فضای دیسک، میزان پهنای باند مصرف شده
- **متریک‌های اپلیکیشن:** تعداد درخواست‌های HTTP، زمان پاسخگویی، تعداد خطاها، میزان حافظه مصرف شده توسط اپلیکیشن
- **متریک‌های کسب‌وکار:** تعداد کاربران فعال، درآمد، میزان تبدیل

---
![[4goldenSignal.png]]

---

### متریک‌ها در پرومتئوس

در پرومتئوس، متریک‌ها به صورت سری‌های زمانی ذخیره می‌شوند. این بدان معنی است که برای هر متریک، یک سری از مقادیر در طول زمان ثبت می‌شود. این ویژگی به شما اجازه می‌دهد تا تغییرات یک متریک را در طول زمان مشاهده کرده و روندهای آن را تحلیل کنید.

---
**ویژگی‌های کلیدی متریک‌ها در پرومتئوس:**
- **نام:** هر متریک یک نام منحصر به فرد دارد که آن را از سایر متریک‌ها متمایز می‌کند.
- ‏**Label‌ها:** Label‌ها به شما اجازه می‌دهند تا متریک‌ها را بر اساس ویژگی‌های مختلف فیلتر و گروه‌بندی کنید.
- **مقدار:** مقدار عددی متریک در یک زمان خاص.
- **زمان:** زمان ثبت مقدار متریک.
---
**مثالی از یک متریک در پرومتئوس:**
```
node_cpu_seconds_total{mode="idle",instance="localhost"} 12345.67
```
در این مثال:
- ‏`node_cpu_seconds_total`: نام متریک است.
-‏ `{mode="idle",instance="localhost"}`: Label‌های این متریک هستند که نشان می‌دهند این داده مربوط به حالت بیکار CPU یک سرور محلی است.
- `12345.67`: مقدار متریک است که نشان می‌دهد CPU در حالت بیکار بوده است.

---
![[sampleTimeSeries.png]]

---
**جمع‌بندی:** متریک‌ها ستون فقرات مانیتورینگ هستند و به شما کمک می‌کنند تا درک عمیقی از سیستم‌های خود به دست آورید. در پرومتئوس، متریک‌ها به همراه Label‌ها و سری‌های زمانی، یک سیستم قدرتمند برای جمع‌آوری، ذخیره و تحلیل داده‌های مانیتورینگ را تشکیل می‌دهند.

---
### انواع داده در پرومتئوس (Prometheus Data Types)
پرومتئوس از چهار نوع داده اصلی برای ذخیره و نمایش متریک‌ها استفاده می‌کند. هر کدام از این نوع‌ها برای نمایش یک نوع خاص از داده طراحی شده‌اند. در ادامه به بررسی هر کدام می‌پردازیم:

https://prometheus.io/docs/concepts/metric_types/


---
### ۱. Counter 
**تعریف:** نوعی متریک است که به صورت مونوتونیک افزایش می‌یابد و هرگز کاهش نمی‌یابد.
**کاربرد:** برای شمارش رویدادهایی مانند تعداد درخواست‌ها، خطاها یا تعداد بایت‌های منتقل شده استفاده می‌شود.
 **مثال:** `http_requests_total` که تعداد کل درخواست‌های HTTP را شمارش می‌کند.
**ویژگی:** برای بازنشانی یک شمارنده، باید سرور یا سرویس مربوطه مجدداً راه‌اندازی شود.
https://prometheus.github.io/client_python/instrumenting/counter/
---
![[counter.png]]

---
### ۲. Gauge 
**تعریف:** متریک‌هایی هستند که می‌توانند افزایش یا کاهش یابند و نشان‌دهنده یک مقدار در یک لحظه خاص هستند.
**کاربرد:** برای نمایش متریک‌هایی مانند استفاده از CPU، حافظه، دمای سیستم و ... استفاده می‌شود.
**مثال:** `cpu_temperature` که دمای CPU را نشان می‌دهد.
http://godoc.org/github.com/prometheus/client_golang/prometheus#Gauge

---

![[gauge.png]]

---
### ۳. Histogram 
**تعریف:** برای اندازه‌گیری توزیع یک مجموعه داده استفاده می‌شود. به طور معمول برای اندازه‌گیری زمان پاسخ، اندازه درخواست‌ها و ... استفاده می‌شود.
**کاربرد:** با استفاده از هیستوگرام می‌توان به اطلاعاتی مانند میانگین، انحراف استاندارد، صدک‌ها و ... دست یافت.
 **مثال:** `http_request_duration_seconds` که زمان پاسخ درخواست‌های HTTP را اندازه‌گیری می‌کند. در واقع یک متریک است که داده‌ها را در بازه‌های از پیش تعریف‌شده (buckets) دسته‌بندی می‌کند و تعداد مواردی که در هر بازه قرار دارند را ثبت می‌کند.
- https://prometheus.github.io/client_python/instrumenting/histogram/

---
![[histogram.png]]

---
- **ویژگی‌ها:**
    - از بازه‌های مشخص (مانند 0.1، 0.5، 1، 5 و ...) استفاده می‌کند.
    - مقدار کل داده‌ها (sum) و تعداد کل داده‌ها (count) را ذخیره می‌کند.
    - توزیع داده‌ها را به صورت **مشخص و گرافیکی** نمایش می‌دهد.
- **مزایا:**
    - امکان رسم گراف‌های درصدی (percentile) بدون نیاز به پردازش اضافی در کلاینت.
    - مناسب برای تحلیل در زمان اجرا (real-time).
    - برای تحلیل در محدوده‌های خاص بسیار مفید است.
- **معایب:**
    - دقت محدود به بازه‌های از پیش تعیین‌شده.
    - افزایش فضای ذخیره‌سازی در صورت تعریف تعداد زیادی بازه.

---
### ۴. Summary 
**تعریف:** مشابه هیستوگرام، یک **Summary** نیز نمونه‌هایی از مشاهدات (معمولاً مواردی مانند مدت زمان درخواست‌ها و اندازه پاسخ‌ها) را جمع‌آوری می‌کند. علاوه بر ارائه تعداد کل مشاهدات و مجموع تمام مقادیر مشاهده‌شده، این متریک quantileهای (صدک) قابل پیکربندی را در یک sliding time window محاسبه می‌کند.
۱. در واقع متریکی است که مستقیماً شاخص‌های آماری مثل درصدهای خاص (quantiles) را محاسبه و ذخیره می‌کند (مانند 50th، 90th، 99th percentile).
https://github.com/prometheus/client_java#summary

---
#### توضیح در مورد Quantile
در آمار، **کوانتایل (Quantile)** به نقطه یا مجموعه‌ای از نقاط در یک توزیع گفته می‌شود که آن را به قسمت‌هایی با اندازه برابر تقسیم می‌کنند. به زبان ساده، کوانتایل‌ها مرزهایی هستند که داده‌ها را به بخش‌های مساوی از نظر تعداد مشاهدات تقسیم می‌کنند.
برای مثال:
- **چارک‌ها (Quartiles)** نوع خاصی از کوانتایل‌ها هستند که داده‌ها را به چهار بخش مساوی تقسیم می‌کنند:
---
- **چارک اول (Q1):** نقطه‌ای که 25٪ داده‌ها کمتر از آن هستند.
- **چارک دوم (Q2):** همان میانه است و نقطه‌ای است که 50٪ داده‌ها کمتر از آن هستند.
- **چارک سوم (Q3):** نقطه‌ای که 75٪ داده‌ها کمتر از آن هستند.
- **دسایل‌ها (Deciles):** کوانتایل‌هایی هستند که داده‌ها را به ۱۰ بخش مساوی تقسیم می‌کنند.
- **پرسنتایل‌ها (Percentiles):** نوع خاصی از کوانتایل‌ها هستند که داده‌ها را به ۱۰۰ بخش مساوی تقسیم می‌کنند. هر پرسنتایل نشان‌دهنده مقداری است که درصد مشخصی از داده‌ها کمتر از آن مقدار قرار دارند. مثلاً **پرسنتایل 90 یا (P90)** عددی است که 90٪ داده‌ها کمتر یا مساوی آن هستند.
---
### نحوه محاسبه کوانتایل
برای پیدا کردن یک کوانتایل خاص (مثلاً صدک ۹۰):
۱. داده‌ها را مرتب کنید.
۲. موقعیت کوانتایل را بر اساس درصد موردنظر محاسبه کنید:
- `موقعیت داده = p×n`  که n تعداد داده‌ها و p درصد کوانتایل به صورت عدد اعشاری (مثلاً 0.9 برای صدک ۹۰) است.
۳. داده‌ای که در موقعیت موردنظر است یا میانگین داده‌های اطراف آن را پیدا کنید.
---
### کاربرد کوانتایل

کوانتایل‌ها در تحلیل داده‌ها و آمار برای:
- توصیف توزیع داده‌ها،
- شناسایی مقادیر پرت (Outliers)،
- دسته‌بندی داده‌ها به گروه‌های مختلف استفاده می‌شوند.
---
یک Summary با نام متریک پایه `<basename>`، چندین سری زمانی را در هنگام جمع‌آوری داده‌ها (scrape) ارائه می‌دهد:

1. **کوانتایل‌های استریمی (streaming φ-quantiles)** برای رخدادهای مشاهده‌شده، که به صورت `<basename>{quantile="<φ>"}` نمایش داده می‌شوند، جایی که.
   0≤φ≤1
2. **مجموع کل مقادیر مشاهده‌شده** که به صورت `<basename>_sum` ارائه می‌شود.
3. **تعداد رخدادهایی که مشاهده شده‌اند** که به صورت `<basename>_count` نمایش داده می‌شود.
---
![[SUMMARIES.png]]

---

۲. **ویژگی‌ها:**
    - محاسبه دقیق درصدها توسط کلاینت (Application) انجام می‌شود و Prometheus فقط مقادیر محاسبه‌شده را ذخیره می‌کند.
    - شامل **sum** و **count** نیز هست، اما مستقیماً درصدهای مشخص‌شده را ارائه می‌دهد.
۳. **مزایا:**
    - ارائه درصدهای دقیق در همان لحظه.
    - مناسب برای زمانی که به درصدهای خاص علاقه‌مند هستید.
۴. **معایب:**
    - تجمیع (aggregation) درصدها در Prometheus بین چندین نمونه یا سرویس ممکن نیست.
    - نیازمند محاسبه درصدها در کلاینت، که ممکن است پیچیدگی اضافه ایجاد کند.

---

### **تفاوت‌های اصلی Histogram و Summaries در Prometheus:**

| **ویژگی**                                | **Histogram **                                                                                                                | **Summary **                                                                                                              |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **پیکربندی مورد نیاز**                   | انتخاب سطل‌هایی (buckets) که برای بازه مورد انتظار مقادیر مشاهده‌شده مناسب باشند.                                             | انتخاب φ-کوانتایل‌های دلخواه و پنجره زمانی لغزان (sliding window). کوانتایل‌ها و پنجره‌های دیگر بعداً قابل محاسبه نیستند. |
| **عملکرد کلاینت**                        | ثبت مشاهدات بسیار ارزان است، زیرا فقط نیاز به افزایش شمارنده‌ها دارند.                                                        | ثبت مشاهدات پرهزینه است به دلیل محاسبه کوانتایل‌های استریمی.                                                              |
| **عملکرد سرور**                          | سرور باید کوانتایل‌ها را محاسبه کند. در صورت طولانی شدن محاسبات (مثلاً در یک داشبورد بزرگ)، می‌توان از قواعد ضبط استفاده کرد. | هزینه کم در سمت سرور.                                                                                                     |
| **تعداد سری‌های زمانی**                  | یک سری زمانی برای هر پیمانه پیکربندی‌شده (علاوه بر سری‌های _sum و _count).                                                    | یک سری زمانی برای هر کوانتایل پیکربندی‌شده.                                                                               |
| **خطای کوانتایل**                        | خطا در بعد مقادیر مشاهده‌شده به وسیله عرض پیمانه مربوطه محدود می‌شود.                                                         | خطا در بعد φ توسط یک مقدار قابل پیکربندی محدود می‌شود.                                                                    |
| **تعیین φ-کوانتایل و پنجره زمانی لغزان** | به صورت آنی با عبارات Prometheus.                                                                                             | به صورت پیش‌فرض توسط کلاینت پیکربندی می‌شود.                                                                              |

---
### مثال در PromQL:

فرض کنید متریکی با نام `http_request_duration_seconds` داریم.
	`rate(http_request_duration_seconds_bucket[5m])`
این کوئری تعداد درخواست‌ها در بازه‌های زمانی مختلف را بررسی می‌کند.
	`rate(http_request_duration_seconds{quantile="0.99"}[5m])`
این کوئری مستقیماً مقدار 99th percentile را نمایش می‌دهد.
**نتیجه‌گیری**: اگر نیازمند دقت بالا برای درصدهای خاص هستید، از **Summaries** استفاده کنید. اما اگر می‌خواهید تجزیه و تحلیل توزیع کلی داده‌ها را انجام دهید و قابلیت تجمیع داده‌ها اهمیت دارد، **Histogram** گزینه بهتری است.

---
**انتخاب نوع داده مناسب:**
- ‏**Counter:** برای شمارش رویدادهای غیرقابل برگشت
- ‏**Gauge:** برای اندازه‌گیری مقادیر متغیر در زمان
- ‏**Histogram:** برای اندازه‌گیری توزیع داده‌ها
- ‏**Summary:** برای محاسبه دقیق موارد آمار‌ی

---
#### ‏Label (Label) در Prometheus: کلیدی برای سازماندهی و فیلتر کردن داده‌ها
در  پرومتئوس، **Label**  یک عنصر بسیار مهم است که به شما کمک می‌کند تا داده‌های متریک را سازماندهی، فیلتر و تجزیه و تحلیل کنید. به عبارت ساده‌تر، Label‌ها مانند تگ‌هایی هستند که به هر داده متریک اختصاص داده می‌شوند و اطلاعات اضافی درباره آن داده را ارائه می‌دهند.

---
### چرا Label‌ها مهم هستند؟
- **سازماندهی داده‌ها:** با استفاده از Label‌ها می‌توانید داده‌های متریک را بر اساس ویژگی‌های مختلف مانند محیط (production، staging)، سرویس، سرور، منطقه و ... گروه‌بندی کنید.
- **فیلتر کردن داده‌ها:** می‌توانید با استفاده از عبارات کوئری PromQL، داده‌های متریک را بر اساس Label‌های خاص فیلتر کنید.
- **ایجاد داشبوردهای سفارشی:** Label‌ها به شما امکان می‌دهند تا داشبوردهای گرافیکی را به گونه‌ای طراحی کنید که اطلاعات مورد نیاز شما را به صورت دقیق و خلاصه نشان دهند.

---
### ساختار یک Label

یک Label از دو بخش تشکیل شده است:
- **نام Label:** یک رشته متنی منحصر به فرد که نوع اطلاعات را مشخص می‌کند (مثلاً: environment، instance، job).
- **مقدار Label:** یک رشته متنی که مقدار خاص آن Label را برای یک داده متریک مشخص می‌کند (مثلاً: production، localhost، node_exporter).

---
**مثال:**
```
node_cpu_seconds_total{mode="idle",instance="localhost"} 12345.67
```
در این مثال:
- ‏`node_cpu_seconds_total`: نام متریک است.
- ‏`{mode="idle",instance="localhost"}`: مجموعه Label‌های این متریک است.
- ‏`mode="idle"`: یک Labelی است که نشان می‌دهد این داده مربوط به حالت بیکار CPU است.
- ‏`instance="localhost"`: یک Labelی است که نشان می‌دهد این داده از سرور local جمع‌آوری شده است.
---
### کاربردهای Label‌ها

- **ایجاد سلسله مراتب:** با استفاده از چندین Label، می‌توانید سلسله مراتب‌های پیچیده‌ای برای سازماندهی داده‌های خود ایجاد کنید.
- **تخصیص منابع:** می‌توانید از Label‌ها برای تخصیص منابع به بخش‌های مختلف سیستم استفاده کنید.
- **تحلیل عملکرد:** می‌توانید با استفاده از Label‌ها، عملکرد بخش‌های مختلف سیستم را با هم مقایسه کنید.
- **ایجاد هشدارهای سفارشی:** می‌توانید هشدارهایی را بر اساس مقادیر خاصی از Label‌ها ایجاد کنید.

---

### مثال‌های دیگر از Label‌ها:

- ‏`job="nginx"`: برای شناسایی متریک‌های مربوط به وب سرور Nginx
- ‏`environment="production"`: برای شناسایی متریک‌های مربوط به محیط تولید
- ‏`datacenter="eu-central-1"`: برای شناسایی متریک‌های مربوط به یک دیتاسنتر خاص
---
### JOBS و INSTANCES

در اصطلاح Prometheus، برای endpointهایی که می توانید آن را scrape کنید، یک instance نامیده می‌شود که معمولاً مربوط به یک فرآیند واحد است. مجموعه‌ای از نمونه ها با همان هدف، فرآیندی که برای مقیاس پذیری یا قابلیت اطمینان تکرار می شود، شغل نامیده می شود. به عنوان مثال، یک کار سرور API با چهار نمونه تکرار شده:
- job: `api-server`
    - instance 1: `1.2.3.4:5670`
    - instance 2: `1.2.3.4:5671`
    - instance 3: `5.6.7.8:5670`
    - instance 4: `5.6.7.8:5671`

---
### جمع‌بندی Label‌ها
‏Label‌ها در پرومتئوس ابزاری قدرتمند برای سازماندهی، فیلتر کردن و تجزیه و تحلیل داده‌های متریک هستند. با استفاده صحیح از Label‌ها، می‌توانید به بینش‌های عمیقی درباره عملکرد سیستم خود دست پیدا کنید و مشکلات را به سرعت شناسایی و برطرف کنید.
- ‏**PromQL:** زبان پرس‌و‌جوی قدرتمندی که برای کار با Label‌ها استفاده می‌شود.
- **داشبوردهای Grafana:** نحوه استفاده از Label‌ها برای ایجاد داشبوردهای سفارشی در Grafana.
- **بهترین روش‌ها برای استفاده از Label‌ها:** توصیه‌هایی برای استفاده موثر از Label‌ها در محیط‌های تولید.

--------
### reference

youtube:
https://virgool.io/@naeemaei/ماینیتوریگ-web-api-با-prometheus-و-grafana-بخش-1-alebzphseodn
https://www.youtube.com/watch?v=vY61h6cSkVA&list=PLrMP04WSdCjrL4OBnaqXRy8X3XEd7ZrKf&index=1
https://www.youtube.com/watch?v=JQrk6HwlN78&list=PL6VBQyIvTlRhoCvodpzjQK9oRVvcviHdA
https://www.youtube.com/watch?v=dk2-_DbWb80&list=PLVx1qovxj-anCTn6um3BDsoHnIr0O2tz3

article:
https://prometheus.io/docs/introduction/overview/
https://virgool.io/@rafiee/در-مسیر-observability-استک-پرومتئوس-قسمت-چهارم-obclldvrwtgp
https://virgool.io/@rafiee/در-مسیر-observability-استک-پرومتئوس-قسمت-پنجم-nktvhhhvye00
https://virgool.io/@ali.fattahi/مانیتورینگ-و-تشخیص-ناهنجاری-anomaly-در-داده-ها-با-استفاده-از-grafanaprometheus-yemhl8ps3fij
https://virgool.io/@pourya.salahi76/monitoring-tools-such-as-prometheus-wjfu6et1vcq0
https://virgool.io/@naeemaei/ماینیتوریگ-web-api-با-prometheus-و-grafana-بخش-1-alebzphseodn

