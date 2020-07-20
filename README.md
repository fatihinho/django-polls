# django-polls
## Django starter project

Part 1
-----------
1- 'django-admin startproject mysite' komutu ile mysite isimli projemizi oluşturduk.
   
2- 'py manage.py runserver' komutu ile server'ımızı başlatıyoruz

3- 'py manage.py startapp polls' komutu ile projemizde polls isimli application'ı oluşturduk

4-  polls/views.py, polls/urls.py, mysite/urls.py dosyalarına gerekli kodları yazarak ilk uygulamayı yazdık.
    
	urlpatterns = [] ile views'taki url'leri tanımladık. Request, Response vs. işlemleri

5-  Uygulamanın database'i için sqlite'ı kullanıyoruz (default olarak gelir)

6- 'py manage.py migrate' ile database'i kuruyoruz.

7-  polls/models.py dosyasında uygulamamız için gerekli olan db modelini oluşturuyoruz.

8-  mysite/settings.py dosyasının içindeki INSTALLED_APPS listesine uygulamamızı 'polls.apps.PollsConfig' şeklinde tanımlıyoruz.

9- Önce 'py manage.py makemigrations polls' sonrasında da 'py manage.py sqlmigrate polls 0001' komutları ile database sql komutlarını
tanımlamış oluyoruz.

Part 2
----------
10- Tekrardan 'py manage.py migrate' komutu ile database'imizin son halini uyguluyoruz.
(Yani;  'py manage.py makemigrations' -> değişikliği yapar 
	'py manage.py migrate'        -> değişikliği uygular)

11- 'py manage.py shell' komutu ile python shell(django settings'e erişebilecek versiyonu ile) sanki py shell gibi console'a geçiyoruz.

12- Bu shell ile veritabanına veri ekleme gibi işlemleri gördük.

13- 'py manage.py createsuperuser' komutu ile projeye admin hesabı açıyoruz.

14- polls/admin.py içerisine admin.site.register(Question) kodu ile admin sayfasında Question'ları yönetebilme şansımız olur.

Part 3
----------
15- polls/views.py dosyasına bir kaç tane daha url ekledik. detail, results, vote gibi.

16- polls/views.py dosyasındaki index fonksiyonunun içine ekrana soruları basması için kod parçacığı yazdık.

17- polls/templates/polls/index.html dosyası oluşturduk ve ilk template'imizi yazdık.

18- polls/views.py dosyasında render() methodu ile template'imizi görüntüledik sınıfını kullanarak template'imizi kullandık.

Part 4
----------
19- Generic views tiplerini gördük. ListView ve DetailView sınıflarını kullanarak daha kısa kod yazmış olduk.

Part 5
----------
20- İlk TestCase'imizi yazdık. 

21- 'py manage.py test polls' komutu ile polls uygulamamızda test başlattık.

Part 6
----------
22- polls/static/polls/style.css uzantılı dosyasına css kodumuzu yazıyoruz

23- Html dosyamızın en üstüne {% load static %} ile static klasöründeki css dosyalarımızı tanımlıyoruz.
Sonrasında altına link olarak .css uzantılı dosyamızı tanımladık. href="{% static 'polls/style.css' %}" şeklinde.

Part 7
----------
24- admin modülündeki ModelAdmin sınıfını implement ettiğimiz QuestionAdmin isminde bir sınıf yazdık.
O sınıfın içerisine fieldsets, inlines, list_display, list_filter, search_fields property'lerini 
istediğimiz şekilde doldurduk. Bu şekilde admin panelinde Question modelimizin nasıl görüneceğini belirliyoruz.

	fieldsets -> Polls › Questions › Question sekmesinde question_text ve pub_date in nasıl duracağını belirler.
	inlines -> StackedInlines sınıfını implement eden sınıfı tanımlıyoruz.
	list_display -> Polls › Questions sekmesinde soru tablosunun kolonları belli olur.
	list_filter -> Polls › Questions sekmesinde sağ tarafta filter açar.
	search_fields -> İstenilen model'e göre arama çubuğu özelliği getirir.

25- Yine aynı şekilde Choice modelimizin nasıl görüneceğini belirlemek için de StackedInline sınıfını implement
ettiğimiz ChoiceInline sınıfını yazdık. (Not: StackedInline yerine başka TabularInline gibi sınıflar da mevcut.)

26- polls/models.py içerisinde Question sınıfına;

		was_published_recently.admin_order_field = 'pub_date'
    	was_published_recently.boolean = True
    	was_published_recently.short_description = 'Published recently?'
	
	kod parçalarını ekledik. Bu sayede admin panelimizde Questions sekmesinde daha detaylı arayüz elde ettik.

27- mysite/settings.py içerisindeki TEMPLATES property'sindeki 'DIR' field'ına kendi template'imizi tanımladık.
