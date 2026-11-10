# CWE-134 – Use of Externally-Controlled Format String

### CWE-134 Nedir?

CWE-134, saldırgan tarafından kontrol edilebilen bir değerin format string olarak kullanılması sonucunda ortaya çıkan bir güvenlik zafiyetidir.

Format string, özellikle C ve C++ gibi programlama dillerinde `printf`, `fprintf`, `sprintf` ve benzeri fonksiyonlarda çıktının nasıl biçimlendirileceğini belirleyen özel ifadeleri içerir.

Örneğin format string içerisinde kullanılan `%s`, `%d`, `%x` gibi ifadeler fonksiyona verilen verilerin nasıl yorumlanacağını belirler.

Problem, bu formatın uygulama tarafından sabit olarak belirlenmesi gerekirken saldırgan tarafından kontrol edilebilir hale gelmesidir.

### Nasıl Oluşur?

Güvenli bir yaklaşımda format string uygulama tarafından belirlenir ve kullanıcı girdisi yalnızca veri olarak kullanılır.

Örneğin mantıksal olarak:

**Uygulama tarafından belirlenen format + Kullanıcı verisi**

şeklinde bir yapı güvenlidir.

Riskli yaklaşımda ise:

**Kullanıcı verisi → Format String**

şeklinde doğrudan kullanım gerçekleşir.

Bu durumda saldırgan format belirteçleri kullanarak uygulamanın normalde gerçekleştirmeyeceği işlemleri tetiklemeye çalışabilir.

Özellikle C/C++ gibi bellek yönetiminin geliştirici tarafından kontrol edildiği dillerde bu durum daha ciddi sonuçlara yol açabilir.

### Güvenlik Riski

CWE-134'ün oluşturabileceği risk, kullanılan programlama dili ve fonksiyonun davranışına göre değişebilir.

Olası sonuçlar arasında:

* Bellekte bulunan bilgilerin okunması,
* Hassas bilgilerin açığa çıkması,
* Uygulamanın beklenmedik şekilde çalışması,
* Uygulamanın çökmesi,
* Bellekte belirli değerlerin değiştirilmesi,
* Bazı durumlarda yetkisiz kod çalıştırılması

bulunabilir.

Özellikle saldırganın format string üzerinde tam kontrol sahibi olduğu durumlarda zafiyet ciddi bir güvenlik problemine dönüşebilir.

### Nasıl Önlenir?

En temel önlem, kullanıcı tarafından kontrol edilen değerlerin hiçbir zaman doğrudan format string olarak kullanılmamasıdır.

Format string uygulama tarafından sabit olarak belirlenmeli ve dışarıdan gelen değerler yalnızca veri olarak aktarılmalıdır.

Bunun yanında:

* Güvenli string formatting yöntemleri kullanılmalıdır.
* Kullanıcı girdileri doğrudan format parametresi olarak geçirilmemelidir.
* C/C++ gibi dillerde `printf` ailesindeki fonksiyonların kullanımı dikkatli yapılmalıdır.
* Derleyici uyarıları ve güvenlik kontrolleri etkinleştirilmelidir.
* Statik analiz araçları kullanılarak format string kullanımları kontrol edilmelidir.
* Kullanıcı tarafından kontrol edilen girdilerin uygulama içerisinde hangi fonksiyonlara aktarıldığı takip edilmelidir.

Güvenli yaklaşımın temel mantığı, **formatın uygulama tarafından, verinin ise dış kaynaktan gelmesi** şeklinde iki kavramı birbirinden ayırmaktır.

### Özet

CWE-134'ün temelinde **saldırgan tarafından kontrol edilen bir verinin format talimatı olarak yorumlanması** problemi bulunur.

Format string uygulama tarafından kontrol edildiğinde kullanıcı girdisi yalnızca veri olarak değerlendirilir ve saldırganın formatlama mekanizmasını değiştirmesi engellenir.
