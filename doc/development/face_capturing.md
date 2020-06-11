# Класс Capturer

Для захвата лиц вы должны создать объект `Capturer`, который нужно создать с помощью `FacerecService.createCapturer`, передав путь к конфигурационному файлу или объект `FacerecService.Config`. При передаче пути к конфигурационному файлу будут использованы параметры по умолчанию. При использовании `FacerecService.Config` можно переопределить значение любого числового параметра из конфигурационного файла. Также значения некоторых параметров можно изменить в уже созданном объекте `Capturer` с помощью метода `Capturer.setParameter`.

Пример 1: 

**C++**: ```pbio::Capturer::Ptr capturer = service->createCapturer("common_capturer4.xml");```  
**C#**: ```Capturer capturer = service.createCapturer("common_capturer4_lbf.xml");```  
**Java**: ```final Capturer capturer = service.createCapturer(service.new Config("common_capturer4_lbf.xml"));```  

Пример 2: 

**C++**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```cpp
pbio::FacerecService::Config capturer_config("common_capturer4.xml");
capturer_config.overrideParameter("min_size", 200);
pbio::Capturer::Ptr capturer = service->createCapturer(capturer_config);
```
</details>

**C#**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```cs
FacerecService.Config capturerConfig = new FacerecService.Config("common_capturer4_lbf.xml");
capturerConfig.overrideParameter("min_size", 200);
Capturer capturer = service.createCapturer(capturerConfig);
```
</details>

**Java**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```java
FacerecService.Config capturerConfig = service.new Config("common_capturer4_lbf.xml");
capturerConfig.overrideParameter("min_size", 200);
final Capturer capturer = service.createCapturer(capturerConfig);
```
</details>

Example 3:

**C++**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```cpp
pbio::Capturer::Ptr capturer = service->createCapturer("common_capturer4.xml");
capturer->setParameter("min_size", 200);
capturer->setParameter("max_size", 800);
// capturer->capture(...);
// ...
capturer->setParameter("min_size", 100);
capturer->setParameter("max_size", 400);
// capturer->capture(...);
```
</details>

**C#**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```cs
Capturer capturer = service.createCapturer("common_capturer4_lbf.xml");
capturer.setParameter("min_size", 200);
capturer.setParameter("max_size", 800);
// capturer.capturer(...);
// ...
capturer.setParameter("min_size", 100);
capturer.setParameter("max_size", 400);
// capturer.capture(...);
```
</details>

**Java**

<details>
  <summary>Нажмите, чтобы развернуть</summary>

```java
Capturer capturer = service.createCapturer(service.new Config("common_capturer4_lbf.xml"));
capturer.setParameter("min_size", 200);
capturer.setParameter("max_size", 800);
// capturer.capturer(...);
// ...
capturer.setParameter("min_size", 100);
capturer.setParameter("max_size", 400);
// capturer.capture(...);
```
</details>

Тип и характеристики созданного детектора зависят от переданного в `FacerecService.createCapturer` конфигурационного файла или объекта `FacerecService.Config`.

Мы рекомендуем использовать следующие конфигурационные файлы: 
* `common_capturer4_fda.xml` – детектор фронтальных лиц, разработанный 3DiVi Inc., который работает значительно лучше, чем детекторы из открытых библиотек, таких как OpenCV или Dlib
* `common_video_capturer_fda.xml` – видеотрекер фронтальных лиц, разработанный 3DiVi Inc. (работает только с цветными изображениями).

_**Примечание:** Для детекции лиц на видеопотоках рекомендуется использовать интерфейсный объект `VideoWorker`. Если при создании `VideoWorker` указаны параметры `matching_thread=0` и `processing_thread=0`, то потребляется обычная [лицензия Face Detector](../components.md)._

Используемые наборы антропометрических точек (см. [Антропометрические точки](#антропометрические-точки)):

|config file|points set|
|-----------|----------|
|common_capturer4_fda.xml |fda|
|common_video_capturer_fda.xml|fda|

Вы можете использовать созданный детектор для обнаружения и отслеживания лиц. Существует два способа подать изображение на вход детектору:
* подать данные раскодированного изображения в метод `Capturer.capture(final RawImage image)`, используя класс `RawImage` (см. [Сэмплы](../samples))
* подать данные закодированного изображения в формате JPEG, PNG, TIF или BMP в метод `Capturer.capture(final byte[] data)`

В обоих случаях результатом является список найденных / отслеженных лиц (`RawSample` – объект, хранящий найденное лицо).

Для трекера вы также можете вызвать метод `Capturer.resetHistory`, чтобы начать отслеживание на новой видеопоследовательности.

# Класс RawSample

При помощи RawSample вы можете:
* получить id, назначенное сэмплу при детекции (`RawSample.getID`) в том случае, если объект был получен от трекера
* получить прямоугольник лица (`RawSample.getRectangle`), углы (`RawSample.getAngles`), левый / правый глаз (`RawSample.getLeftEye` / `RawSample.getRightEye`, см. [Антропометрические точки](#антропометрические-точки)), антропометрические точки (`RawSample.getLandmarks`, см. [Антропометрические точки](#антропометрические-точки)), если если лицо расположено фронтально (т.е. получено фронтальным детектором / трекером)
* обрезать лицо (см. [Обрезка лиц](#обрезка-лиц), [test_facecut](../samples/cpp/test_facecut.md)
* уменьшить внутреннее изображение лица до предпочтительного размера (`RawSample.downscaleToPreferredSize`)
* сериализовать объект в бинарном формате (`RawSample.save` или `RawSample.saveWithoutImage`), после чего вы можете десериализовать объект методом `FacerecService.loadRawSample` или `FacerecService.loadRawSampleWithoutImage`
* передать объект в методы оценки возраста, пола, качества и принадлежности лица реальному человеку (см. [Оценка лиц](face_estimation.md), [test_facecut](../samples/cpp/test_facecut.md), [test_videocap](../samples/cpp/test_videocap.md))
* передать объект в `Recognizer.processing` для создания шаблона (см. [Идентификация лиц](face_identification.md), [test_identify](../samples/cpp/test_identify.md))

