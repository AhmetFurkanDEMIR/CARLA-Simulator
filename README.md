
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

Carla.BlueprintLibrary sınıfı, carla.ActorBlueprint öğelerinin bir listesini içerir. Ona erişimi sağlayabilen dünya nesnesidir.

```python
blueprint_library = world.get_blueprint_library()
```

Taslakların onları tanımlamak için bir kimliği vardır ve aktörler onunla birlikte ortaya çıkar. Kitaplık, belirli bir kimliği bulmak, rastgele bir plan seçmek veya sonuçları bir joker karakter kalıbı kullanarak filtrelemek için okunabilir.

```python
# Belirli bir plan bulun.
collision_sensor_bp = blueprint_library.find('sensor.other.collision')
# Rastgele bir araç planı seçin.
vehicle_bp = random.choice(blueprint_library.filter('vehicle.*.*'))
```

Bunun yanı sıra, her carla.ActorBlueprint, alınıp ayarlanabilen bir carla.ActorAttribute serisine sahiptir.


```python
is_bike = [vehicle.get_attribute('number_of_wheels') == 2]
if(is_bike)
    vehicle.set_attribute('color', '255,0,0')
```

Özniteliklerin carla.ActorAttributeType değişkeni vardır. Türünü bir numaralandırma listesinden belirtir. Ayrıca değiştirilebilir öznitelikler, önerilen değerlerin bir listesiyle birlikte gelir.

```python
for attr in blueprint:
    if attr.is_modifiable:
        blueprint.set_attribute(attr.id, random.choice(attr.recommended_values))
```

Spawning

Dünya nesnesi, oyuncuları yetiştirmekten ve bunların takibinden sorumludur. Spawning yalnızca bir plan ve oyuncu için bir konum ve dönüş belirten bir carla.Transform gerektirir.

Oyuncu yetiştirmek için dünyanın iki farklı yöntemi vardır.

spawn_actor() Spawning başarısız olursa bir istisna yaratır.
try_spawn_actor() Spawning başarısız olursa None döndürür.


```python
transform = Transform(Location(x=230, y=195, z=40), Rotation(yaw=180))
actor = world.spawn_actor(blueprint, transform)
```

Oyuncu, belirtilen konumda çarpışma durumunda ortaya çıkmayacaktır. Bunun statik bir nesneyle veya başka bir oyuncuyla olması farketmez. Bu istenmeyen Spawning çarpışmalarından kaçınmayı denemek mümkündür.

```python
# araçlar için. Önerilen Spawning noktalarının bir listesini döndürür.
spawn_points = world.get_map().get_spawn_points()
```

yürüyüşçüler için world.get_random_location (). Kaldırımda rastgele bir nokta verir. Aynı yöntem, yürüyüşçüler için bir hedef konumu belirlemek için kullanılır.

```python
spawn_point = carla.Transform()
spawn_point.location = world.get_random_location_from_navigation()
```


### Haritalar ve navigasyon

Harita, simüle edilmiş dünyayı, çoğunlukla şehri temsil eden nesnedir. Mevcut sekiz harita var. Hepsi yolları açıklamak için OpenDRIVE 1.4 standardını kullanıyor.

Yollar, şeritler ve kavşaklar, istemciden erişilmek üzere Python API tarafından yönetilir. Bunlar, araçlara bir navigasyon yolu sağlamak için ara nokta sınıfı ile 
birlikte kullanılır.

Trafik işaretlerine ve trafik ışıklarına, OpenDRIVE tanımları hakkında bilgi içeren carla.Landmark nesneleri olarak erişilebilir. Ek olarak, simülatör, OpenDRIVE 
dosyasındaki bilgileri kullanarak çalışırken otomatik olarak durur, verim ve trafik ışığı nesneleri oluşturur. Bunların yola yerleştirilmiş sınırlayıcı kutuları 
vardır. Araçlar, sınır kutularına girdiklerinde onlardan haberdar olurlar.

**Varsayılan olarak gelene haritalar**

