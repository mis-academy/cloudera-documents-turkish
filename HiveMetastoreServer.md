#  Hive Metastore Server
Hive metastore servisi, Hive tabloları ve bölümleri için meta veriyi ilişkisel bir veritabanında depolar ve metastore servis API'sini kullanarak istemcilere bu bilgileri erişim (Hive dahil) sağlar. Bu sayfa, dağıtım seçeneklerini açıklar ve önerilen yapılandırmada bir veritabanı kurmak için yönergeler sağlar.

# Hive'a Giriş
Apache Hive, Hadoop dosyalarında saklanan büyük veri kümelerini sorgulamak ve analiz etmek için Hadoop Haused'ın üzerine kurulmuş açık kaynak kodlu bir veri ambarı sistemidir.
Hive temel olarak SQL ile rahat olan kullanıcılara yöneliktir. SQL'e benzer HiveQL (HQL) adlı kovan kullanım dili. HiveQL otomatik olarak SQL benzeri sorguları MapReduce işlerine dönüştürür.
Metastore, Apache Hive meta verilerinin merkezi deposudur. Hive tabloları için meta verileri (şemaları ve konumu gibi) ve ilişkisel bir veritabanındaki bölümleri depolar. Bu bilgiye metastore servis API'sini kullanarak istemci erişimi sağlar.

## **Hive metastore iki temel birimden oluşur:**
* Diğer Apache Hive hizmetlerine metastore erişimi sağlayan bir hizmet.
* HDFS depodan ayrı olan Hive meta verileri için disk depolama.

## Hive Metastore Modları

Hive Metastore dağıtımı için üç mod vardır:
* Gömülü Metastore (Embedded Metastore)
* Yerel Metastore (Local Metastore)
* Uzak Metastore (Remote Metastore)

### Embedded Metastore
* Gömülü mod, CDH için varsayılan metastore dağıtım modudur. Bu modda, metastore bir Derby veritabanı kullanır ve hem veritabanı hem de metastore servisi ana HiveServer işlemine gömülür. HiveServer işlemini başlattığınızda her ikisi de sizin için başlatılır.

### Local Metastore
* Yerel modda(lokal), Hive metastore hizmeti ana HiveServer işlemi ile aynı işlemde çalışır, ancak metastore veritabanı ayrı bir işlemde çalışır ve ayrı bir ana bilgisayar üzerinde olabilir. Gömülü metastore servisi, JDBC üzerinden metastore veritabanı ile iletişim kurar.

### Remote Metastore
* Uzak modda, Hive metastore servisi kendi JVM işleminde çalışır. HiveServer2, HCatalog, Impala ve diğer işlemler Thrift ağ API'sini (hive.metastore.uris özelliği kullanılarak yapılandırılmış) kullanarak iletişim kurar.Veritabanı, HiveServer işlemi ve metastore hizmeti aynı ana bilgisayarda olabilir, ancak HiveServer işleminin ayrı bir ana bilgisayarda çalıştırılması daha iyi kullanılabilirlik ve ölçeklenebilirlik sağlar.
Uzak modun localde asıl avantajı,remote modda yöneticinin her Hive kullanıcısı ile metastore veritabanı için JDBC oturum açma bilgilerini paylaşmasını gerektirmemesidir.
