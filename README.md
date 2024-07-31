# Machine-Vision-Project
افزایش داده رویکردی است که می‌تواند به طور قابل ملاحظه‌ای تعداد نمونه‌های داده در مجموعه داده را برای آموزش یک مدل افزایش دهد. در مورد مجموعه داده‌های تصویر، این رویکرد از عملیات پردازشی مانند انعکاس، چرخش، برش یا پر کردن برای افزایش داده ها استفاده می‌کند. در این مطالعه، دو عملیات پردازش تصویر، یعنی انعکاس و چرخش، برای افزایش داده استفاده شده‌اند. برای این منظور رویکرد زیر در نظر گرفته شد: 
1- در مرحله اول از افزایش داده، 90 تصویر ایکس‌ری برای به دست آوردن 90 تصویر جدید دیگر، منعکس(flipped) شده‌اند.
2- در مرحله دوم، 90 تصویر اصلی با زاویه 90 درجه چرخانده شده‌اند تا 90 تصویر دیگر به دست آید.
3-  در گام بعد تصاویر اصلی را با زاویه 180 درجه چرخانده تا 90 تصویر جدید دیگر به حاصل شود.
4- در نهایت، 90 تصویر اصلی با زاویه 270 درجه چرخانده شده‌اند تا به 90 تصویر دیگر برسیم.
این عملیات‌ها  منجر به تولید یک مجموعه داده که شامل 450 تصویر ایکس‌ری COVID-19 است، شدند.
سپس به منظور افزایش داده، اقدام به افزایش داده های داده شده برای این تمرین می‌کنیم. اما ابتدا باید داده ها را در محیط colab بارگذاری کنیم.
در صورت عدم اطلاع از استفاده از colab می‌توانید از آموزش زیر استفاده نمایید:

https://www.aparat.com/v/u751kb9

پس از بارگذاری داده ها در محیط colab، اقدام به data augmentation یا افزایش داده (داده های آموزش) با توجه به عملیات های مورد استفاده در مقاله می‌کنیم. برای این منظور اقدام به تعریف تابع data_augment  می‌کنیم.
این تابع ابتدا دایرکتوری مربوط به داده های اصلی و دایرکتوری خروجی برای ذخیره داده های augment شده را دریافت می‌کند. ابتدا بررسی می‌کند که آیا دایرکتوری خروجی وجود دارد یا خیر؟ اگر وجود نداشت، اقدام به ایجاد آن می‌کند. سپس تمامی داده های عکس که دارای پسوند “.jpg”، “.jpeg” و “.png” هستند را ابتدا ذخیره می‌کند و سپس اقدام به انجام عملیات های مربوط به افزایش داده به ترتیب کرده و بعد از هر عملیات فایل جدید را با نام مناسب ذخیره می‌کند. برای عملیات انعکاس(flip)، از آنجایی که در مقاله اشاره ایی صریح به انعکاس عمودی یا افقی نشده، قبل از اقدام به انعکاس تصویر داده، نوع انعکاس با استفاده از یک تولیدکننده عدد تصادفی انتخاب می‌شود. چرخش ها نیز به ترتیب 90، 180 و 270 درجه انجام می‌شوند و هر کدام ذخیره می‌شوند.
سپس داده های افزایش داده شده و داده های آزمون را در برنامه بارگذاری می‌کنیم.
سپس اقدام به rescale کردن داده های آموزش و آزمون می‌کنیم. برای داده های validation نیز از داده های آموزش زیر مجموعه‌ای با اندازه 0.25  داده های آموزش، ایجاد می‌کنیم و آن ها را نیر rescale می‌کنیم.
سپس یک batch  از داده های آموزش که افزایش داده شده ‌اند را گرفته و اقدام به چاپ 4 داده اول آن batch کردیم. (هر batch دارای ساختار (32, 150, 150, 3) می‌باشد. یعنی در هر batch  به تعداد 32 داده موجود است.)
همچنین batch دیگری را از این داده ها در نظر گرفتیم و 4 تصویر دیگر آن را نیز چاپ کردیم.
یک معماری شبکه عصبی پیچشی (CNN) برای وظایف دسته‌بندی دودویی استفاده شده است. مدل CNN شامل ۳۸ لایه است که شامل لایه‌های کانولوشن (Conv2D)، max pooling، dropout، تابع فعال‌سازی، نرمال‌سازی دسته‌ای (batch normalization)، flatten، و لایه‌های کاملاً متصل(fully connected layers) می‌شود. ابعاد تصویر ورودی به (150، 150، 3) برای تصاویر RGB تعیین شده است. لایه‌های کانولوشن از هسته ۳ × ۳ استفاده می‌کنند. پس از هر لایه Conv2D، تکنیک‌های مختلفی اعمال می‌شود، از جمله max pooling (با اندازه ۲ × ۲)، نرمال‌سازی دسته‌ای (با محور 1-)، تابع فعال‌سازی ReLU، و لایه dropout (با نرخ 20%). خروجی نهایی، که از ۲۵۶ نورون در آخرین لایه Conv2D به دست می‌آید، از طریق لایه‌های max pooling، نرمال‌سازی دسته‌ای، فعال‌سازی، و لایه dropout عبور می‌کند. برای دسته‌بندی دودویی، مدل از تابع از دست دادن متقاطع دودویی (BCE) و تابع فعال‌سازی sigmoid استفاده می‌کند، زیرا تنها یک نود خروجی برای دسته‌بندی داده به یکی از دو کلاس موجود لازم است.  بهینه‌ساز "Adam" برای تنظیم پویا ویژگی‌های وزن و نرخ یادگیری مدل، به منظور کاهش از دست دادن مدل استفاده می‌شود. با توجه به معماری بیان شده و بهره‌ از کتابخانه tensorflow  اقدام به پیاده‌سازی مدل پیشنهادی می‌کنیم.
سپس اقدام به آموزش مدل می‌کنیم که از داده های validation که در گام های قبل تولید کردیم، استفاده کردیم. همچنین تعداد epoch ها را مشابه مقاله برابر با 50 قرار داده ایم. مقدار learning rate  را برابر با 0.006  قرار دادیم. این مقدار را به صورت تجربی و با انجام آزمایش به دست آوردیم. پس از آموزش مدل اقدام به رسم نمودار loss و  accuracy برای داده های آموزش و validation کردیم.
سپس اقدام به ارزیابی شبکه پیاده سازی شده، می‌کنیم. برای ارزیابی بیشتر این ساختار شبکه اقدام به تعریف مدل هایی با تعداد لایه کانولوشن 1 ، 2، 3، 4، 5 کردیم و با داده های افزایش داده شده مشابه مدل اصلی که دارای 6 لایه کانولوشن است، آن ها را آموزش داده و سپس با استفاده از داده های آزمون و validation اقدام به ارزیابی هرکدام از مدل ها می‌کنیم.





