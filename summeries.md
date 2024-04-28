DOCKER

تعریف :

Docker پلتفرمی برای توسعه، ارسال و اجرای برنامه‌های کاربردی با استفاده از کانتینر است

container

کانتینرها شکل سبکی از مجازی‌سازی هستند که به برنامه‌ها و وابستگی‌های آن‌ها امکان بسته‌بندی و اجرای مداوم در محیط‌های مختلف را می‌دهند.

Docker راهی برای خودکارسازی استقرار، مقیاس‌بندی و مدیریت برنامه‌ها ارائه می‌کند که ایجاد، توزیع و اجرای نرم‌افزار را آسان‌تر می‌کند.

نکات :

container ها باید ساده و تک proccess هست

container ها باید سبک باشند

دستورات

wsl --list --verbose

مشاهده vm های موجود

نصب ubuntu

wsl install

wsl --setdefault Ubuntu

update ubuntu

sudo apt update

sudo apt full-upgrade -y

اجرای دستورات docker

ورژن

docker --version

تست داکر با برنامه سلام دنیا

docker run hello-world

دریافت image برنامه nginx از docker hub

docker pull nginx

اجرای image

docker run image-name

exp.

docker run nginx

لیست پردازش های فعال

docker ps

لیست پردازش های کلی داکر

docker ps -a

name و docker-id یکتا هستند

ps aux | grep nginxدستور

برای نمایش فرآیندهای مربوط به nginx در حال اجرا بر روی سیستم استفاده می شود.

دستور docker inspect container-id

نمایش اطلاعات مربوط به entity

مثلا

docker inpect e17af1bc9cb1

توقف container

docker stop container-id

اجرای کانتینر موجود :

اول شروع

docker start <container_name_or_id>

بعد اجرا

docker exec -it <container_name_or_id> <command>

docker container ls -a

معادل

docker ps -a

حذف container :

docker rm container-id[s] or container-name[s]

exp.

docker rm 86ab6ffaf2d0 nifty_chatterjee

container های فعال اول باید stop و بعد پاک شوند

docker pull ubuntu

docker run ubuntu

بعد از اجرا می بینیم هیچ اتفاقی نمیافتد چون ubuntu یک os هست و تنها proccess ی که دارد bash هست که خارج شده است که در docker ps -a قابل مشاهده هست

برای این مساله باید به صورت interactive سیستم ubuntu اجرا شود یعنی

docker run -it ubuntu

تغییر نام پیشفرض container

docker run -it --name myos ubuntu

بعد از خروج از ubuntu کانتینر پاک شود با --rm

docker run -it --name myos ubuntu

لیست image های موجود در local

docker images ls

tag یعنی ورژن image که pull شده

با : میتوان تگ را مشخص کرد

مثلا نسخه 18.04 اوبونتو را اگر بخواهیم مینویسم

docker pull ubuntu:18.04

برای حذف image های موجود در local

docker rmi image-id[s] or repository[s]

برای استفاده از image یک کاربر در hub.docker به نام anvari

docker anvari/image-name

در hub.docker برای هر image بخشی به عنوان Supported tags وجود دارد که نسخه های مختلف مشخص شده

برای دانلود بالاترین نسخه که با 1.21 شروع شده مثلا 1.21.2 1.21.4 1.21.6 میزنیم

docker pull image-name:1.21

که به صورت پیشفرض بالاترین نسخه 1.21 یعنی 1.21.6 را دانلود میکند

کانتینرها یا از طریق نتورک با هم در ارتباط هستند یا از طریق استوریج

اشتراک حافظه میان دو کانتینر مختلف از طریق فایل سیستم امکان پذیر هست که هر دو کانتینر از یک پوشه مشترک استفاده میکنند

معمولا هر سازمان که از داکر استفاده میکند برای خودش یک ریجیستری بالا میاره و image ها رو در آنجا قرار میده

docker pull python:3.8-alpine

یعنی image برنامه python نسخه 3.8 که سیستم عاملش alpine هست را دانلود کن

docker run -it python:3.8-alpine

پایتون دانلود شده را اجرا میکنیم

docker run -it python:3.8-alpine /bin/sh

با دستور بالا به جای اجرای معمولی پایتون 3.8 بخش shell را اجرا میکنیم

دستور apk add در shell پایتون برابر با apt get در لینوکس هست

ابتدا bash را نصب میکنیم

apk add bash

سپس با دستور bash اجرا میکنیم

سپس ادیتور vim را نصب میکنیم

apk add vim

ساخت فایل با vim

vim app.py

در vim با زدن esc به حالت دستور وارد می شویم

در بخش دستور با نوشتن :qw فایل نوشته شده ذخیره و خارج میشود

ایجاد یک image

docker commit container-id image-name

docker run --rm image-name

با نوشتن --rm در دستور بالا بعد از اتمام container حذف میشود

docker run --rm --publish 80:5000 myapp flask run

نکته مهم :

روال کار روی ویندوز با wsl و docker desktop بدین صورت هست که app پایتونی وقتی از طریق wsl اجرا میشود روی host 0.0.0.0 و port 5000 برای flask تنظیم شود و هنگام اجرا image از طریق دستور بالا پورت 5000 local که در اینجا wsl یعنی لینوکس محل می باشد روی پورت 80 داکر امیج تنظیم شود که میشود پورت default مرورگر ویندوز

