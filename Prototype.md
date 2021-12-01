<h1>
  Prototype
</h1>
<div dir="rtl">
  <p>
    نمونه اولیه (prototype) یک الگو طراحی خلاقانه است که به شما اماکن میدهد اشیاء موجود را بدون اینکه کد خود را به کلاس های آنها وابسته کنید کپی کنید
  </p>
  <h2> مشکل : </h2>
  <p>
  فرض کنید که شما یک شیء دارید و می خواهید دقیقا یک کپی از آن بسازید. چگونه این کار را انجام میدهدید؟ اول شما باید یک شی جدید از همان کلاس بسازید و سپس همه فیلد ها و پارامتر های شیء اصی را بدست بیاورید و به شیء جدید بدهید
  </p>
  <div>
    <img src="https://refactoring.guru/images/patterns/content/prototype/prototype-comic-1-en.png">
  </div>
  <p>
  راهکار خوبی است ولی یک مشکل وجود دارد. بعضی شیء ها اجزا خصوصی دارند واجازه دسترسی به آن ها را نمی دهند و نمی شود آن ها را به این شکل کپی کرد. به علاوه برای ساختن شیء کپی باید کلاس شیء اصلی را داشته باشیم و این باعث وابستگی به آن کلاس می شود. بعضیوقتا ما دسترسی به کلاس سازنده یک شیء نداریم و فقط ظاهر آن را می بینیم
  </p>
  <h2>راه حل :</h2>
  <p>
  الگو طراحی نمونه اولیه (prototype) فرایند شبیه سازی را به اشیائی که شبیه سازی شده اند واگذار میکند. این الگو یک رابط مشترک را برای تمام اشیائی که از شبیه سازی پشتیبانی میکنند می سازد.
    این رابط به شما امکان می دهد یک شیء را بدون کوپلینگ کد خود با کلاس آن شیء کلون کنید.
  </p>
  <p>
  پیاده سازی متد کلون در همه کلاس ها بسیار شبیه است. این متد یک شئ از کلاس فعلی ایجاد میکند و تمام مقادیر فیلد های شئ قدیمی را به شئ جدید منتقل میکند.
    حتی می تواند فیلدهای خصوصی را کپی کنید زیرا اکثر زبان های برنامه نویسی به اشیا اجازه می دهند به فیلد های خصوصی دیگر اشیاء متعلق به همان کلاس دسترسی پیدا کنند.
  </p>
  <p>
  شیئی که از شبیه سازی پشتیبانی میکند نمونه اولیه نامیده میشود.
    وقتی اشیاء شما دارای ده ها فیلد و صدها پیکربندی ممکن باشند شبیه سازی آن ها روش جایگزین برای زیرکلاس ساختن است.
  </p>
  <div>
    <img src="https://refactoring.guru/images/patterns/content/prototype/prototype-comic-2-en.png">
  </div>
  <p>
  این الگو به این صورت کار میکند که شما یک مجموعه از شیء های مختلف میسازید و هر وقت که یک شئ مشابه شئ های اول میخواستید به ا اینکه از اول یک شئ جدید بسازید فقط یک کلون از نمونه اویه درست می کنید
  </p>
  <h2>ساختار :</h2>
  <div>
    <img src="https://refactoring.guru/images/patterns/diagrams/prototype/structure.png">
  </div>
  <h2>مزایا و معایب:</h2>
  <h3>مزایا:</h3>
  <p>۱.می توان اشیاپ رو بدون کوپلینگ با کلاس سازنده کلون کرد</p>
  <p>۲.به خاطر ایجاد نمونه های اولیه میتوان از تکرار کد های سازنده جلوگیری کرد</p>
  <p>۳.میتوان اشیاء \یچده را راحت تر ایجاد کرد</p>
  <p>۴.روش جیاگزین وراثت در هنگام سرکار داشتن با کانفیگ های اولیه برای یک شئ پیچده پیدا می کنید</p>
  <h3>معایب:</h3>
  <p>شبیه سازی اشیاء که دارای کلاس های سازنده وابسته هستند ممکن است بسیار مشکل باشد</p>
  <h2>مثال مفهومی در  پایتون :</h2>
  <div>
    <div dir="rtl">
              در پایتون الگو طراحی نمونه اولیه با مدل copy از قبل وجود دارد
    </div>
    <code>
    import copy

    class SelfReferencingEntity:
    def __init__(self):
        self.parent = None

    def set_parent(self, parent):
        self.parent = parent


    class SomeComponent:
    """
    Python provides its own interface of Prototype via `copy.copy` and
    `copy.deepcopy` functions. And any class that wants to implement custom
    implementations have to override `__copy__` and `__deepcopy__` member
    functions.
    """

    def __init__(self, some_int, some_list_of_objects, some_circular_ref):
        self.some_int = some_int
        self.some_list_of_objects = some_list_of_objects
        self.some_circular_ref = some_circular_ref

    def __copy__(self):
        """
        Create a shallow copy. This method will be called whenever someone calls
        `copy.copy` with this object and the returned value is returned as the
        new shallow copy.
        """

        # First, let's create copies of the nested objects.
        some_list_of_objects = copy.copy(self.some_list_of_objects)
        some_circular_ref = copy.copy(self.some_circular_ref)

        # Then, let's clone the object itself, using the prepared clones of the
        # nested objects.
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__.update(self.__dict__)

        return new

    def __deepcopy__(self, memo={}):
        """
        Create a deep copy. This method will be called whenever someone calls
        `copy.deepcopy` with this object and the returned value is returned as
        the new deep copy.

        What is the use of the argument `memo`? Memo is the dictionary that is
        used by the `deepcopy` library to prevent infinite recursive copies in
        instances of circular references. Pass it to all the `deepcopy` calls
        you make in the `__deepcopy__` implementation to prevent infinite
        recursions.
        """

        # First, let's create copies of the nested objects.
        some_list_of_objects = copy.deepcopy(self.some_list_of_objects, memo)
        some_circular_ref = copy.deepcopy(self.some_circular_ref, memo)

        # Then, let's clone the object itself, using the prepared clones of the
        # nested objects.
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__ = copy.deepcopy(self.__dict__, memo)

        return new


    if __name__ == "__main__":

    list_of_objects = [1, {1, 2, 3}, [1, 2, 3]]
    circular_ref = SelfReferencingEntity()
    component = SomeComponent(23, list_of_objects, circular_ref)
    circular_ref.set_parent(component)

    shallow_copied_component = copy.copy(component)

    # Let's change the list in shallow_copied_component and see if it changes in
    # component.
    shallow_copied_component.some_list_of_objects.append("another object")
    if component.some_list_of_objects[-1] == "another object":
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # Let's change the set in the list of objects.
    component.some_list_of_objects[1].add(4)
    if 4 in shallow_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )

    deep_copied_component = copy.deepcopy(component)

    # Let's change the list in deep_copied_component and see if it changes in
    # component.
    deep_copied_component.some_list_of_objects.append("one more object")
    if component.some_list_of_objects[-1] == "one more object":
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # Let's change the set in the list of objects.
    component.some_list_of_objects[1].add(10)
    if 10 in deep_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )

    print(
        f"id(deep_copied_component.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent)}"
    )
    print(
        f"id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent)}"
    )
    print(
        "^^ This shows that deepcopied objects contain same reference, they "
        "are not cloned repeatedly."
    )
    
      
      ====== output =====
      Adding elements to `shallow_copied_component`'s some_list_of_objects adds it to `component`'s some_list_of_objects.
      Changing objects in the `component`'s some_list_of_objects changes that object in `shallow_copied_component`'s some_list_of_objects.
      Adding elements to `deep_copied_component`'s some_list_of_objects doesn't add it to `component`'s some_list_of_objects.
      Changing objects in the `component`'s some_list_of_objects doesn't change that object in `deep_copied_component`'s some_list_of_objects.
      id(deep_copied_component.some_circular_ref.parent): 4429472784
      id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent): 4429472784
      ^^ This shows that deepcopied objects contain same reference, they are not cloned repeatedly.
  </code>
  </div>
</div>

