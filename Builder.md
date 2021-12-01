<h1>Builder</h1>
<div dir="rtl">
<p>
سازنده (Builder) یک الگوی طرای خلاقانه است که شما اماکن می دهد شیء های پیچیده را مرحله به مرحله بسازید. این الگو به شما اجازه می دهد تا انواع مختلفی از یک شیء را با استفاده از کد ساختاری یکسان تولید کنید
</p>
<p>
<img src="https://refactoring.guru/images/patterns/content/builder/builder-en.png">
</p>
<h2>
مشکل :
</h2>
<p>
یک شیء پیچیده را تصور کنید که نیاز به مقداردهی های اولیه فراوان و تو در تو دارد. چنین کدی معمولا در داخل یک سازنده هیولایی با پارامتر های زیاد دفن می شود.
</p>
<p>
برای مثال تصور کنید که می خواهیم یک شیء خانه بسازیم. برای یک خانه ساده نیاز به دیوار‌‍‍ زمین در پنجره و یک سقف داریم. اما اگر بخواهیم یک خانه بزرگتر یا حیاط یا استخر و... ساخت چکار باید کرد؟
</p>
<p>
ساده ترین راه حل این است که کلاس اولیه خانه را گسترش دهیم و زیرکلاس های از ان درست کنیم که همه ویژگی هیا مورد نیاز ما را پوشش دهند. که باعث ایجاد تعداد زیادی زیرکلاس ها می شود و ما هر دفعه برای اضافه کردن یک پارامتر جدید باید همه آن ها را تغییر دهیم
</p>
<p>
<img src="https://refactoring.guru/images/patterns/diagrams/builder/problem2.png">
</p>
<p>
یک راه حل دیگر این است که به کلاس اصلی متد ها و ویژگی های زیادی اضافه کنیم که همه پارامتر های مورد نیاز ما را داشته باشد. که در این راه اکثر اوقات بیشتر پارامتر های ما بدون استفاده می مانند و کلاس سازنده را بسیار کثیف میکنند.
</p>
<h2>
راه حل :
</h2>
<p>
الگو طراحی سازنده (Builder) پیشنهاد میکند که متد های سازنده شیء را از کلاس اصلی جدا کرده و در اشیاء دیگه که سازنده نامیده میشوند ذخیره کرد.
</p>
<p>
<img src="https://refactoring.guru/images/patterns/diagrams/builder/solution1.png">
</p>
<p>
این الگو مراحل ساخت یک شیء را به گام های مختلف دسته بندی می کند و شما برای ساختن یک شیء فقط کافی است تا تعدادی از این گام ها را اجرا کنید. نکته مهم این است که نیاز به اجرا کردن همه گام ها نیست و فقط آن ها که برای ساختن شیء ضروری هستند اجرا می شوند.
</p>
<p>
اگر یک گام ساختن شیء حالت های مختلفی داشته باشد می توان کلاس های سازنده مختلفی طراحی کرد که این گام را به شکل های مختلف اجرا کرد. برای مثال اگر بخواهیم دیوار خانه را از چوب یا سنگ یا الماس بسازیم کلاس سازنده های مختلف میسازیم که گام ساختن دیوار آن های متفاوت است.
</p>
<h2>
ساختار :
</h2>
<p>
<img src="https://refactoring.guru/images/patterns/diagrams/builder/structure.png">
</p>
<h2>
مزایا و معایب :
</h2>
<h3>
مزایا :
</h3>
<p>
۱. می توان یک شیء را گام به گام ساخت. یک گام را به شکل های مختلف یا به طور بازگشتی اجرا کرد.
</p>
<p>
۲.می توان از یک کد برای ساختن شکل های مختلف یک شیء استفاده کرد.
</p>
<p>
۳. می توان قسمت ساخت یک شیء را از قسمت منطقی آن جدا کرد.
</p>
<h3>
معایب :
</h3>
<p>
۱. پیچیدگی کد به خاطر نیاز به ساختن کلاس های مختلف بالا می رود.
</p>
<h2>
مثال مفهومی در زبان پایتون :
</h2>
<code dir="ltr">

	from __future__ import annotations
	from abc import ABC, abstractmethod
	from typing import Any


 	class Builder(ABC):

    """
    The Builder interface specifies methods for creating the different parts of
    the Product objects.
    """

    @property
    @abstractmethod
    def product(self) -> None:
        pass

    @abstractmethod
    def produce_part_a(self) -> None:
        pass

    @abstractmethod
    def produce_part_b(self) -> None:
        pass

    @abstractmethod
    def produce_part_c(self) -> None:
        pass


 	class ConcreteBuilder1(Builder):
    """
    The Concrete Builder classes follow the Builder interface and provide
    specific implementations of the building steps. Your program may have
    several variations of Builders, implemented differently.
    """

    def __init__(self) -> None:
        """
        A fresh builder instance should contain a blank product object, which is
        used in further assembly.
        """
        self.reset()

    def reset(self) -> None:
        self._product = Product1()

    @property
    def product(self) -> Product1:
        """
        Concrete Builders are supposed to provide their own methods for
        retrieving results. That's because various types of builders may create
        entirely different products that don't follow the same interface.
        Therefore, such methods cannot be declared in the base Builder interface
        (at least in a statically typed programming language).

        Usually, after returning the end result to the client, a builder
        instance is expected to be ready to start producing another product.
        That's why it's a usual practice to call the reset method at the end of
        the `getProduct` method body. However, this behavior is not mandatory,
        and you can make your builders wait for an explicit reset call from the
        client code before disposing of the previous result.
        """
        product = self._product
        self.reset()
        return product

    def produce_part_a(self) -> None:
        self._product.add("PartA1")

    def produce_part_b(self) -> None:
        self._product.add("PartB1")

    def produce_part_c(self) -> None:
        self._product.add("PartC1")


	class Product1():
	
    """
    It makes sense to use the Builder pattern only when your products are quite
    complex and require extensive configuration.

    Unlike in other creational patterns, different concrete builders can produce
    unrelated products. In other words, results of various builders may not
    always follow the same interface.
    """

    def __init__(self) -> None:
        self.parts = []

    def add(self, part: Any) -> None:
        self.parts.append(part)

    def list_parts(self) -> None:
        print(f"Product parts: {', '.join(self.parts)}", end="")


	class Director:
    """
    The Director is only responsible for executing the building steps in a
    particular sequence. It is helpful when producing products according to a
    specific order or configuration. Strictly speaking, the Director class is
    optional, since the client can control builders directly.
    """

    def __init__(self) -> None:
        self._builder = None

    @property
    def builder(self) -> Builder:
        return self._builder

    @builder.setter
    def builder(self, builder: Builder) -> None:
        """
        The Director works with any builder instance that the client code passes
        to it. This way, the client code may alter the final type of the newly
        assembled product.
        """
        self._builder = builder

    """
    The Director can construct several product variations using the same
    building steps.
    """

    def build_minimal_viable_product(self) -> None:
        self.builder.produce_part_a()

    def build_full_featured_product(self) -> None:
        self.builder.produce_part_a()
        self.builder.produce_part_b()
        self.builder.produce_part_c()


	if __name__ == "__main__":
    """
    The client code creates a builder object, passes it to the director and then
    initiates the construction process. The end result is retrieved from the
    builder object.
    """

    director = Director()
    builder = ConcreteBuilder1()
    director.builder = builder

    print("Standard basic product: ")
    director.build_minimal_viable_product()
    builder.product.list_parts()

    print("\n")

    print("Standard full featured product: ")
    director.build_full_featured_product()
    builder.product.list_parts()

    print("\n")

    # Remember, the Builder pattern can be used without a Director class.
    print("Custom product: ")
    builder.produce_part_a()
    builder.produce_part_b()
    builder.product.list_parts()
    
    
    
    
    ====== output =====
    
	Standard basic product: 
	Product parts: PartA1

	Standard full featured product: 
	Product parts: PartA1, PartB1, PartC1

	Custom product: 
	Product parts: PartA1, PartB1
</code>

</div>