|   Kasaba Özeti    |   Özet  |
| ------------------| ----------- |
| Town01            | Tüm "T kavşakları" ile temel bir şehir düzeni.       |
| Town02            | Town01'e benzer, ancak daha küçük.         |
| Town03            | 5 şeritli bir kavşak, döner kavşak, düzensizlik, tünel ve çok daha fazlasıyla en karmaşık kasaba.       |
| Town04            | Bir otoyol ve küçük bir kasaba ile sonsuz bir döngü.       |
| Town05            | Kavşakları ve köprüsü olan kare şeklinde şehir. Yön başına birden fazla şeridi vardır. Şerit değişiklikleri yapmak için kullanışlıdır.        |
| Town06            | Birçok otoyol girişi ve çıkışı olan uzun otoyollar. Aynı zamanda bir Michigan solu da var.        |
| Town07            | Dar yolları, neredeyse hiç olmayan trafik ışıkları ve ahırları olan kırsal bir ortam.        |
| Town08            | Cadde veya gezinti yeri gibi farklı ortamlara ve daha gerçekçi dokulara sahip bir şehir ortamı.       |

<p align="center">
  <img src="https://user-images.githubusercontent.com/54184905/109822845-66da3c80-7c48-11eb-9924-7b9e68d382e4.png" />
</p>

### Sensörler ve veriler

Sensörler bir olayın gerçekleşmesini bekler ve ardından simülasyondan veri toplar. Verilerin nasıl yönetileceğini tanımlayan bir fonksiyon çağırırlar. Sensör, bir ana araca bağlı bir aktördür. Etrafındaki aracı takip ederek çevrenin bilgilerini toplar. Mevcut sensörler, Taslak kitaplığındaki planlarına göre tanımlanır.

    Kameralar (RGB, derinlik ve anlamsal bölümleme).
    Çarpışma detektörü.
    Gnss sensörü.
    IMU sensörü.
    Lidar raycast.
    Şerit istilası dedektörü.
    Engel detektörü.
    Radar.
    RSS.


Sensörler adım adım

Carla.Sensor sınıfı, verileri ölçebilen ve aktarabilen özel bir aktör türünü tanımlar.

Bu veriler nedir? Sensör tipine bağlı olarak çok değişir. Tüm veri türleri genel carla.SensorData'dan miras alınır.

Verileri ne zaman alırlar? Ya her simülasyon adımında ya da belirli bir olay kaydedildiğinde. Sensör tipine bağlıdır. Her sensörün verileri almak ve yönetmek için bir listen () yöntemi vardır.

Ayarlar

As with every other actor, find the blueprint and set specific attributes. This is essential when handling sensors. Their attributes will determine the results obtained. These are detailed in the sensors reference.

The following example sets a dashboard HD camera.


```python
# Sensörün planını bulun.
blueprint = world.get_blueprint_library().find('sensor.camera.rgb')

# Görüntü çözünürlüğünü ve görüş alanını ayarlamak için planın niteliklerini değiştirin.
blueprint.set_attribute('image_size_x', '1920')
blueprint.set_attribute('image_size_y', '1080')
blueprint.set_attribute('fov', '110')

# Sensör yakalamaları arasındaki süreyi saniye cinsinden ayarlayın
blueprint.set_attribute('sensor_tick', '0.2')
```

Dinleme

Her sensörün bir listen () yöntemi vardır. Bu, sensör her veri aldığında çağrılır. Argüman geri çağrısı bir lambda işlevidir. Veriler alındığında sensörün ne yapması gerektiğini açıklar.


```python
# do_something(), kamera tarafından her yeni görüntü oluşturulduğunda çağrılacaktır.
sensor.listen(lambda data: do_something(data))

...

# Bu çarpışma sensörü, her çarpışma algılandığında yazdıracaktır.
def callback(event):
    for actor_id in event:
        vehicle = world_ref().get_actor(actor_id)
        print('Vehicle too close: %s' % vehicle.type_id)

sensor02.listen(callback)
```

Veri

Çoğu sensör veri nesnesinin, bilgileri diske kaydetme işlevi vardır. Bu, diğer ortamlarda kullanılmasına izin verecektir.

Sensör verileri, sensör türleri arasında çok farklılık gösterir. Ayrıntılı bir açıklama almak için sensör referansına bir göz atın. Bununla birlikte, hepsi her zaman bazı temel bilgilerle etiketlenir.


|   Sensör veri özelliği    |    Tip   | Açıklama |
| --------------------------|----------|----------|
| frame                     | int      | Ölçüm gerçekleştiğinde çerçeve numarası. |
| timestamp                 | Double   | Bölümün başlangıcından bu yana simülasyon saniyelerinde ölçümün zaman damgası. |
| transform                 | [carla.Transform](https://carla.readthedocs.io/en/latest/python_api/#carlatransform)       | World reference of the sensor at the time of the measurement. |
