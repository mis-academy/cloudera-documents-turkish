# Impala Catalog Service

Katalog hizmeti olarak bilinen Impala bileşeni, Impala SQL ifadelerinden meta veri değişikliklerini bir kümedeki tüm Impala daemonlarına aktarır. Catalogd adlı bir daemon süreci ile fiziksel olarak temsil edilir; Sadece kümedeki bir ana bilgisayarda böyle bir sürece ihtiyacınız var. İstekler, statustore daemon'undan geçtiğinden, aynı ana bilgisayardaki statetored ve catalogd hizmetlerini çalıştırmak mantıklıdır.
