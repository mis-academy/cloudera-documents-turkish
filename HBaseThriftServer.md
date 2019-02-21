# HBase Thrift Server

HBase Thrift Server sağlık testi, kullanılan dosya tanımlayıcılarının sayısının, HBase Thrift Server dosya tanımlayıcı sınırının üzerine çıkıp çıkmadığını kontrol eder.
Bu test, Dosya Tanımlayıcısı İzleme Eşikleri(**File Descriptor Monitoring Thresholds**) HBase Thrift Server izleme ayarı kullanılarak yapılandırılabilir.

* Default Value	critical:70.0, warning:50.0

# HBase Thrift Server Heap Dump Directory Free Space
HBase Thrift Server sağlık testi, bu HBase Thrift Server'ın yığın dökümü dizinini içeren dosya sisteminin yeterli boş alana sahip olduğunu kontrol eder
Bu test Heap Dump Directory Free Space Monitoring Absolute Thresholds ve Heap Dump Directory Free Space Monitoring Percentage Thresholds HBase Thrift Server monitoring ayarları kullanılarak yapılandırılabilir.

* **Heap Dump Directory Free Space Monitoring Absolute Thresholds** : Bu rolün yığın dökümü dizinini içeren dosya sistemindeki boş alanın izlenmesi için sağlık testi eşiğidir.
* **Heap Dump Directory Free Space Monitoring Percentage Thresholds** : Bu rolün yığın dökümü dizinini içeren dosya sistemindeki boş alanın izlenmesi için sağlık testi eşiğidir. Bu dosya sistemindeki kapasitenin yüzdesi olarak belirtilir. Yığın Dökümü Dizin Boş Alan İzlemesi Mutlak Eşikleri ayarı yapılandırılmışsa, bu ayar kullanılmaz.

# HBase Thrift Server Host Health
Bu testin başarısız olması, HBase Thrift Server'ı çalıştıran sunucunun bir sorun yaşadığı anlamına gelir. Daha fazla ayrıntı için host durum sayfasına bakın. Bu test, HBase Thrift Server Host Health, HBase Thrift Server izleme ayarını kullanarak etkinleştirilebilir veya devre dışı bırakılabilir.

# HBase Thrift Server Process Status
Bu HBase Thrift Server sağlık testi, HBase Thrift Server ana bilgisayarındaki Cloudera Manager Agent'ın doğru bir şekilde kalp atışı(heart beating çalışıyor mu çalışmıyor mu özetle) olduğunu ve HBase Thrift Server rolüyle ilişkili işlemin Cloudera Manager tarafından beklenen durumda olduğunu kontrol eder.

# HBase Thrift Server Swap Memory Usage

Bu HBase Thrift Server sağlık testi, rol tarafından kullanılan swap belleğinin miktarını kontrol eder. Bu sağlık testinde başarısızlık, makinenizin aşırı yüklendiğini gösterebilir.
Konfigürasyonu için Process Swap Memory Thresholds monitoring.
