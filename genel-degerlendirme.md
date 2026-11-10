# Genel Değerlendirme

İncelenen üç CWE farklı güvenlik katmanlarındaki problemleri temsil etmektedir.

**CWE-78**, kullanıcı girdisinin işletim sistemi komutlarına güvenli olmayan şekilde dahil edilmesiyle ortaya çıkar ve yetkisiz komut çalıştırma riski oluşturur.

**CWE-319**, hassas bilgilerin şifrelenmemiş iletişim kanallarından gönderilmesiyle ortaya çıkar ve ağ trafiğinin izlenmesi sonucunda bilgilerin ele geçirilmesine neden olabilir.

**CWE-134** ise saldırgan tarafından kontrol edilen verinin format string olarak kullanılmasıyla ortaya çıkar ve özellikle düşük seviyeli dillerde bellek bilgilerinin açığa çıkması veya daha ciddi güvenlik problemleri oluşturabilir.

Bu üç zafiyetin ortak noktası, uygulama tarafından kontrol edilmesi gereken alanların dışarıdan gelen girdiler tarafından kontrol edilebilir hale gelmesidir. Bu nedenle güvenli yazılım geliştirme sürecinde **input validation, güvenli API kullanımı, uygun veri/komut ayrımı, güvenli iletişim ve minimum yetki prensibi** gibi temel güvenlik yaklaşımlarının uygulanması önemlidir.
