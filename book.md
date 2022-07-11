## Head First Java, 3rd Edition Notları
### Chapter 16. Saving Objects (and Text): Serialization and File I/O

![image](https://user-images.githubusercontent.com/95742539/178163742-78b94997-a51c-4bc3-9fd1-c06117aa48ba.png)

Java I/O API destinations ve sources ları temsil eden (files, network sockets vs...) connection stream lere sahiptir.
Çoğu zaman işe yarar birşey ortaya çıkarmak için iki akış (stream) gerekir. Biri connection u temsil etmek için diğeri ise metotları çağırmak için.
  -  Çünkü connection stream ler genellikle low-leveldir.
Mesela FileOutputStream byte yazıyor ama biz nesne yazmak istiyoruz. O yüzden daha yüksek seviyeli bir stream ile zincir oluşturuyoruz.
  - Peki neden ikisini de aynı anda yapan bir akış (stream) yok ?
**Çünkü OO ya göre düşünürsek her sınıf tek bir işi yapar** FileOutputStreams, bir dosyaya bayt yazar. ObjectOutputStreams, nesneleri bir akışa yazılabilen verilere dönüştürür.

![image](https://user-images.githubusercontent.com/95742539/178163730-029aab0c-4e2a-473a-8b15-2ad8cbdf4580.png)

## Nesneler serileştirilince ne olur ?
Serileştirilmiş nesneler, eşdeğer bir instance ın (nesnenin) heap üzerinde hayata döndürülebilmesi için instance değişkenlerinin değerlerini kaydeder.

![image](https://user-images.githubusercontent.com/95742539/178163947-8aacd133-35f4-4e31-a845-9cefab2dbf53.png)

- Class ını serileştirmek istiyorsan Serializable interface ini implemente etmelisin. Bu interface **marker** veya **tag** interface olarak geçer. Çünkü **bu interface bünyesinde imlemente edebileceğin metot bulundurmaz.** Tek amacı, onu uygulayan sınıfın serileştirilebilir olduğunu duyurmaktır. Bir sınıfın herhangi bir üst sınıfı serileştirilebilirse, alt sınıf da serileştirilebilir. Bunu açıkça beyan etmese bile alt sınıf otomatik olarak serileştirilebilir. (Arayüzler her zaman böyle çalışır. Üst sınıfınız “IS-A” Serileştirilebilirse, siz de öylesiniz.)

![image](https://user-images.githubusercontent.com/95742539/178164736-0169f65e-ccf8-407e-b120-dce79afcf885.png)

### Nesnenin bir kısmı düzgün kaydedilmezse ne olur ?

Ya tam haliyle nesneyi serileştirebilirsiniz ya da hiç serileştirme yapamazsınız. Örneğin bir Pond (Gölet) nesneniz var ve bunu serileştirmek istiyorsunuz. İçerisindeki Duck (Örnek) nesnesi serileşebilir bir nesne değilse işlem başarısız olur.

![image](https://user-images.githubusercontent.com/95742539/178164947-611fd37c-14ef-4f82-9243-fef5d646a6cf.png)

- Bir örnek değişkeni kaydedilemiyorsa (veya kaydedilmemesi gerekiyorsa) **Transient** olarak işaretleyin.
Bir örnek değişkenin serileştirme işlemi tarafından atlanmasını istiyorsanız, değişkeni **transient** anahtar sözcüğüyle işaretleyin.**

![image](https://user-images.githubusercontent.com/95742539/178165040-e4a4b03d-6fc2-45c2-a82c-bfb915503cf2.png)
Peki neden bir nesne serileştirilemez ? Çünkü developer o sınıfı serileştirilebilir hale getirmeyi unutmuş ya da serileştirilmesi istenmiyor olabilir. Mesela Java Class Library de bulunan çoğu şey(network connections, threads, or file objects) serileştirilemez. (Runtime a özgüdür) Başka bir deyişle, belirli bir platformda, belirli bir JVM'de programınızın belirli bir çalışmasına özgü bir şekilde somutlaştırılırlar. **Program kapandığında, bu şeyleri anlamlı bir şekilde hayata döndürmenin hiçbir yolu yoktur; her seferinde sıfırdan oluşturulmaları gerekir.**

## Deserialization: restoring an object

![image](https://user-images.githubusercontent.com/95742539/178170362-06f14cda-8db6-435f-9630-e69486c1cad7.png)

![image](https://user-images.githubusercontent.com/95742539/178170372-8bca9d2c-58be-4795-a8b2-3660e832ec2c.png)

Bir nesne deserialized edildiği zaman, JVM, serileştirilmiş nesnenin seri hale getirildiği sırada sahip olduğu aynı duruma(state) sahip heap üzerinde yeni bir nesne oluşturarak nesneyi hayata döndürmeye çalışır. Null (nesne referansları için) ya da varsayılan ilkel değerler olarak geri gelen geçici değişkenler dışında.

![image](https://user-images.githubusercontent.com/95742539/178170595-38321767-8b24-46c7-84ea-49231de3a6e0.png)








