# الگوریتم استراسن
والکر استراسن الگوریتم استراسن را در سال ۱۹۶۹ منتشر کرد. اگرچه الگوریتم او فقط کمی سریع تر از الگوریتم‌های استاندارد برای ضرب ماتریس است، اما او اولین کسی بود که اشاره کرد رویکرد استاندارد مطلوب نمی‌باشد. مقالهٔ او به جستجوی الگوریتم‌های سریعتر مانند الگوریتم پیچیده تر Coppersmith–Winograd منتشر شده در سال ۱۹۸۷ پرداخت. 

### الگوریتم
![This is an image](https://upload.wikimedia.org/wikipedia/fa/3/39/AL-1.JPG)

ولکر استراسن با بررسی‌هایی که انجام داد، الگوریتم تقسیم و غلبه‌ای برای ضرب ماتریس‌ها با استفاده از تقسیم‌بندی ارائه داد که به جای هشت عمل ضرب در هر مرحله، هفت عمل نیاز دارد. به این ترتیب:

  

T′(n)=7T′(n2)=72T′(n22)=⋯=7kT′(n2k)
n=2k⇒T′(n)=7kT′(nn)=(2log27)kT′(1)=(2k)log27×1=nlog27

  

در نتیجه مرتبه‌ی اجرای الگوریتم به O(n2.81) تبدیل می‌شود. به عنوان مثال اگر n برابر 1024 باشد:

  

n=1024=210⇒k=10
T(1024)=810=1073741824
T′(1024)=710=282475249
T(1024)T′(1024)≃3.8

  

یعنی در این حالت زمان محاسبه‌ی حاصلضرب به روش استراسن نسبت به حالت عادی نزدیک به چهار برابر کمتر می‌شود.

در روش استراسن ماتریس‌های زیر که همه از مرتبه‌ی n2 هستند از روی زیرماتریس‌های ماتریس‌های A و B ساخته می‌شوند:

  

P=(A11+A22)(B11+B22)
Q=(A21+A22)B11
R=A11(B12−B22)
S=A22(B21−B11)
T=(A11+A12)B22
U=(A21−A11)(B11+B12)
V=(A12−A22)(B21+B22)

  

که تنها هفت عمل ضرب برای محاسبه نیاز دارند. استراسن ثابت کرد زیرماتریس‌های متناظر ماتریس حاصلضرب از رابطه‌های زیر به دست می‌آید:

  
**C11=P+S−T+V**
**C12=R+T**
**C21=Q+S**
**C22=P−Q+R+U**

  
# تقسیم کردن ماتریس‌ها به چهار بخش - برای محاسبه به روش استراسن - تا زمانی ادامه پیدا می‌کند که مرتبه‌ی ماتریس‌ها به 2 برسند. وقتی به این مرحله رسیدیم، با تعریف اصلی ضرب ماتریس‌ها حاصلضرب را محاسبه می‌کنیم.




 نکته: علت اینکه چرا تنها عمل ضرب را بررسی کردیم این بود که عمل ضرب هزینه‌ی زمانی بیشتری نسبت به عمل جمع و تفریق دارد. اگرچه  می‌توان ثابت کرد که این روش به ازای مقادیر بزرگ n از نظر میزان عمل جمع و تفریق هم کاراتر است.

### پیچیدگی الگوریتم
ضرب ماتریسی استاندارد تقریباً عملیات محاسباتی ۲n^۳ (که n=۲^n) (جمعها و ضرب‌ها) را می‌پذیرد؛ پیچیدگی مجانبی (O(N۳می‌باشد. تعداد جمع‌ها و ضرب‌های مورد نیاز در الگوریتم استراسن را می‌توان به صورت زیر محاسبه کرد:

اجازه دهید (f(n تعداد عملیات برای یک ماتریس ۲n * ۲n باشد. آنگاه با عملیات بازگشتی الگوریتم استراسن می‌بینیم که برای برخی l ثابت که به تعداد جمع‌های انجام شده در هر عملیات الگوریتم وابسته‌است. یعنی پیچیدگی مجانبی برای ضرب ماتریسها با استفاده از الگوریتم استراسن به شرح زیر است: 
![This is an image](https://upload.wikimedia.org/wikipedia/fa/9/97/AL-6.JPG)


هرچند کاهش در تعداد عملیات محاسباتی تا حدودی به بهای کاهش ثبات عددی می‌باشد. 