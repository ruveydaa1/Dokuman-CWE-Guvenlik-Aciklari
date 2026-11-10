# CWE-319 – Cleartext Transmission of Sensitive Information

### CWE-319 Nedir?

CWE-319, hassas bilgilerin güvenli olmayan ve şifreleme sağlamayan bir iletişim kanalı üzerinden gönderilmesi durumunu ifade eder.

Bir uygulama kullanıcı adı, parola, erişim token'ı, oturum bilgisi veya başka hassas veriler gönderiyorsa bu verilerin aktarım sırasında korunması gerekir.

Veriler şifrelenmeden gönderildiğinde, iletişim kanalını izleyebilen bir saldırgan bu bilgileri okuyabilir veya ele geçirebilir.

Bu nedenle CWE-319 özellikle ağ üzerinden çalışan web uygulamalarında önemli bir güvenlik problemidir.

### Nasıl Oluşur?

CWE-319 genellikle güvenli iletişim protokolünün kullanılmaması sonucunda oluşur.

Örneğin bir web uygulamasının hassas bilgileri:

**HTTP → Sunucu**

şeklinde şifrelenmemiş bir bağlantı üzerinden göndermesi risk oluşturur.

Bunun yerine hassas verilerin aktarımı:

**HTTPS → TLS ile şifrelenmiş bağlantı → Sunucu**

üzerinden gerçekleştirilmelidir.

CWE-319 yalnızca parolalarla sınırlı değildir. Aşağıdaki bilgiler de hassas veri olarak değerlendirilebilir:

* Kullanıcı adı ve parola
* Authentication token
* Session bilgileri
* API anahtarları
* Kişisel bilgiler
* Finansal bilgiler
* Gizli uygulama verileri

### Güvenlik Riski

Hassas bilgilerin cleartext olarak aktarılması durumunda saldırgan, ağ trafiğini izleyerek bu bilgileri elde edebilir.

Örneğin bir kullanıcının giriş bilgilerinin şifrelenmemiş bir bağlantı üzerinden gönderildiğini düşünelim. Saldırgan ağ trafiğini görebiliyorsa kullanıcı adı ve parolayı doğrudan elde edebilir.

Bu durum:

* Kullanıcı hesaplarının ele geçirilmesine,
* Oturumların kötüye kullanılmasına,
* Authentication tokenlarının çalınmasına,
* Hassas kişisel verilerin açığa çıkmasına,
* Yetkisiz sistem erişimine

neden olabilir.

Özellikle ortak Wi-Fi ağları, güvenilmeyen ağlar veya saldırganın ağ trafiğine erişebildiği ortamlarda risk daha yüksektir.

### Nasıl Önlenir?

CWE-319'u önlemek için hassas verilerin aktarımında **HTTPS/TLS** kullanılmalıdır.

Uygulanabilecek temel önlemler şunlardır:

* Web uygulamalarında HTTPS kullanılmalıdır.
* HTTP bağlantıları mümkün olduğunca HTTPS'e yönlendirilmelidir.
* TLS yapılandırması güncel ve güvenli protokolleri kullanmalıdır.
* Geçersiz veya güvenilmeyen sertifikalar kabul edilmemelidir.
* Hassas bilgiler URL parametrelerinde gönderilmemelidir.
* Authentication bilgilerinin güvenli şekilde taşınması sağlanmalıdır.
* Cookie kullanılıyorsa `Secure` özelliği etkinleştirilmelidir.
* Oturum bilgilerinin istemci ve sunucu arasında güvenli şekilde aktarılması sağlanmalıdır.

HTTPS kullanımı yalnızca parolaların korunmasını sağlamaz; istemci ile sunucu arasındaki iletişimin bütünlüğünün ve gizliliğinin korunmasına da yardımcı olur.

### Özet

CWE-319'un temel problemi, **hassas bilgilerin aktarım sırasında korunmamasıdır**.

Bir uygulama güvenli bir şekilde çalışsa bile ağ üzerinden gönderilen bilgiler şifrelenmiyorsa saldırgan tarafından ele geçirilebilir. Bu nedenle hassas verilerin bulunduğu tüm iletişimlerde HTTPS/TLS kullanılması temel güvenlik gereksinimlerinden biridir.
