
<h2>Decorator</h2>
<div dir="rtl">
<p>
هنگامی که می خواهید رفتار شی ای در برنامه را تغییر دهید، ممکن هست extend کردن کلاس اولین راهی باشد که به ذهن شما برسد. اما باید نکاتی را در نظر بگیرید:</p>
<p>
اول اینکه ارث بری، استاتیک است به این معنا که نمی توانید رفتار شی ای را هنگام اجرا تغییر دهید. فقط می توانید شی را با شی ایجاد شده از زیرکلاسی دیگر جایگزین کنید.
و دوم اینکه در بیشتر زبان ها هر زیرکلاس نمی تواند چندین کلاس والد داشته باشد و تنها از یک کلاس ارث بری می کند.
</p>
<p>
روش طراحی ‌Decorator به منظور اضافه کردن رفتارهای جدید به اشیای در حال اجرا ، استفاده می شود و این کار را بدون شکستن کدهایی که از این اشیا استفاده می کنند، انجام می دهد.
</p>
<p>
برای رسیدن به این هدف ، می توان از Aggregation و Composition به جای ارث بری استفاده کرد. در هردوی این رابطه هنگامیها، یک شی ارجاع به شی دیگری دارد و کاری را به آن محول می کند اما در ارث بری، یک شی رفتارها را از والد خود گرفته و خودش کارها را انجام می دهد.
در Aggregation شی A شامل شی B هست و B بدون A می تواند زندگی کند. در Compositio شی A شامل شی B هست اما ‌B بدون A زنده نمی ماند.
در Aggregation و Compositionُ ، عکس ارث بری می توان به منظور ایجاد تغییرات در زمان اجرا ، شی متصل (helper) را با شی ای دیگر جایگزین کرد و رفتار container را در زمان اجرا تغییر داد.
Aggregation و Composition ایده ی ورای بسیاری از الگوهای طراحی می باشد.
</p>
<p>
نام دیگرالگوی طراحی Wrapper، Decorator می باشد. در این روش طراحی،Wrapper شی ای هست که می تواند به اشیا target متصل گردد. شی Wrapper شامل تمام متدهای شی target می باشد و تمام request هایی که به آن می رسد را به target می فرستد. در نظر داشته باشید که wrapper ممکن هست نتایج را قبل و یا بعد از ارسال request به target، با انجام کارهایی تغییر بدهد.
</p>
<p>
اما چه زمانی یک wrapper مانند یک دکوریتور واقعی عمل می کند؟ همانطور که قبلا گفته شد، یک wrapper تمام interfaceهای شی target را اجرا می کند. به این دلیل هست که از دید کاربر تمام این اشیا یکی دیده می شوند. درون دکوریتور یک attributeی از جنس target(شی ای که می خواهد پوشانده شود) قرار داده می شود. همچنین این دکوریتور می تواند تمام اشیای زیرکلاس های target را نیز ‍پوشش بدهد.
</p>
<p>
ساختار زیر به خوبی این موضوع را نمایش می دهد:
</p>
</div>

![enter image description here](https://refactoring.guru/images/patterns/diagrams/decorator/structure.png?id=8c95d894aecce5315cc1)
<div  dir="rtl">
<p>
۱: component کلاسی هست که از زیرکلاسهای آن، اشیای تارگت ساخته می شوند و توسط دکوریتور پوشش داده می شوند.</p>
<p>
۲: conceret component کلاسی هست که اشیای آن پوشش داده می شوند. در این کلاس رفتارهای basic تعریف شده است که می تواند توسط دکوریتورها تغییر کند.</p>
<p>
۳: کلاس Base Decorator یک attribute ی دارد که اشاره به شی target می کند. این کلاس تمام عملیات را روی شی target انجام می دهد.
</p>
<p>
۴: در کلاس Concrete Decorators رفتارها و عملیات بیشتری نسبت به کلاس والد ‌Base Decorator تعریف می شود. این کلاس متدهای کلاس والد را override می کند و عملیات مورد نظر خود را قبل و یا بعد از متدهای والد انجام می دهد.
</p>
<p>
۵: کلاینت می تواند هر کامپوننت را در چندین لایه دکوریتور بپوشاند.
</p>
<p>
برای دیدن اطلاعات بیشتر و مشاهده ی کدها به به لینک زیر مراجعه کنید:
</p>

[Decoraotr Design Pattern](https://refactoring.guru/design-patterns/decorator)
</div>





















