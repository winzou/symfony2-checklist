Hata sayfalarını kişiselleştir
temel
Eğer geliştirme ortamındaki hata sayfalarına alıştıysanız, umalım ki üretim ortamındaki sitenizin ziyaretçileri aynı durum ile karşılaşmasın. Bu yüzden farklı hata sayfalarınızı kişiselleştirip, kendi düzeniniz ile entegre hale getirmelisiniz.

Hata sayfalarını kişiselleştirmek gerçekten kolay. View dosyaları`TwigBundle` bundle içinde bulunur, bu da size bunları sizinkiler ile ezmenize olanak sunar. Oluşturmanız gereken viewler: `Exception/errorXXX.html.twig`, buradaki `XXX` karşılaşılan hatanın numarasıdır. En azından 404 ve 500 hatalarını kişiselleştirmeniz önemle tavsiye edilir.

Kendi viewlerinizi kullanmanız için iki olası yol vardır:

1. `TwigBundle`'ı ezen yeni bir bundle oluşturabilir, ve viewlerinizi `Resources/views/Exception/errorXXX.html.twig` klasörü altına koyarsınız. Bu tekrar kullanılabilir bir bundle olacağı için farklı projelerinizde de kullanılabilmenizi sağlar;
2. Basitçe viewlerinizi `app/Resources/TwigBundle/views/Exception/errorXXX.html.twig` altına koyarsınız. Eğer viewleriniz bu projeye özgü ise sadece bu iş için yeni bir bundle oluşturmanıza gerek bırakmaz.

* _Bkz. [Hata mesajlarını kişiselleştirme, Symfony dokümantasyonu](http://symfony.com/doc/master/cookbook/controller/error_pages.html)_