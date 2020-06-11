# C# сэпмлы

Для сборки и запуска C# демо требуются следующие зависимости:

* [Платформа .NET Core](https://docs.microsoft.com/en-us/dotnet/core/get-started) (рекомендуемая версия: 2.1)
* [Обертка .NET для OpenCV](https://github.com/shimat/opencvsharp) (рекомендуемая версия: 3.4.1)
* Для Linux требуется ручная сборка OpenCvSharp.

Для сборки демо-проекта в VisualStudio:

1. Создайте пустое консольное приложение C#
2. Добавьте исходные файлы демо в проект
3. Добавьте ссылки на библиотеку `FacerecCSharpWrapper.dll` и [OpenCvSharp3-AnyCPU](https://www.nuget.org/packages/OpenCvSharp3-AnyCPU)
