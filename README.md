
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
Sunucu, simülasyonun kendisiyle ilgili her şeyden sorumludur: sensör oluşturma, fiziğin hesaplanması, dünya durumu ve aktörleri hakkında güncellemeler ve çok daha 
fazlası. Gerçekçi sonuçları hedeflediğinden, en uygun seçenek, özellikle makine öğrenimi ile uğraşırken sunucuyu özel bir GPU ile çalıştırmak olacaktır.
Müşteri tarafı, sahnedeki aktörlerin mantığını kontrol eden ve dünya koşullarını belirleyen bir dizi müşteri modülünden oluşur. Bu, sunucu ve istemci arasında 
aracılık eden ve yeni işlevler sağlamak için sürekli gelişen bir katman olan CARLA API'den (Python veya C ++) yararlanılarak elde edilir.

CARLA'yı anlamak bundan çok daha fazlasıdır, çünkü içinde birçok farklı özellik ve öğe bir arada bulunur. CARLA'nın neler başarabileceğine dair bakış açısı kazanmak 
için bunlardan bazıları aşağıda listelenmiştir.

* **Trafik Müdürü** Öğrenme için kullanılanın yanı sıra araçların kontrolünü ele alan yerleşik bir sistem. Gerçekçi davranışlarla kentsel benzeri ortamları yeniden 
yaratmak için CARLA tarafından sağlanan bir iletken görevi görür.

* **Sensörler** Araçlar, çevreleriyle ilgili bilgileri vermek için onlara güveniyor. CARLA'da, araca takılan belirli bir tür aktördür ve aldıkları veriler, süreci 
kolaylaştırmak için alınabilir ve saklanabilir. Şu anda proje, kameralardan radarlara, lidara ve çok daha fazlasına kadar bunların farklı türlerini 
desteklemektedir.

* **Recorder** Bu özellik, dünyadaki her oyuncu için bir simülasyonu adım adım yeniden canlandırmak için kullanılır. Dünyanın herhangi bir yerindeki zaman 
çizelgesindeki herhangi bir ana erişim sağlayarak harika bir izleme aracıdır.

* **ROS köprüsü ve Otomatik Yazılım uygulaması** Evrenselleştirme meselesi olarak, CARLA projesi düğümleri birbirine bağlar ve simülatörün diğer öğrenme 
ortamlarına entegrasyonu için çalışır.

* **Varlıkları aç** CARLA, hava koşullarını kontrol ederek kentsel ortamlar için farklı haritalar ve kullanılacak geniş bir aktör setine sahip bir plan kitaplığı 
sağlar. Ancak, bu öğeler özelleştirilebilir ve basit yönergeler izlenerek yenileri oluşturulabilir.

* **Senaryo koşucusu** CARLA, araçlar için öğrenme sürecini kolaylaştırmak amacıyla, farklı durumları açıklayan bir dizi rota sunar. Bunlar aynı zamanda herkesin 
çözümlerini test etmesi ve liderlik tablosuna girmesi için CARLA mücadelesinin temelini oluşturdu.


## Building CARLA » Linux build

<p align="center">
  <img src="https://user-images.githubusercontent.com/54184905/107883217-b1e11980-6efe-11eb-8742-b3f792d8e602.png" />
</p>

**Ubuntu Kurulumu için ilerleyiniz** [Link](https://ubuntu.com/download)

**Carla Ubuntu kurulumu için ilerleyiniz** [link](https://carla.readthedocs.io/en/latest/build_linux/)

**Cuda geliştirici kiti Ubuntu kurulumu için ilerleyiniz** [link](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu-installation)

**Carla Simulatoru Colab üzerinde çalıştırmak için ilerleyiniz** [link](https://colab.research.google.com/github/MichaelBosello/carla-colab/blob/master/carla-simulator.ipynb#scrollTo=w4Ywwr43AGR9)
