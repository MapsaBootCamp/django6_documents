# الگوی iterator
##### Iterator یک الگوی طراحی رفتاری است که به شما امکان می دهد عناصر یک مجموعه را بدون افشای نمایش زیرین آن (فهرست، پشته، درخت و غیره) طی کنید.

## مشکل
##### مجموعه ها یکی از پرکاربردترین انواع داده در برنامه نویسی هستند. با این وجود، یک مجموعه فقط یک ظرف برای گروهی از اشیاء است.


![انواع مجموعه ها.](https://refactoring.guru/images/patterns/diagrams/iterator/problem1.png)


اکثر مجموعه ها عناصر خود را در لیست های ساده ذخیره می کنند. با این حال، برخی از آنها بر اساس پشته ها، درختان، نمودارها و دیگر ساختارهای داده پیچیده هستند.

اما مهم نیست که یک مجموعه چگونه ساختار یافته است، باید راهی برای دسترسی به عناصر خود ارائه دهد تا سایر کدها بتوانند از این عناصر استفاده کنند. باید راهی برای عبور از هر عنصر مجموعه بدون دسترسی مکرر به عناصر مشابه وجود داشته باشد.

اگر مجموعه ای بر اساس فهرست دارید، ممکن است کار آسانی به نظر برسد. شما فقط روی همه عناصر حلقه بزنید. اما چگونه می‌توان عناصر یک ساختار داده پیچیده، مانند درخت را به‌طور متوالی طی کرد؟ برای مثال، یک روز ممکن است با اولین پیمایش در عمق یک درخت خوب باشید. با این حال روز بعد ممکن است نیاز به پیمایش اول داشته باشید. و هفته بعد، ممکن است به چیز دیگری نیاز داشته باشید، مانند دسترسی تصادفی به عناصر درختی.

![یک مجموعه را می توان به چندین روش مختلف طی کرد.](https://refactoring.guru/images/patterns/diagrams/iterator/problem2.png)

افزودن الگوریتم‌های پیمایش بیشتر و بیشتر به مجموعه، به تدریج مسئولیت اصلی آن، که ذخیره‌سازی کارآمد داده‌ها است را محو می‌کند. علاوه بر این، برخی از الگوریتم ها ممکن است برای یک برنامه خاص طراحی شوند، بنابراین گنجاندن آنها در یک کلاس مجموعه عمومی عجیب خواهد بود.

از سوی دیگر، کد کلاینت که قرار است با مجموعه‌های مختلف کار کند، ممکن است حتی به نحوه ذخیره عناصر خود اهمیتی ندهد. با این حال، از آنجایی که مجموعه ها همه راه های مختلفی برای دسترسی به عناصر خود ارائه می دهند، شما هیچ گزینه ای ندارید جز اینکه کد خود را با کلاس های مجموعه خاص ادغام کنید.

## راه حل
ایده اصلی الگوی Iterator این است که رفتار پیمایش یک مجموعه را در یک شی جداگانه به نام تکرار کننده استخراج کند.

![تکرار کننده ها الگوریتم های پیمایش مختلفی را پیاده سازی می کنند. چندین شی تکرار کننده می توانند همزمان از یک مجموعه عبور کنند.](https://refactoring.guru/images/patterns/diagrams/iterator/solution1.png)

علاوه بر پیاده سازی خود الگوریتم، یک شی تکرار کننده تمام جزئیات پیمایش، مانند موقعیت فعلی و تعداد عناصر باقیمانده تا پایان را در خود محصور می کند. به همین دلیل، چندین تکرار کننده می توانند به طور همزمان و مستقل از یکدیگر از یک مجموعه واحد عبور کنند.

معمولاً تکرارکننده‌ها یک روش اصلی را برای واکشی عناصر مجموعه ارائه می‌کنند. کلاینت می تواند این متد را تا زمانی که چیزی برنگرداند ادامه دهد، به این معنی که تکرار کننده تمام عناصر را طی کرده است.

همه تکرار کننده ها باید یک رابط را پیاده سازی کنند. این باعث می شود کد مشتری با هر نوع مجموعه یا هر الگوریتم پیمایش تا زمانی که یک تکرار کننده مناسب وجود داشته باشد سازگار باشد. اگر به روش خاصی برای پیمایش یک مجموعه نیاز دارید، فقط یک کلاس تکرارکننده جدید ایجاد می‌کنید، بدون اینکه نیازی به تغییر مجموعه یا کلاینت باشد.

## آنالوژی دنیای واقعی

![راه های مختلف برای قدم زدن در اطراف رم.](https://refactoring.guru/images/patterns/content/iterator/iterator-comic-1-en.png)

قصد دارید برای چند روز از رم دیدن کنید و از تمام دیدنی ها و جاذبه های اصلی آن دیدن کنید. اما زمانی که به آنجا می رسید، می توانید زمان زیادی را برای راه رفتن در دایره ها تلف کنید، حتی نمی توانید کولوسئوم را پیدا کنید.

از سوی دیگر، می‌توانید یک اپلیکیشن راهنمای مجازی برای گوشی هوشمند خود بخرید و از آن برای پیمایش استفاده کنید. این هوشمند و ارزان است و می توانید تا زمانی که بخواهید در مکان های جالبی بمانید.

گزینه سوم این است که می توانید مقداری از بودجه سفر را خرج کنید و یک راهنمای محلی استخدام کنید که شهر را به خوبی می شناسد. راهنما می‌تواند تور را مطابق میل شما تنظیم کند، همه جاذبه‌ها را به شما نشان دهد و داستان‌های هیجان‌انگیز زیادی تعریف کند. این حتی سرگرم کننده تر خواهد بود؛ اما، افسوس، گران تر، بیش از حد.

همه این گزینه‌ها - جهت‌های تصادفی که در ذهن شما متولد می‌شوند، ناوبر تلفن هوشمند یا راهنمای انسان - به عنوان تکرارکننده‌های مجموعه وسیعی از مناظر و جاذبه‌های واقع در رم عمل می‌کنند.

## ساختار

![ulm برای این مدل دیزاین پترن](https://refactoring.guru/images/patterns/diagrams/iterator/structure-indexed.png)

1. رابط Iterator عملیات مورد نیاز برای پیمایش یک مجموعه را اعلام می کند: واکشی عنصر بعدی، بازیابی موقعیت فعلی، راه اندازی مجدد تکرار و غیره.
2. Concrete Iterators الگوریتم های خاصی را برای پیمایش یک مجموعه پیاده سازی می کند. شی تکرار کننده باید پیشرفت پیمایش را به تنهایی دنبال کند. این به چندین تکرار کننده اجازه می دهد تا از یک مجموعه به طور مستقل از یکدیگر عبور کنند.
3. رابط مجموعه یک یا چند روش را برای سازگار کردن تکرارکننده‌ها با مجموعه اعلام می‌کند. توجه داشته باشید که نوع برگشتی متدها باید به عنوان رابط تکرار شونده اعلام شود تا مجموعه های بتن بتوانند انواع مختلف تکرار کننده را برگردانند.
4. Concrete Collections نمونه‌های جدیدی از یک کلاس تکرارکننده بتن خاص را هر بار که مشتری درخواست می‌کند، برمی‌گرداند. شاید بپرسید بقیه کد مجموعه کجاست؟ نگران نباشید، باید در همان کلاس باشد. فقط این است که این جزئیات برای الگوی واقعی مهم نیستند، بنابراین ما آنها را حذف می کنیم.
5. کلاینت هم با مجموعه ها و هم با تکرارکننده ها از طریق رابط هایشان کار می کند. به این ترتیب کلاینت به کلاس‌های مشخص متصل نمی‌شود، و به شما امکان می‌دهد از مجموعه‌ها و تکرارکننده‌های مختلف با کد مشتری یکسان استفاده کنید.

به طور معمول، مشتریان به تنهایی تکرار کننده ایجاد نمی کنند، بلکه آنها را از مجموعه ها دریافت می کنند. با این حال، در موارد خاص، مشتری می تواند مستقیماً یکی را ایجاد کند. به عنوان مثال، زمانی که مشتری تکرار کننده خاص خود را تعریف می کند.

## Pseudocode

در این مثال، الگوی Iterator برای عبور از یک مجموعه خاص استفاده می‌شود که دسترسی به نمودار اجتماعی فیس‌بوک را در بر می‌گیرد. این مجموعه چندین تکرار کننده را ارائه می دهد که می توانند پروفایل ها را به روش های مختلف طی کنند.

![نمونه ای از تکرار روی پروفایل های اجتماعی.](https://refactoring.guru/images/patterns/diagrams/iterator/example.png)

تکرار کننده "دوستان" می تواند برای مرور دوستان یک نمایه مشخص استفاده شود. تکرار کننده «همکاران» همین کار را می کند، با این تفاوت که دوستانی را که در یک شرکت به عنوان فرد مورد نظر کار نمی کنند، حذف می کند. هر دو تکرار کننده یک رابط مشترک را پیاده سازی می کنند که به مشتریان اجازه می دهد تا پروفایل ها را بدون فرو رفتن در جزئیات پیاده سازی مانند احراز هویت و ارسال درخواست های REST واکشی کنند.

کد کلاینت با کلاس های مشخص همراه نیست زیرا با مجموعه ها و تکرار کننده ها فقط از طریق رابط ها کار می کند. اگر تصمیم دارید برنامه خود را به یک شبکه اجتماعی جدید متصل کنید، کافی است بدون تغییر کد موجود، مجموعه‌های جدید و کلاس‌های تکرارکننده را ارائه دهید.

## قابلیت کاربرد

* زمانی که مجموعه شما دارای ساختار داده پیچیده ای است، اما می خواهید پیچیدگی آن را از مشتریان پنهان کنید (به دلایل راحتی یا امنیتی) از الگوی Iterator استفاده کنید.

تکرار کننده جزئیات کار با یک ساختار داده پیچیده را در بر می گیرد و چندین روش ساده برای دسترسی به عناصر مجموعه را در اختیار مشتری قرار می دهد. در حالی که این رویکرد برای مشتری بسیار راحت است، مجموعه را در برابر اقدامات بی دقت یا مخربی که مشتری می تواند در صورت کار مستقیم با مجموعه انجام دهد، محافظت می کند.

* از این الگو برای کاهش تکرار کد پیمایش در برنامه خود استفاده کنید.
کد الگوریتم های تکرار غیر پیش پا افتاده بسیار حجیم است. هنگامی که در منطق تجاری یک برنامه قرار می گیرد، ممکن است مسئولیت کد اصلی را محو کند و آن را کمتر قابل نگهداری کند. انتقال کد پیمایش به تکرارکننده‌های تعیین‌شده می‌تواند به شما کمک کند کد برنامه را نازک‌تر و تمیزتر کنید.

* کد الگوریتم های تکرار غیر پیش پا افتاده بسیار حجیم است. هنگامی که در منطق تجاری یک برنامه قرار می گیرد، ممکن است مسئولیت کد اصلی را محو کند و آن را کمتر قابل نگهداری کند. انتقال کد پیمایش به تکرارکننده‌های تعیین‌شده می‌تواند به شما کمک کند کد برنامه را نازک‌تر و تمیزتر کنید.

این الگو چند رابط عمومی را هم برای مجموعه ها و هم برای تکرارکننده ها فراهم می کند. با توجه به اینکه کد شما اکنون از این رابط‌ها استفاده می‌کند، اگر مجموعه‌ها و تکرارکننده‌های مختلفی را که این رابط‌ها را پیاده‌سازی می‌کنند به آن ارسال کنید، همچنان کار خواهد کرد.

## نحوه پیاده سازی

1. رابط تکرار کننده را اعلام کنید. حداقل باید روشی برای واکشی عنصر بعدی از مجموعه داشته باشد. اما برای راحتی می توانید چند روش دیگر مانند واکشی عنصر قبلی، ردیابی موقعیت فعلی و بررسی پایان تکرار اضافه کنید.
2. رابط مجموعه را اعلان کنید و روشی را برای واکشی تکرارکننده ها شرح دهید. نوع بازگشتی باید با رابط تکرارکننده برابر باشد. اگر قصد دارید چندین گروه متمایز از تکرار کننده ها داشته باشید، می توانید روش های مشابهی را اعلام کنید.
3. برای مجموعه‌هایی که می‌خواهید با تکرارکننده‌ها قابل عبور باشند، کلاس‌های تکرارکننده مشخص را اجرا کنید. یک شی تکرار کننده باید با یک نمونه مجموعه پیوند داده شود. معمولاً این پیوند از طریق سازنده تکرارکننده ایجاد می شود.
4. رابط مجموعه را در کلاس های مجموعه خود پیاده کنید. ایده اصلی این است که یک میانبر برای ایجاد تکرارکننده، متناسب با یک کلاس مجموعه خاص، به مشتری ارائه شود. شی مجموعه باید خود را به سازنده تکرارکننده منتقل کند تا پیوندی بین آنها برقرار کند.
5. برای جایگزینی همه کد پیمایش مجموعه با استفاده از تکرار کننده، روی کد مشتری بروید. مشتری هر بار که نیاز به تکرار روی عناصر مجموعه دارد، یک شی تکرار کننده جدید واکشی می کند.