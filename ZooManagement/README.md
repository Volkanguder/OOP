# Hayvanat Bahçesi Yönetimi

&emsp; Bir hayvanat bahçesindeki hayvanlar hakkındaki bilgileri takip etmek için bir sistem tasarlıyoruz.

- Hayvanlar:
- Atlar (atlar, zebralar, eşekler vb.),
- Kedigiller (kaplanlar, aslanlar vb.),
- Kemirgenler (sıçanlar, kunduzlar vb.) gibi gruplardaki türlerle karakterize edilir.
- Hayvanlar hakkında depolanan bilgilerin çoğu tüm gruplamalar için aynıdır.
- tür adı, ağırlığı, yaşı vb.
- Sistem ayrıca her hayvan için belirli ilaçların dozajını alabilmeli => getDosage ()
- Sistem Yem verme zamanlarını hesaplayabilmelidir => getFeedSchedule ()

&emsp; Sistemin bu işlevleri yerine getirme mantığı, her gruplama için farklı olacaktır. Örneğin, atlar için yem verme algoritması farklı olup, kaplanlar için farklı olacaktır.

&emsp; Polimorfizm modelini kullanarak, yukarıda açıklanan durumu ele almak için bir sınıf diyagramı tasarlayalım.



# Zoo Management

&emsp; We are designing a system to track information about animals in a zoo.

- Animals:
- They are characterized by species in groups such as Horses (horses, zebras, donkeys, etc.), Felids (tigers, lions, etc.), and Rodents (rats, beavers, etc.).
- Most of the stored information about the animals is the same for all groups.
- Species name, weight, age, etc.
- The system should also be able to retrieve the dosage of specific medications for each animal => getDosage()
- The system should be able to calculate feeding schedules => getFeedSchedule()

&emsp; The logic for performing these functions in the system will be different for each group. For example, the feeding algorithm for horses will be different from that of tigers.

&emsp; Using the polymorphism model, let's design a class diagram to address the situation described above.

