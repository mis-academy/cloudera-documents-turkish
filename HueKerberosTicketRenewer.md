#  Hue Kerberos Ticket Renewer
Hue'nin kimlik doğrulaması için Kerberos kullanan bir Cloudera kümesiyle düzgün çalışması için, Kerberos Bilet Yenilemesi(Hue Kerberos Ticket Renewer), Hue hizmetine eklenmelidir.

Cloudera Manager'da bir Kerberos Bilet Yenileme(Hue Kerberos Ticket Renewer) rol örneği ekleme:
 * Hue servisine gidin.
 * Örnekler sekmesini tıklayın.
 * Rol Örnekleri Ekle düğmesini tıklayın.
 * Kerberos Bilet Yenileme rolünü, Hue sunucusuyla aynı ana bilgisayara atayın.
 * Sihirbaz durumu bittiğinde, Kerberos Bilet Yenileme rol örneği yapılandırılır. Hue hizmeti artık güvenli Hadoop kümesiyle çalışır.
 * Her bir Hue Sunucusu rolü için bu adımları tekrarlayın.
 
Eğer Hue Kerberos Ticket Renewer tekrar başlamıyorsa **Kerberos Key Distribution Center** konfigürasyon dosyasını kontrol edin.
