# CARLA Simulator

<p align="center">
  <img src="https://user-images.githubusercontent.com/54184905/107882265-5f512e80-6ef9-11eb-8c12-9b44579a69cc.jpg" />
</p>

CARLA, açık kaynaklı bir otonom sürüş simülatörüdür. Otonom sürüş problemiyle ilgili bir dizi görevi ele almak için modüler ve esnek bir API olarak hizmet vermek 
üzere sıfırdan oluşturuldu. CARLA'nın ana hedeflerinden biri, kullanıcılar tarafından kolayca erişilebilen ve özelleştirilebilen bir araç olarak hizmet veren otonom 
sürüş Ar-Ge'sini demokratikleştirmeye yardımcı olmaktır. Bunu yapmak için, simülatörün, genel sürüş problemi (örneğin, sürüş politikalarını öğrenmek, eğitim 
algılama algoritmaları, vb.) Dahilindeki farklı kullanım durumlarının gereksinimlerini karşılaması gerekir. CARLA simülasyonu Unreal Engine üzerine kurulmuştur, 
yolları ve kentsel ayarları tanımlamak için OpenDRIVE standardını (bugünkü 1.4) kullanır. Simülasyon üzerinde kontrol, proje yaptıkça sürekli büyüyen Python ve C ++ 
'da ele alınan bir API aracılığıyla sağlanır.

<p align="center">
  <img src="https://user-images.githubusercontent.com/54184905/107882385-059d3400-6efa-11eb-9935-30e216bed0e6.png" />
</p>

CARLA simülatörü, ölçeklenebilir bir istemci-sunucu mimarisinden oluşur.
Sunucu, simülasyonun kendisiyle ilgili her şeyden sorumludur: sensör oluşturma, fiziğin hesaplanması, dünya durumu ve aktörleri hakkında güncellemeler ve çok daha fazlası. Gerçekçi sonuçları hedeflediğinden, en uygun seçenek, özellikle makine öğrenimi ile uğraşırken sunucuyu özel bir GPU ile çalıştırmak olacaktır.
Müşteri tarafı, sahnedeki aktörlerin mantığını kontrol eden ve dünya koşullarını belirleyen bir dizi müşteri modülünden oluşur. Bu, sunucu ve istemci arasında aracılık eden ve yeni işlevler sağlamak için sürekli gelişen bir katman olan CARLA API'den (Python veya C ++) yararlanılarak elde edilir.

