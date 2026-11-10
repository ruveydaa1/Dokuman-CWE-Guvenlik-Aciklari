# CWE-78 – OS Command Injection

### CWE-78 Nedir?

CWE-78, uygulamanın dışarıdan aldığı verileri işletim sistemi komutlarına güvenli olmayan bir şekilde dahil etmesi sonucunda ortaya çıkan bir güvenlik zafiyetidir.

Bir uygulamanın işletim sistemi üzerinde bir komut çalıştırması gerektiğinde, bu komuta kullanıcıdan veya başka bir dış kaynaktan gelen verilerin eklenmesi gerekebilir. Eğer bu veriler yeterince doğrulanmadan veya güvenli şekilde parametrelenmeden komut içerisinde kullanılırsa saldırgan, uygulamanın çalıştırdığı komutu değiştirebilir.

Bu durum **OS Command Injection** olarak adlandırılır.

Buradaki temel problem, uygulamanın yalnızca kendi çalıştırmak istediği komutu çalıştırması gerekirken saldırgan tarafından sağlanan girdinin de komutun bir parçası haline gelmesidir.

### Nasıl Oluşur?

Bu güvenlik açığı genellikle aşağıdaki akış sonucunda ortaya çıkar:

1. Uygulama dışarıdan bir veri alır.
2. Bu veri bir işletim sistemi komutunda kullanılmak üzere hazırlanır.
3. Kullanıcı girdisi yeterli doğrulama yapılmadan komuta eklenir.
4. Uygulama oluşturulan komutu işletim sisteminde çalıştırır.
5. Saldırgan, özel karakterler veya komut ifadeleri kullanarak çalıştırılan komutun davranışını değiştirebilir.

Örneğin bir uygulamanın kullanıcıdan aldığı bir dosya adını doğrudan işletim sistemi komutuna eklediği düşünülürse, saldırgan dosya adı alanını yalnızca geçerli bir dosya adı olacak şekilde kullanmak yerine komutun yapısını değiştirecek bir değer gönderebilir.

Bu nedenle yalnızca kullanıcı girdisinin "beklenen formatta" görünmesi yeterli olmayabilir. Girdinin hangi bağlamda kullanıldığı da önemlidir.

### Güvenlik Riski

CWE-78'in en önemli riski, saldırganın uygulamanın çalıştığı sistem üzerinde yetkisiz komutlar çalıştırabilmesidir.

Başarılı bir saldırı sonucunda saldırgan:

* Sistem üzerindeki dosyaları okuyabilir.
* Dosyaları değiştirebilir veya silebilir.
* Sistem hakkında bilgi toplayabilir.
* Uygulamanın kullandığı servisleri etkileyebilir.
* Ortam değişkenleri veya yapılandırma dosyaları gibi hassas bilgileri elde edebilir.
* Uygulamanın sahip olduğu yetkiler doğrultusunda daha ileri saldırılar gerçekleştirebilir.

Açığın etkisi büyük ölçüde uygulamanın hangi kullanıcı yetkileriyle çalıştığına bağlıdır. Uygulama yüksek sistem yetkileriyle çalışıyorsa aynı zafiyetin oluşturabileceği zarar da önemli ölçüde artar.

### Nasıl Önlenir?

CWE-78'i önlemenin en güvenli yolu, mümkün olduğu durumlarda işletim sistemi komutlarını doğrudan çalıştırmaktan kaçınmaktır. Yapılması gereken işlem için güvenli bir kütüphane veya API mevcutsa bu yöntem tercih edilmelidir.

İşletim sistemi komutu çalıştırılması zorunluysa:

* Kullanıcı girdileri doğrudan komut satırına eklenmemelidir.
* Güvenli API ve parametreleme yöntemleri kullanılmalıdır.
* Girdiler beklenen format açısından doğrulanmalıdır.
* İzin verilen değerler mümkün olduğunca sınırlandırılmalıdır.
* Shell üzerinden komut çalıştırılması gerekiyorsa özel karakterlerin komut yapısını değiştirmesi engellenmelidir.
* Uygulama mümkün olan en düşük işletim sistemi yetkileriyle çalıştırılmalıdır.

Burada önemli olan yalnızca belirli karakterleri filtrelemek değil, kullanıcı girdisinin komut olarak yorumlanmasını tamamen engelleyecek güvenli bir tasarım kullanmaktır.

### Özet

CWE-78'in temelinde **veri ile komutun birbirinden yeterince ayrılmaması** problemi bulunur. Kullanıcı tarafından kontrol edilen bir değer işletim sistemi tarafından çalıştırılacak komutun parçası haline geldiğinde saldırganın komutun davranışını değiştirme ihtimali ortaya çıkar.

Bu nedenle özellikle sistem komutları çalıştıran uygulamalarda güvenli parametreleme, input validation ve minimum yetki prensibi uygulanmalıdır.