یعنی اگر در flask app قطعه کد

if \_\_name\_\_ == '\_\_main\_\_':

    app.run(host='0.0.0.0', port=5000)

تنظیم شود و با دستور قبل build شود آنگاه روی مرورگر با کلمه localhost اجرا میشود

در دستور بالا اعلام کردیم پورت 80 هاست را روی پورت 5000 کانتینر مپ کن

Dockerfile

From python:3-8-alpine

یعنی برو از image به نام pytthon:3.8-alpine بخون

WORKDIR /app

یعنی همه کارها رو در شاخه app انجام بدی

COPY . .

نقطه اول از هاست هست یعنی نقطه فعلی هاست

نقطه دوم برای image هست یعنی نقطه فعلی image

RUN pip install -r requirements.txt

یعنی اجرا کن دستور مورد نظر

CMD ["python3","app.py"]

یعنی از پایتون 3 استفاده کن و فایل app.py رو اجرا کن

docker build -t pyapp:1 .

یعنی اجرا کن فایل داکر را از imageبه نام pyapp

نسخه 1 در مسیر فعلی

best practice python app's docker files :

FROM python:3.8-alpine

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY app.py .

EXPOSE 80

CMD ["python3","app.py"]

دایرکتیو expose صرفا اطلاع میدهد که این برنامه روی پورت 80 ظاهر می شود

ENTRYPOINT ["python3","app.py"]

اگر به جای cmd از ENTRYPOINT استفاه کنیم دیگ نمیتوانیم دستور

docker run -t --rm pyapp:4 python3 را اجرا کنیم

redis یک data storing memory هست یعنی اطلاعات را موقتا در حافظه رم ذخیره میکند و یک نوع پایگاه داده محسوب می شود

docker pull redis:6

برای ساخت یک برنامه redis ابتدا برنامه pyapp را با استفاده از محتویات
این آدرس app.py · master · docker101 / py-counter
تغییر میدهیم
این برنامه به redis وصل میشود
و همچنین redis را به requirements.txt اضافه میکنیم
حال میتوانیم برنامه را اجرا کنیم که متغیر نام خوانده نمیشود همچنین در بخش visit به redis وصل نمیشود

برای اینکه بتوانیم به redis وصل شویم ابتدا از طریق کد زیر برنامه ای از image redis ایجاد مکنیم
docker run --name redis1 redis:6

نام برنامه را redis1 میگذاریم تا بتوانیم به راحتی در هر جا آن را فراخوانی کنیم

همچنین محتویات app.py در pyapp را به حالت زیر تغییر میدهیم

.
.
.

Connect to Redis
redis = Redis(host=os.getenv("REDIS_HOST","127.0.0.1"), db=0, socket_connect_timeout=2, socket_timeout=2)
...

حالا برای اجرای pyapp:7 دستور را به صورت زیر مینویسیم

docker run -it --rm --publish 81:5000 -e
REDIS_HOST=172.17.0.3 -e NAME=MrCod3r pyapp:7

در دستور بالا مقدار redis_host و name به عنوان enviroment var انتقال داده شده اند

حالا نرم افزار درست کار میکند و وقتی localhost:81 را مشاهده میکنیم صفحه ای با مشخصات زیر قابل مشاهده است

Hello MrCod3r!
Hostname: fc99a4ab2060
Visits: 6

که در آن hostnameمقدار همان id container شناسه container در حال اجرا هست

همانطور که دقت شد در بخش app قسمت redis هاست به صورت دستی وارد شده که در برنامه های بزرگ و شلوغ کار سخت میشود

برای رفع مشکل docker از یک سیستم شبیه dns استفاده میکند
با این تفاوت که نام container ها به عنوان دامنه عمل میکند یعنی اسم container به ip وصلmap میشود
تنها نکته این هست که هر دو container باید در یک network باشند

network :
یک مفهوم انتزاعی هست شبکه ای بین container ها موجود می شود که با نام هم قابل تعامل خواهند بود

برای اجرای network :
ابتدا دو تا نرم افزار ها stop میکنیم

ایجاد یک شبکه :
docker network create <net-name>
exp.
docker network create net-app
در کد بالا یک شبکه با نامه net-app ایجاد کردیم
docker network ls
لیست تمام شبکه ها

هر شبکه یک driver دارد

برای این ابتدا محتویات app.py به شکل زیر تغییر میکند

Connect to Redis
redis = Redis(host=os.getenv("REDIS_HOST","redis1"), db=0, socket_connect_timeout=2, socket_timeout=2)

یعنی redis1 به عنوان host اعلام میشود

از طرفی container redis1 پاک مکنیم و از دوباره با تعریف شبکه اجرا میکنیم

docker rm redis1

docker run --name redis1 --network net-app redis:6

و برنامه pyapp

docker run -it --rm --publish 81:5000 -e REDIS_HOST=redis1 -e NAME=MrCod3r --network net-app pyapp:7

این روش به نوعی ترکیب دو برنامه در داکر بود که compose نام دارد که به صورت دستی انجام شد و این روال کار نیست

روال کار در داکر استفاده از docker compose هست
