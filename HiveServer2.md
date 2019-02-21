# HiveServer2
HiveServer2 (HS2), istemcilerin Hive'ye karşı sorguları yürütmesini sağlayan bir hizmettir. HiveServer2, kullanımdan kaldırılmış olan HiveServer1'in başka bir versiyonudur. HS2, çoklu istemci eşzamanlılığını ve kimlik doğrulamasını destekler. JDBC ve ODBC gibi açık API istemcileri için daha iyi destek sağlamak üzere tasarlanmıştır.
HS2, Thrift tabanlı Hive servisini (TCP veya HTTP) ve web kullanıcı arayüzü için bir Jetty web sunucusunu içeren bir karma hizmet olarak çalışan tek bir işlemdir.

## HS2(HiveServer2) Mimarisi
Thrift tabanlı Hive servisi HS2'nin çekirdeğini oluşturur ve Hive sorgularına (örn. Beeline'dan) hizmet etmekten sorumludur. Thrift, çapraz platform hizmetleri oluşturmak için bir RPC çerçevesidir. Yığın 4 katmandan oluşur: Sunucu, Aktarım, Protokol ve İşlemci.( Server, Transport, Protocol ve Processor)

### Server
HS2, TCP modu için bir TThreadPoolServer (Thrift'ten) veya HTTP modu için bir Jetty sunucusu kullanır.TThreadPoolServer, TCP bağlantısı başına bir çalışan iş parçacığı ayırır. Her iş parçacığı, bağlantı boşta olsa bile her zaman bir bağlantıyla ilişkilendirilir. Dolayısıyla, çok sayıda eşzamanlı bağlantı nedeniyle çok sayıda iş parçacığı nedeniyle ortaya çıkan potansiyel bir performans sorunu vardır. Gelecekte HS2, TCP modu için başka bir sunucu tipine geçebilir, örneğin TThreadedSelectorServer.
### Transport
İstemci ve sunucu arasında bir proxy gerektiğinde HTTP modu gereklidir (örneğin, yük dengeleme veya güvenlik nedenleriyle). Bu yüzden, TCP modunun yanı sıra desteklenmektedir.
### Protocol
Protokol uygulaması, serileştirme ve serileştirme işlemlerinden sorumludur. HS2 şu anda serileştirme için Thrift protokolü olarak TBinaryProtocol kullanıyor.
### Processor
Süreç uygulama istekleri işlemek için uygulama mantığı( logic to handle requests). Örneğin, ThriftCLIService.ExecuteStatement () yöntemi, bir Kovan sorgusunu derlemek ve yürütmek için mantığı uygular.

# HS2(HiveServer2) Bağımlılıkları
### Metastore
* Metastore gömülü (HiveServer2 ile aynı süreçte) veya uzak bir sunucu (Thrift tabanlı servis de olan) olarak yapılandırılabilir. HS2, sorgu derlemesi için gereken meta veriler için metastore ile iletişim kurulur.

### Hadoop cluster
* HS2(HiveServer2), çeşitli yürütme motorları (MapReduce / Tez / Spark) için fiziksel yürütme planları hazırlar ve işleri yürütmek için Hadoop kümesine gönderir.

# JDBC Client
İstemci tarafının HS2 ile etkileşime girmesi için JDBC sürücüsü önerilir. Thrift istemcisinin doğrudan kullanıldığı ve JDBC'nin atlandığı bazı kullanım durumlarının (ör. Hadoop Hue) olduğunu unutmayın.
##  ilk sorguyu yapmak için bir dizi API çağrısı var:
* JDBC istemcisi (ör. Beeline), bir SessionHandle almak için bir OpenSession API çağrısı ve ardından bir taşıma bağlantısı (ör. TCP bağlantısı) başlatarak bir HiveConnection oluşturur. Oturum, sunucu tarafında oluşturulur.
* HiveStatement yürütülür (JDBC standartlarını izler) ve Thrift istemcisinden bir ExecuteStatement API çağrısı yapılır. API çağrısında, SessionHandle bilgileri, sorgu bilgileriyle birlikte sunucuya iletilir.
* HS2 sunucusu isteği alır ve sorgu ayrıştırma ve derleme için sürücüyü sorar. Sürücü, Hadoop ile konuşacak bir arkaplan işi başlatıyor ve hemen müşteriye bir cevap veriyor.
* Istemci, sorgu yürütme durumunu yoklaması ve HS2 ile konuşması için OperationHandle kullanır.
