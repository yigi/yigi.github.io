### İlk sinir ağınızı eğitin: temel sınıflandırma IMAGE

```python
from __future__ import absolute_import, division, print_function, unicode_literals

# TensorFlow ve tf.keras
import tensorflow as tf
from tensorflow import keras

# Yardimci kutuphaneler
import numpy as np
import matplotlib.pyplot as plt

print(tf.__version__)
```

```python
fashion_mnist = keras.datasets.fashion_mnist

(train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
```

Veri kümesinin yüklenmesi sonucunda 4 NumPy dizisi oluşur:

train_images ve train_labels dizileri eğitim veri setidir - modelin eğitilmesinde kullanılır.
test_images ve test_labels dizileri test veri setidir - modelin test edilmesinde kullanılır.
train_images, test_images 28x28 boyutunda ve piksel değerleri 0 ile 255 arasında değişen NumPy dizileridir. train_labels, test_labels ise 0 ile 9 arasında değişen ve her biri bir giyim eşyası sınıfı ile eşleşen tam sayı dizisidir:


<img align="center" width="850" height="500" src="https://tensorflow.org/images/fashion-mnist-sprite.png?hl=TR">

```python
class_names = ['Tişört/Üst', 'Pantolon', 'Kazak', 'Elbise', 'Mont', 
               'Sandal', 'Gömlek', 'Spor Ayakkabı', 'Çanta', 'Yarım Bot']
```

```python
train_images.shape
# (60000, 28, 28)
```

to see image in 255 color 
<img align="right" width="300" height="200" src="https://www.tensorflow.org/tutorials/keras/basic_classification_files/output_m4VEw8Ud9Quh_0.png?hl=TR">
```python
plt.figure()
plt.imshow(train_images[0])
plt.colorbar()
plt.grid(False)
plt.show()
```

```python
plt.figure(figsize=(10,10))
for i in range(25):
    plt.subplot(5,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(train_images[i], cmap=plt.cm.binary)
    plt.xlabel(class_names[train_labels[i]])
plt.show()
```

Katmanların hazırlanması
Sinir ağını oluşturan temel yapı taşları katman'lardır. Katmanlar, kendilerine beslenen verileri kullanarak bu verilere ait çıkarımlar oluştururlar. Bu çıkarımların, bu örnekte görüntülerin sınıflandırılması olarak karşımıza çıkan problemin çözümüne yardımcı olması beklenir.

Çoğu derin öğrenme modeli, birbirlerine bağlanmış birçok basit katman içermektedir. Çoğu katman, tf.keras.layers.Dense gibi, eğitme sürecinde öğrenilen parametrelere sahiptir.

```python
model = keras.Sequential([
    keras.layers.Flatten(input_shape=(28, 28)),
    keras.layers.Dense(128, activation=tf.nn.relu),
    keras.layers.Dense(10, activation=tf.nn.softmax)
])
```

Ağımızın ilk katmanı olan **tf.keras.layers.Flatten**, görüntülerin formatını 2 boyutlu sayı dizisinden (28 x 28 piksel), 28 * 28 = 784 piksel değerinden oluşan tek boyutlu bir sayı dizisine çevirir. Bu katmanın, görüntüleri oluşturan piksel satırlarının çıkarılarak, art arda birleştirilmesi ile oluştuğunu düşünebilirsiniz. Bu katmanda öğrenilecek parametre olmayıp, sadece görüntünün formatını düzenler.

Görüntüyü oluşturan pikselleri tek boyutlu sayı dizisine düzleştirdikten sonra, ağımız ardaşık iki **tf.keras.layers.Dense** katmanını içerir. Bunlara, yoğun-bağlı veya tam-bağlı ağ katmanları denir. İlk 'Yoğun' katman 128 neron'a (düğüm) sahiptir. İkinci katman is 10 neronlu 'softmax' katmanıdır. Bu son katmanın çıktısı, toplam değerleri 1' eşit olan ve 10 farklı olasılık sonucunu içeren sayı dizisidir. Her bir düğüm, mevcut görüntünün hangi sınıfa ait olduğu belirten olasılık değerini içerir.

Kayıp Fonksiyonu - Loss Function — Bu fonksiyon modelin eğitim sürecinde ne kadar doğru sonuç verdiğini ölçer. Bu fonksiyonun değerini en aza indirgeyerek, modelin doğru istikamete "yönlendirmek" isteriz.
Eniyileme - Optimizer — Beslenen veriler ve kayıp fonksiyonu ile modelin nasıl güncellediğini belirler
Metrikler - Metrics — Eğitim ve test adımlarını gözlemlemek için kullanılır. Aşağıdaki örnekte, doğruluk-accuracy, modelin doğru sınıfladığı görüntü oranı, kullanılmaktadır.
```python
model.compile(optimizer='adam', 
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```
**Fit the model**

```python
model.fit(train_images, train_labels, epochs=5)
```
```python
test_loss, test_acc = model.evaluate(test_images, test_labels)

print('Test accuracy:', test_acc)

#10000/10000 [==============================] - 1s 54us/sample - loss: 0.3589 - accuracy: 0.8705
#Test accuracy: 0.8705
```

**Test veri setinden bir resim secelim.**
```python
img = test_images[0]

print(img.shape)

(28, 28)
```
tf.keras modelleri, veri yığınları içerisindeki örnekler üzerinden tahminleme yapmak üzere optimize edilmiştirler. Tek bir görüntü kullanmamıza rağmen, bu nedenle görüntüyü bir listeye aktarmamız gerekmektedir:

**Resmi tek ogesi kendisi olacagi bir listeye aktaralim**
```python
img = (np.expand_dims(img,0))

print(img.shape)

(1, 28, 28)
```

**Şimdi görüntüyü tahminleyelim:**
```python
predictions_single = model.predict(img)

print(predictions_single)

plot_value_array(0, predictions_single, test_labels)
plt.xticks(range(10), class_names, rotation=45)
plt.show()
```

**model.predict** çalıştırıldığında, veri yığını içerisindeki her bir görüntüye ait bir liste verir. Yığın içerisinden görüntümüze (örneğimizdeki tek görüntü) ait tahminleme sonuçlarını alalım:
```python
prediction_result = np.argmax(predictions_single[0])
print(prediction_result)

9
```
<img align="center" width="350" height="340" src="https://www.tensorflow.org/tutorials/keras/basic_classification_files/output_6Ai-cpLjO-3A_0.png">

