# Оценка лиц 

* [Пол и возраст](#пол-и-возраст)
* [Качество изображения лица](#качество-изображения-лица)
* [Принадлежность лица реальному человеку (2D и 3D)](#принадлежность-лица-реальному-человеку)
* [Эмоции](#эмоции)

## Пол и возраст

_**Примечание:** Определение пола и возраста лиц на видеопотоке рассматривается в пункте [Определение пола, возраста и эмоций](video_stream_processing.md#определение-пола-возраста-и-эмоций) раздела [Обработка видеопотока](video_stream_processing.md)._

Для оценки пола и возраста необходимо создать объект `AgeGenderEstimator`, вызвав метод `FacerecService.createAgeGenderEstimator`, передав конфигурационный файл. На данный момент имеется только один файл конфигурации – `age_gender_estimator.xml`. С помощью `AgeGenderEstimator` вы можете определить пол и возраст лица, вызвав метод `AgeGenderEstimator.estimateAgeGender`. Результатом будет структура `AgeGenderEstimator.AgeGender`, содержащая число возраста (в годах), возрастную группу (`AgeGenderEstimator.Age`) и пол (`AgeGenderEstimator.Gender`). 

Пример использования *AgeGenderEstimator* см. в [demo.cpp](../../examples/cpp/demo/demo.cpp). Также вы можете узнать, как определять пол, возраст и эмоции в [нашем туториале](../tutorials/estimating_age_gender_and_emotions.md).

## Качество изображения лица

В настоящий момент существует два интерфейса для оценки качества: `QualityEstimator` и `FaceQualityEstimator`.
* `QualityEstimator` предоставляет **дискретные оценки качества**: степень засветки, равномерность освещения, уровень шума и резкости.
* `FaceQualityEstimator` предоставляет качество в виде **единственного вещественного числа**, агрегирующего качество освещения, размытие, шум и ракурс, что очень удобно для срaвнения качества изображений, полученных от трекера.

### QualityEstimator

Для создания объекта `QualityEstimator` необходимо вызвать метод `FacerecService.createQualityEstimator`, передав конфигурационный файл. На данный момент имеется только один файл конфигурации – `quality_estimator.xml`. При помощи `QualityEstimator` вы можете определить качество изображения лица, вызвав метод `QualityEstimator.estimateQuality`. Результатом будет структура `QualityEstimator.Quality`, содержащая оценки засветки (`flare`), равномерности освещения (`lighting`), шума (`noise`) и резкости (`sharpness`). 

Пример использования `QualityEstimator` см. в [demo.cpp](../../examples/cpp/demo/demo.cpp).

### FaceQualityEstimator

Для создания объекта `FaceQualityEstimator` необходимо вызвать метод `FacerecService.createFaceQualityEstimator`, передав конфигурационный файл. На данный момент имеется только один файл конфигурации – `face_quality_estimator.xml`. При помощи `FaceQualityEstimator` вы можете определить качество изображения лица, вызвав метод `FaceQualityEstimator.estimateQuality`. Результатом будет вещественное число (чем оно больше, тем выше качество), агрегирующее качество освещения, размытие, шум и ракурс. 

Пример использования `FaceQualityEstimator` см. в [demo.cpp](../../examples/cpp/demo/demo.cpp).

## Принадлежность лица реальному человеку

Основной целью оценки принадлежности лица реальному человеку является предотвращение злонамеренных действий с использованием фото вместо реального лица. На данный момент определить принадлежность лица реальному человеку можно двумя способами – [посредством анализа карты глубины](#класс-depthlivenessestimator), либо [посредством анализа цветного изображения с камеры](#класс-livenessestimator). 

Узнайте, как определять принадлежность лица реальному человеку в [нашем туториале](../tutorials/liveness_detection.md). 

### Класс DepthLivenessEstimator 

Для оценки принадлежности лица реальному человеку с использованием карты глубины необходимо создать объект `DepthLivenessEstimator`, вызвав метод `FacerecService.createDepthLivenessEstimator`.

Доступны следующие файлы конфигурации:
* `depth_liveness_estimator.xml` – первая реализация, не рекомендуется использовать (предназначен только для сохранения обратной совместимости)
* `depth_liveness_estimator_cnn.xml` – реализация на основе нейронных сетей, рекомендуемый вариант (используется в `VideoWorker` по умолчанию)

Для использования этого алгоритма необходимо получать синхронизированные и отрегестрированные кадры (цветное изображение + карта глубины) и использовать цветное изображение для детектирования / трекинга лиц, а карту глубины – для передачи в `DepthLivenessEstimator.estimateLiveness`.

Для получения оценки вы можете вызвать метод `DepthLivenessEstimator.estimateLiveness`. Вы получите один из нижеперечисленных результатов:
* `DepthLivenessEstimator.Liveness.NOT_ENOUGH_DATA` – слишком много отсутствующих значений на карте глубины
* `DepthLivenessEstimator.Liveness.REAL` – наблюдаемое лицо принадлежит живому человеку
* `DepthLivenessEstimator.Liveness.FAKE` – наблюдаемое лицо является фотографией

### Класс LivenessEstimator

Для оценки принадлежности лица реальному человеку с использованием цветного изображения с камеры необходимо создать объект `LivenessEstimator`, вызвав метод `FacerecService.createLivenessEstimator`. Вам нужно создать по одному объекту `LivenessEstimator` на каждый уникальный ID и предоставить отслеженный трекером объект `RawSample` соответствующему объекту `LivenessEstimator` через метод `LivenessEstimator.addSample`.

Для получения результата оценки вы можете вызвать метод `LivenessEstimator.estimateLiveness`. Результат будет один из нижеперечисленных:
* `LivenessEstimator.Liveness.NOT_ENOUGH_DATA` – слишком мало кадров или движений лица для принятия решения
* `LivenessEstimator.Liveness.REAL` – наблюдаемое лицо принадлежит живому человеку
* `LivenessEstimator.Liveness.FAKE` – наблюдаемое лицо является фотографией

Пример использования `LivenessEstimator` см. в [demo.cpp](../../examples/cpp/demo/demo.cpp).

## Эмоции

_**Примечание:** Определение эмоций лиц на видеопотоке рассматривается в пункте [Определение пола, возраста и эмоций](video_stream_processing.md#определение-пола-возраста-и-эмоций) раздела [Обработка видеопотока](video_stream_processing.md)._

Для оценки эмоций необходимо создать объект `EmotionsEstimator`, вызвав метод `FacerecService.createEmotionsEstimator`. На данный момент имеется только один файл конфигурации – `emotions_estimator.xml`. При помощи объекта `EmotionsEstimator` вы можете определить эмоцию лица, вызвав метод `EmotionsEstimator.estimateEmotions`. Результатом будет вектор с элементами `EmotionsEstimator.EmotionConfidence`, содержащий эмоции с коэффициентами уверенности. 

Пример использования `EmotionsEstimator` см. в [demo.cpp](../../examples/cpp/demo/demo.cpp).
