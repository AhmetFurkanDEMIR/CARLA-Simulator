
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
istemci tarafı, sahnedeki aktörlerin mantığını kontrol eden ve dünya koşullarını belirleyen bir dizi müşteri modülünden oluşur. Bu, sunucu ve istemci arasında 
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

**Carla Simulatoru Colab üzerinde çalıştırmak için ilerleyiniz** [link](https://lnkd.in/dtzWR3S)


## Adımlar

Aşağıdaki adımlar ile Carla Simulator 'u daha detaylıca inceleyip öğrenecğiz :).

<p align="center">
  <img src="https://carla.org/img/posts/2020-31-07/lidar_raycast.gif" />
</p>

### Dünya ve istemci

<p align="center">
  <img src="https://user-images.githubusercontent.com/54184905/108078591-ebd92980-707e-11eb-987b-cf989541f2b8.gif" />
</p>

İstemci, kullanıcının simülasyonda bilgi veya değişiklik istemek için çalıştırdığı modüldür. Bir istemci bir IP ve belirli bir bağlantı noktası ile çalışır. 
Sunucuyla terminal üzerinden iletişim kurar. Aynı anda çalışan birçok müşteri olabilir. Gelişmiş çok istemci yönetimi, CARLA ve senkronizasyonun tam olarak 
anlaşılmasını gerektirir.

Dünya, simülasyonu temsil eden bir nesnedir. Oyuncuları ortaya çıkarmak, havayı değiştirmek, dünyanın mevcut durumunu elde etmek vb. İçin ana yöntemleri içeren 
soyut bir katman görevi görür. Simülasyon başına yalnızca bir dünya vardır. Harita değiştirildiğinde yok edilecek ve yenisiyle değiştirilecektir.

```python
# client oluşturma
# localhost üzerinden 2000 portundan carla simulatore erişilir.
client = carla.Client('localhost', 2000)
```

```python
# İstemci oluşturulduktan sonra zaman aşımını ayarlayın. Bu, tüm ağ işlemlerini sınırlar, böylece bunlar istemciyi sonsuza kadar engellemez. Bağlantı başarısız olursa bir hata döndürülür.
client.set_timeout(10.0) # seconds
```

```python
# Dünya bağlantısı, world adlı degisken kullanılır.
world = client.get_world()
```

```python
# mevcut haritaları listeleyip, o haritayı yükleyebilirsiniz.
print(client.get_available_maps())
world = client.load_world('Town01')
```

Hava

Hava durumu tek başına bir sınıf değil, dünyadan erişilebilen bir dizi parametredir. Parametrizasyon, güneş yönü, bulutluluk, rüzgar, sis ve çok daha fazlasını içerir. Carla.WeatherParameters yardımcı sınıfı, özel bir hava durumunu tanımlamak için kullanılır.

```python
weather = carla.WeatherParameters(
    cloudiness=80.0,
    precipitation=30.0,
    sun_altitude_angle=70.0)

world.set_weather(weather)

print(world.get_weather())
```

Doğrudan dünyaya uygulanabilecek bazı hava durumu ön ayarları vardır. Bunlar carla.WeatherParameters içinde listelenir ve bir enum olarak erişilebilir.

```python
world.set_weather(carla.WeatherParameters.WetCloudySunset)
```

Hata ayıklama

World nesneleri, genel bir öznitelik olarak carla.DebugHelper nesnesine sahiptir. Simülasyon sırasında farklı şekillerin çizilmesine izin verir. Bunlar meydana gelen olayları izlemek için kullanılır. Aşağıdaki örnek, bir oyuncunun konumuna ve dönüşüne kırmızı bir kutu çizer.

```python
debug = world.debug
debug.draw_box(carla.BoundingBox(actor_snapshot.get_transform().location,carla.Vector3D(0.5,0.5,2)),actor_snapshot.get_transform().rotation, 0.05, carla.Color(255,0,0,0),0)
```

Dünya anlık görüntüleri

Simülasyondaki her oyuncunun durumunu tek bir karede içerir. Bir zaman referansı ile dünyanın bir tür hareketsiz görüntüsü. Bilgi, asenkron modda bile aynı simülasyon adımından gelir.

```python
# Retrieve a snapshot of the world at current frame.
world_snapshot = world.get_snapshot()
```


### Aktörler ve planlar

Bir aktör, simülasyonda rol oynayan her şeydir.

    Araçlar.
    Yürüyüşçüler.
    Sensörler.
    Seyirci.
    Trafik işaretleri ve trafik ışıkları.

Taslaklar, bir aktör yaratmak için gerekli olan önceden hazırlanmış aktör düzenleridir. Temel olarak, animasyonlara ve bir dizi özelliğe sahip modeller. Bu 
özelliklerden bazıları kullanıcı tarafından özelleştirilebilir, bazıları özelleştirilmez. Mevcut tüm planları ve bunlarla ilgili bilgileri içeren bir Taslak 
kitaplığı vardır.

### Haritalar ve navigasyon

Harita, simüle edilmiş dünyayı, çoğunlukla şehri temsil eden nesnedir. Mevcut sekiz harita var. Hepsi yolları açıklamak için OpenDRIVE 1.4 standardını kullanıyor.

Yollar, şeritler ve kavşaklar, istemciden erişilmek üzere Python API tarafından yönetilir. Bunlar, araçlara bir navigasyon yolu sağlamak için ara nokta sınıfı ile 
birlikte kullanılır.

Trafik işaretlerine ve trafik ışıklarına, OpenDRIVE tanımları hakkında bilgi içeren carla.Landmark nesneleri olarak erişilebilir. Ek olarak, simülatör, OpenDRIVE 
dosyasındaki bilgileri kullanarak çalışırken otomatik olarak durur, verim ve trafik ışığı nesneleri oluşturur. Bunların yola yerleştirilmiş sınırlayıcı kutuları 
vardır. Araçlar, sınır kutularına girdiklerinde onlardan haberdar olurlar.

### Sensörler ve veriler

Sensörler bir olayın gerçekleşmesini bekler ve ardından simülasyondan veri toplar. Verilerin nasıl yönetileceğini tanımlayan bir işlevi çağırırlar. Hangisine bağlı olarak, sensörler farklı tipte sensör verilerini alır.

Sensör, bir ana araca bağlı bir aktördür. Etrafındaki aracı takip ederek çevrenin bilgilerini toplar. Mevcut sensörler, Taslak kitaplığındaki planlarına göre tanımlanır.

    Kameralar (RGB, derinlik ve anlamsal bölümleme).
    Çarpışma detektörü.
    Gnss sensörü.
    IMU sensörü.
    Lidar raycast.
    Şerit istilası dedektörü.
    Engel detektörü.
    Radar.
    RSS.


