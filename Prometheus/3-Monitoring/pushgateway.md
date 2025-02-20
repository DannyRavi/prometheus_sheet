https://prometheus.github.io/client_python/exporting/pushgateway/
https://github.com/prometheus/pushgateway?tab=readme-ov-file

در سیستم **Prometheus**، به طور معمول، **Pull-based** یا مدل pull برای جمع‌آوری داده‌ها استفاده می‌شود. در این مدل، Prometheus داده‌ها را مستقیماً از سرویس‌ها یا اپلیکیشن‌های مانیتورینگ شده می‌گیرد. اما در برخی موارد خاص، این مدل مناسب نیست. اینجاست که **Pushgateway** وارد عمل می‌شود.

---

### **‏Pushgateway چیست؟**
‏**Pushgateway** یک ابزار است که به برنامه‌ها یا سرویس‌ها اجازه می‌دهد **متریک‌های خود را به صورت Push** ارسال کنند (به جای اینکه Prometheus آنها را Pull کند). Pushgateway مانند یک واسط عمل می‌کند که متریک‌ها را از سرویس‌ها دریافت کرده و آنها را در یک **Endpoint** ذخیره می‌کند تا Prometheus بتواند این داده‌ها را از آنجا جمع‌آوری کند.



----
## Non-goals

اول از همه، Pushgateway قادر نیست Prometheus را به یک سیستم مانیتورینگ مبتنی بر push تبدیل کند. برای توضیحات کلی در مورد موارد استفاده از Pushgateway، لطفاً بخش "زمان استفاده از Pushgateway" را مطالعه کنید.

