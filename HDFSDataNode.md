# HDFS DataNode

DataNode, [HadoopFileSystem] dosyasında veri depolar.Fonksiyonel bir dosyasisteminde birden fazla DataNode bulundurur ve veriler arasında çoğaltılır(replicated).

DataNode NameNode'a bağlanır.Bu server'a ulaşana kadar sürer daha sonra dosya sistemleri için namenode isteklere yanıt verir.

NameNode verileri sağladıktan sonra clientlar direk olarak datanode ile iletişim haline geçerler.Buna benzer örnek ise

MapReduse TaskTracker verilebilir.

DataNode örnekleri birbirleriyle konuşabilir, veriyi çoğaltırken(replicated) yaptıkları şey budur.

Genellikle DataNode verileri için RAID depolaması kullanılmasına gerek yoktur, çünkü veriler aynı sunucudaki birden çok disk yerine birden çok sunucuda çoğaltılmak üzere tasarlanmıştır.

Bir sunucunun DataNode'a, bir TaskTracker'a ve CPU başına bir TaskTracker'a sahip olması ideal bir yapılandırmadır.Bu,her TaskTracker'ın bir CPU'nun% 100'üne ve ayrı disklere veri okuma ve yazma olanağı sağlayacaktır.
