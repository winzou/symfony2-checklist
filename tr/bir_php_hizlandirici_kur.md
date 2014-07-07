Bir PHP hızlandırıcı kur
performans
Symfony2 esnek ve güçlü bir çatıdır... bu oldukça yavaş bağlantı sürelerine sebep olur. Tabii ki üretim ortamı geliştirme ortamına göre çok daha hızlıdır, ama bu yeterli değil.

Uygulamanızı üretim ortamında hızlandırmak için, APC gibi bir PHP Hızlandırıcı kurmanız şiddetle tavsiye edilir.

### Özel sunuculara

#### Linuxte
APC'yi Debian türevi dağıtımlara kurmak için, basitçe şu komutu çalıştırın:

    apt-get install php-apc

Komutu dağıtımınıza göre adapte edin.

#### Windowsta
`php.ini`deki ilgili satırı yorumdan çıkarın:

    extension=php_apc.dll

#### Tüm durumlarda
Kurulum sonrasında eklentiyi aktive etmeniz gerekir. Bu `php.ini` sonuna şu satırı ekleyerek yapılır:

    [APC]
    apc.enabled=1

### Paylaşımlı hostinglerde
Paylaşımlı hostinglerde kurulum için ssh erişimi gereklidir. Bu durumda en iyisi yönetici ile irtibata geçmektir. Ona PHP hızlandırıcı yüklemenin serverlar için iyi olduğunu söyleyin.

* _Bkz. [APC PHP doc](http://php.net/manual/en/book.apc.php)_