‏Pushgateway به صراحت یک _aggregator_ یا _counter_ توزیع‌شده نیست، بلکه یک حافظه موقت (کش) برای متریک‌ها است. این سرویس دارای  مشابهتی مثل [statsd](https://github.com/etsy/statsd) نیست. متریک‌هایی که به Pushgateway ارسال می‌شوند دقیقاً همان‌هایی هستند که شما در یک برنامه دائماً در حال اجرا برای scrape کردن ارائه می‌دهید. اگر به شمارنده توزیع‌شده نیاز دارید، می‌توانید از statsd واقعی در ترکیب با[ Prometheus statsd exporter](https://github.com/prometheus/statsd_exporter) استفاده کنید یا به prom-aggregation-gateway نگاهی بیندازید. با کسب تجربه بیشتر، پروژه Prometheus ممکن است روزی بتواند یک راه‌حل بومی ارائه دهد، جدا از Pushgateway یا حتی به عنوان بخشی از آن.

برای متریک‌های سطح ماشین، معمولاً textfile collector مربوط به Node Exporter مناسب‌تر است. Pushgateway برای متریک‌های سطح سرویس طراحی شده است.

‏Pushgateway یک ذخیره‌کننده رویداد (event store) نیست. در حالی که می‌توانید از Prometheus به عنوان منبع داده برای [Grafana annotations](http://docs.grafana.org/reference/annotations/) استفاده کنید، ردیابی چیزی مانند رویدادهای انتشار (release events) باید با استفاده از یک چارچوب ثبت رویداد (event-logging framework) انجام شود.



---

### **کاربردهای اصلی Pushgateway**
1. **مانیتورینگ سرویس‌های کوتاه‌عمر (Short-lived Services):**  
   برخی از سرویس‌ها مانند **Job‌های Batch**، اسکریپت‌های خط فرمان یا وظایف زمان‌بندی‌شده (Cron Jobs) ممکن است کوتاه‌عمر باشند و قبل از اینکه Prometheus بتواند داده‌های آنها را Pull کند، از بین بروند.  
   - ‏Pushgateway این متریک‌ها را قبل از پایان یافتن سرویس ذخیره می‌کند تا Prometheus بتواند آنها را بخواند.

   **مثال:**
   ```bash
   echo "my_batch_job_duration_seconds 123" | curl --data-binary @- http://localhost:9091/metrics/job/my_batch_job
   ```

2. ‏**Push کردن متریک‌ها از محیط‌های محدود:**  
   در برخی موارد، یک برنامه یا سرویس ممکن است در محیطی اجرا شود که Prometheus نمی‌تواند به آن دسترسی داشته باشد (مثل محیط‌های **NAT**، فایروال، یا شبکه‌های داخلی). در این موارد، Pushgateway می‌تواند به عنوان یک واسطه عمل کند.

3. **جمع‌آوری داده از سیستم‌های خارجی:**  
   برای جمع‌آوری داده از سیستم‌هایی که به صورت بومی از مدل **Pull** Prometheus پشتیبانی نمی‌کنند (مثل برخی دستگاه‌های IoT یا APIهای خارجی)، Pushgateway امکان Push داده‌ها را فراهم می‌کند.

---

### **چگونه Pushgateway کار می‌کند؟**
1. ‏**Push داده‌ها:**  
   سرویس یا اسکریپت، متریک‌ها را با استفاده از یک درخواست **HTTP POST** یا **PUT** به Pushgateway ارسال می‌کند.
   
2. **ذخیره‌سازی متریک‌ها:**  
   ‏Pushgateway متریک‌ها را در حافظه ذخیره می‌کند و آنها را در فرمت سازگار با Prometheus در **/metrics** نمایش می‌دهد.

3. **جمع‌آوری توسط Prometheus:**  
   ‏Prometheus به صورت دوره‌ای Pushgateway را اسکرپ (Scrape) می‌کند و متریک‌های ذخیره‌شده را جمع‌آوری می‌کند.

---

### **معایب و محدودیت‌ها**
1. **مشکل تمیزکاری متریک‌ها (Metric Cleanup):**  
   متریک‌هایی که به Pushgateway ارسال می‌شوند باید به صورت دستی حذف شوند، در غیر این صورت ممکن است اطلاعات قدیمی و بی‌اعتبار در متریک‌ها باقی بماند.
   
   **راه‌حل:** از **Labels** مناسب و API حذف متریک‌ها استفاده کنید.

2. **عدم تناسب برای متریک‌های Real-Time:**  
   ‏Pushgateway برای متریک‌های لحظه‌ای و real-time طراحی نشده است. برای این نوع متریک‌ها بهتر است از مدل Pull استفاده شود.

3. **اضافه شدن یک لایه واسط:**  
   استفاده از Pushgateway می‌تواند پیچیدگی سیستم را افزایش دهد، به خصوص زمانی که به درستی پیکربندی نشده باشد.

---

### **پیکربندی Pushgateway با Prometheus**
ابتدا Pushgateway را اجرا کنید:
```bash
docker run -d -p 9091:9091 prom/pushgateway
```

سپس در فایل پیکربندی Prometheus (معمولاً `prometheus.yml`) Pushgateway را به عنوان یک Target اضافه کنید:
```yaml
scrape_configs:
  - job_name: 'pushgateway'
    static_configs:
      - targets: ['localhost:9091']
```

پس از این تنظیمات، Prometheus می‌تواند متریک‌ها را از Pushgateway جمع‌آوری کند.

---

### **جمع‌بندی**
‏**Pushgateway** برای سناریوهایی مفید است که مدل Pull استاندارد Prometheus کافی نیست، به ویژه برای جمع‌آوری متریک‌های سرویس‌های کوتاه‌عمر و محیط‌های محدود. با این حال، باید با دقت استفاده شود تا مشکلاتی مانند متریک‌های قدیمی یا افزایش پیچیدگی سیستم رخ ندهد.

 در واقع**Pushgateway** یک سرویس واسطه است که به شما اجازه می‌دهد متریک‌ها را از jobهایی که نمی‌توان آن‌ها را اسکرپ کرد، ارسال کنید. برای جزئیات بیشتر، به بخش **Pushing metrics** مراجعه کنید.

---

### **آیا باید از Pushgateway استفاده کنم؟**

ما تنها در موارد خاص و محدود استفاده از Pushgateway را توصیه می‌کنیم. استفاده از Pushgateway به جای مدل کشش (pull model) معمول Prometheus برای جمع‌آوری متریک‌ها می‌تواند مشکلاتی ایجاد کند:

1. **نقطه شکست واحد و گلوگاه:**  
   هنگام مانیتور کردن چندین نمونه از طریق یک Pushgateway، Pushgateway به یک نقطه شکست واحد و گلوگاه  تبدیل می‌شود.

2. **عدم مانیتورینگ خودکار وضعیت نمونه‌ها:**  
   شما مانیتورینگ خودکار وضعیت instance‌ها از طریق متریک **up** (که در هر اسکرپ تولید می‌شود) را از دست می‌دهید.

3. **ذخیره دائمی متریک‌ها در Pushgateway:**  
  یک Pushgateway هیچگاه سری‌های ارسال‌شده به خود را فراموش نمی‌کند و آن‌ها را برای همیشه به Prometheus نمایش می‌دهد مگر اینکه آن سری‌ها به صورت دستی از طریق API Pushgateway حذف شوند.

4. **مشکل با تغییرات نام یا حذف instance‌ها:**  
   این موضوع به ویژه زمانی مهم است که چندین instance از یک job، متریک‌های خود را در Pushgateway از طریق لیبل **instance** یا مشابه آن تفکیک می‌کنند. متریک‌های مربوط به یک instance سپس در Pushgateway باقی خواهند ماند حتی اگر نمونه اصلی تغییر نام داده یا حذف شود. دلیل این موضوع این است که چرخه عمر Pushgateway به عنوان یک pull متریک کاملاً جدا از چرخه عمر فرآیندهایی است که متریک‌ها را به آن ارسال می‌کنند. در مقایسه با مدل معمول pull Prometheus: وقتی یک instance ناپدید می‌شود (چه عمداً و چه نه)، متریک‌های آن به طور خودکار با آن ناپدید می‌شوند. اما در زمان استفاده از Pushgateway، اینطور نیست و شما باید متریک‌های قدیمی را به صورت دستی حذف کرده یا این هماهنگی چرخه زندگی را به طور خودکار انجام دهید.

---

### **مورد کاربرد معتبر Pushgateway**
معمولاً تنها مورد کاربرد معتبر برای Pushgateway، ثبت نتیجه یک job دسته‌ای (batch job) در سطح سرویس است. یک job دسته‌ای در سطح سرویس، به معنای jobی است که به طور معنایی به یک ماشین یا نمونه خاص مربوط نمی‌شود (برای مثال، یک job دسته‌ای که تعداد زیادی کاربر را از یک سرویس حذف می‌کند). متریک‌های چنین jobهایی نباید شامل لیبل ماشین یا instance باشند تا چرخه عمر ماشین‌ها یا نمونه‌های خاص از متریک‌های ارسال‌شده تفکیک شود. این کار بار مدیریت متریک‌های قدیمی در Pushgateway را کاهش می‌دهد. برای بهترین شیوه‌های مانیتورینگ jobهای دسته‌ای، به مستندات مراجعه کنید.

---

### **استراتژی‌های جایگزین**
1. **انتقال سرور Prometheus پشت فایروال یا NAT:**
   اگر یک فایروال ورودی یا NAT مانع از pull شدن متریک‌ها از اهداف می‌شود، پیشنهاد می‌کنیم سرور Prometheus را نیز پشت همان مانع شبکه قرار دهید. به طور کلی، توصیه می‌شود که سرورهای Prometheus در همان شبکه‌ای که نمونه‌های مانیتور شده قرار دارند، اجرا شوند.

2. **استفاده از PushProx:**
   در غیر این صورت، می‌توانید از **PushProx** استفاده کنید که به Prometheus این امکان را می‌دهد که از یک فایروال یا NAT عبور کند.
https://github.com/prometheus-community/PushProx

3. **استفاده از Node Exporter برای jobهای مربوط به ماشین:**
   برای jobهای دسته‌ای که به یک ماشین مرتبط هستند (مانند cronjobهای به‌روزرسانی امنیتی خودکار یا اجرای کلاینت‌های مدیریت پیکربندی)، متریک‌های حاصل را از طریق **textfile collector** در **Node Exporter** به جای Pushgateway منتشر کنید.

---
سرور **Prometheus** به هر متریکی که اسکرپ می‌کند، دو لیبل **job** و **instance** اضافه می‌کند. مقدار لیبل **job** از تنظیمات اسکرپ (scrape configuration) گرفته می‌شود. وقتی Pushgateway را به عنوان یک هدف اسکرپ برای سرور Prometheus تنظیم می‌کنید، احتمالاً نامی مانند **pushgateway** را برای job انتخاب می‌کنید. مقدار لیبل **instance** به صورت خودکار به میزبان (host) و پورت هدف اسکرپ شده تنظیم می‌شود. بنابراین، همه متریک‌هایی که از Pushgateway اسکرپ می‌شوند، میزبان و پورت Pushgateway را به عنوان لیبل **instance** و نام job مانند **pushgateway** خواهند داشت.  

هرگونه تداخل با لیبل‌های **job** و **instance** که ممکن است به متریک‌هایی که به Pushgateway ارسال شده‌اند اضافه شده باشد، با تغییر نام آن‌ها به **exported_job** و **exported_instance** حل می‌شود.

---

با این حال، این رفتار معمولاً هنگام اسکرپ کردن Pushgateway مطلوب نیست. به طور کلی، شما می‌خواهید که لیبل‌های **job** و **instance** متریک‌هایی که به Pushgateway ارسال شده‌اند، حفظ شوند. به همین دلیل باید در تنظیمات اسکرپ Pushgateway مقدار **honor_labels: true** را تنظیم کنید. این کار رفتار مورد نظر را فعال می‌کند. برای جزئیات بیشتر به [مستندات]([Pushgateway](https://github.com/prometheus/pushgateway)) مراجعه کنید.


---

حالا به حالتی می‌رسیم که متریک‌های ارسال‌شده به Pushgateway لیبل **instance** ندارند. این حالت معمول است، زیرا متریک‌های ارسال‌شده معمولاً در سطح سرویس هستند و به یک نمونه خاص مربوط نمی‌شوند. حتی با تنظیم **honor_labels: true**، سرور Prometheus یک لیبل **instance** اضافه می‌کند اگر در ابتدا هیچ لیبل **instance** تنظیم نشده باشد. بنابراین، اگر یک متریک بدون لیبل **instance** (و بدون لیبل instance در کلید گروه‌بندی، که در ادامه توضیح داده شده است) به Pushgateway ارسال شود، Pushgateway آن را با یک لیبل **instance** خالی (**{instance=""}**) صادر می‌کند. این معادل عدم وجود لیبل **instance** است، اما از اضافه شدن آن توسط سرور جلوگیری می‌کند.


---

اگر متریک‌ها را در زمان **t1** ارسال کنید، ممکن است تصور کنید که Prometheus آنها را با همان timestamp یعنی **t1** اسکرپ می‌کند. اما در واقع، Prometheus زمانی را به عنوان timestamp متریک‌ها ثبت می‌کند که Pushgateway را اسکرپ می‌کند. چرا اینطور است؟

در دیدگاه Prometheus، یک متریک می‌تواند در هر زمانی اسکرپ شود. متریکی که قابل اسکرپ نباشد، اساساً به عنوان متریکی که دیگر وجود ندارد در نظر گرفته می‌شود. Prometheus تا حدی تحمل‌پذیر است، اما اگر نتواند طی ۵ دقیقه نمونه‌ای از یک متریک دریافت کند، آن متریک را به عنوان متریکی که دیگر وجود ندارد تلقی می‌کند. جلوگیری از این موضوع یکی از دلایل استفاده از Pushgateway است. Pushgateway متریک‌های job‌های کوتاه‌عمر (ephemeral) شما را در هر زمانی قابل اسکرپ می‌کند. اگر زمان ارسال متریک به عنوان timestamp به آن متصل شود، این هدف از بین می‌رود، زیرا ۵ دقیقه پس از آخرین Push، Prometheus متریک شما را به اندازه یک متریک غیرقابل اسکرپ که دیگر وجود ندارد، قدیمی می‌بیند.  
(در Prometheus، تنها یک timestamp برای هر نمونه ذخیره می‌شود و هیچ راهی برای تمایز بین "زمان ارسال" و "زمان اسکرپ" وجود ندارد.)

از آنجایی که هیچ مورد کاربردی وجود ندارد که منطقی باشد یک timestamp متفاوت به متریک‌ها اضافه شود و بسیاری از کاربران به اشتباه تلاش می‌کنند این کار را انجام دهند (با وجود اینکه هیچ کتابخانه کلاینتی از این قابلیت پشتیبانی نمی‌کند)، Pushgateway هر Push‌ای که شامل timestamp باشد را رد می‌کند.

اگر فکر می‌کنید که نیاز به ارسال timestamp دارید، لطفاً بخش **When To Use The Pushgateway** را مطالعه کنید.

---

### **ثبت اطلاعات درباره Push‌های موفق و ناموفق**
برای تسهیل اعلان (Alert) در مورد Push‌های شکست‌خورده یا Push‌هایی که اخیراً انجام نشده‌اند، Pushgateway دو متریک **`push_time_seconds`** و **`push_failure_time_seconds`** را با timestamp یونیکس آخرین Push موفق یا شکست‌خورده (POST/PUT) به هر گروه اضافه می‌کند. این متریک‌ها هر متریک دیگری با همین نام را بازنویسی می‌کنند.  
مقدار صفر برای هر یک از این متریک‌ها به این معناست که آن گروه هرگز یک POST/PUT موفق یا ناموفق نداشته است.

------

اگر چند سری داده با لیبل‌های مشابه به Pushgateway ارسال کنید، **Pushgateway آن‌ها را ذخیره می‌کند** و آن‌ها را **overwrite نمی‌کند**. این بدان معناست که برای هر ترکیب از نام متریک و لیبل‌ها، یک سری داده مجزا ایجاد می‌شود. به عبارت دیگر، اگر چندین مقدار مختلف برای همان نام متریک و لیبل‌های مشابه ارسال شود، هرکدام از آن‌ها به صورت یک سری داده مستقل ذخیره می‌شود.

البته باید توجه داشته باشید که اگر برای یک سری داده همان نام متریک و لیبل‌ها با مقادیر یکسان دوباره ارسال شود، Pushgateway آن را **overwriten** نخواهد کرد و سری داده جدیدی با همان نام و لیبل‌ها اضافه می‌کند.  

در نتیجه، اگر شما بخواهید که مقادیر قبلی را تغییر دهید، باید آن سری داده‌ها را به صورت دستی از طریق API حذف کنید.