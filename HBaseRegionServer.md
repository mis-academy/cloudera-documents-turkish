#  HBase RegionServer
HBase, HDFS'nin üstünde düşük gecikmeli rastgele okuma ve yazma sağlayan ve petabaytlarca veriyi işleyebilen Hadoop depolama yöneticisidir.
HBase'deki ilginç özelliklerden biri, auto-sharding'dir; bu, tabloların çok büyük olduklarında sistem tarafından dinamik olarak dağıtıldığı anlamına gelir.
HBase'de yatay ölçeklenebilirliğin temel birimi, Region olarak adlandırılır. Region, tablonun verilerinin bir alt kümesidir ve temel olarak, birlikte depolanan bitişik, sıralı bir dizi satırdır.
HBase'de köleler(slaves) Bölge Sunucuları(RegionServer) olarak adlandırılır. Her Bölge Sunucusu(RegionServer) bir dizi bölgeye(Region) hizmet vermekten sorumludur ve bir Bölge(Region) (yani satır aralığı) yalnızca bir Bölge Sunucusu(Region Server) tarafından sunulabilir.
HBase mimarisinin iki ana hizmeti vardır: kümeyi koordine etmekten ve yönetim işlemlerini yürütmekten sorumlu olan HMaster ve tablo verilerinin bir alt kümesini işlemekten sorumlu HRegionServer.

# HMaster, Region Assignment, ve Balancing
Bir Bölge Sunucusu bir veya daha fazla Bölgeye hizmet verebilir. Her Bölge başlangıçta bir Bölge Sunucusuna atanır ve master, bir Bölgeyi bir Yük Dengesi işleminin sonucu olarak bir Bölge Sunucusundan diğerine taşımayı seçebilir.
Bölgeler ve Bölge Sunucularının haritalandırılması META adı verilen bir sistem tablosunda tutulur.META'yı okuyarak, anahtarınız için hangi bölgenin sorumlu olduğunu belirleyebilirsiniz.Bu, okuma ve yazma işlemleri için, master'ın hiçbir şekilde dahil olmadığı ve istemcilerin talep edilen verilere hizmet vermekten sorumlu Bölge Sunucusuna doğrudan gidebileceği anlamına gelir.

# Client API'sı: Master ve Bölgeler Sorumlulukları
**HBaseAdmin** tabloları oluşturarak / silerek / değiştirerek “tablo şeması” ile etkileşime izin verir ve bölgeleri birleştirerek / atama yaparak, bölgeleri bir araya getirerek, bir temizleme(flush) çağrısı oluşturur. Bu arayüz Master ile iletişim kurar.
**HTable**, istemcinin belirli bir tablonun verilerini get, put, delete ve diğer tüm veri işlemlerini kullanarak işlemesine izin verir. Bu arabirim, istenen anahtar kümesini işlemek için sorumlu Bölge Sunucuları ile doğrudan iletişim kurar.

Bu iki arabirimin ayrı sorumlulukları vardır: HBaseAdmin yalnızca yönetici işlemlerini yürütmek ve Master ile iletişim kurmak için kullanılırken, HTable verileri işlemek ve Bölgelerle iletişim kurmak için kullanılır.
