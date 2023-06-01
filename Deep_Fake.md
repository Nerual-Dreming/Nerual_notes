# Простой способ сделать Deep Fake Видео в 1 клик. 




## Colab
Google Colab для запуска бесплатно и онлайн : https://colab.research.google.com/github/FurkanGozukara/Stable-Diffusion/blob/main/ColabNotebooks/1_click_deep_fake_for_free_by_SECourses.ipynb



## Подготовка

### Шаг 1 : Python
https://www.python.org/downloads/

**Скачивание и установка Microsoft C++ Build Tools**

https://visualstudio.microsoft.com/visual-cpp-build-tools/

Скриншот что надо выбрать при установке  C++ > клкините чтобы открыть : https://i.imgur.com/7hM2Vsz.png

**Скачайте и устоновите Python 3.10.9 и git**

https://www.python.org/ftp/python/3.10.9/python-3.10.9-amd64.exe
Не забудьте поставить галочку PATH

https://git-scm.com/downloads

### Шаг 2 : Скачайте и устоновите ffmpeg

* https://github.com/GyanD/codexffmpeg/releases
* Скачайте ffmpeg
* Извлеките содержимое архива куда хотите
* Скопируйте путь до папки где лежат exe файлы
* Поменяйте Переменные среды
* Мой путь для примера
* C:\ffmpeg\bin

### Шаг 3 : Запуск на GPU и установка CuDNN  - если у вас слабая видеокарта пропустите этот шаг. 

Скачайите cuDNN v8.7.0 (November 28th, 2022) (https://developer.nvidia.com/rdp/cudnn-archive) , for CUDA 11.x. Потребуется регистрация. Или используйте прямую ссылку ниже

**Прямая ссылка на скачивание : https://huggingface.co/MonsterMMORPG/SECourses/resolve/main/cudnn%208.7.0.84.zip**

* Создайте папку NVIDIA на вашем диске C
* Внутри неё папку CUDNN
* Внутри папку с версией CUDNN C:\NVIDIA\CUDNN\8.7.0.84
* Извлеките bin, lib, включая все папки
* Добавтье путь в переменные среды
* Как на скриншоте

![image](https://github.com/FurkanGozukara/Stable-Diffusion/assets/19240467/8194a8e0-c8b9-4c10-8830-565217d3c69f)

![image](https://github.com/FurkanGozukara/Stable-Diffusion/assets/19240467/08f95f16-aeb5-4959-9c6c-1f9332217bee)

### Шаг 4 : Скачайте и устоновите CUDA Toolkit 11.4 Update 3. 


Ссылка на скачивание, потребуется регистрация : https://developer.nvidia.com/cuda-11-4-3-download-archive?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exe_local

Я использовал этот файл : cuda_11.4.3_472.50_win10.exe

Вот так выглядит мой путь

![image](https://github.com/FurkanGozukara/Stable-Diffusion/assets/19240467/3a635a3b-f606-4ff6-8f5f-e38f8fc8954a)

### Step 5 : Установка Deep Fake Roop

https://github.com/s0md3v/roop основной репозиторий


```

git clone https://github.com/s0md3v/roop


cd roop && pip install -r requirements.txt

```

Скачайте файл модели и положите в корень папки : https://huggingface.co/MonsterMMORPG/SECourses/resolve/main/inswapper_128.onnx

**Делаем запуск удобным**

Создайте текстовой файл и назовите его start.bat, измените содержимое с помощью блакнота и добавтье одну из строк ниже. 

```python run.py``` - стандартный запуск

```python run.py --keep-frames --keep-fps ``` - сохранить папку с фреймами и держать фпс не выше 30

```python run.py --keep-frames --keep-fps --max-cores 1``` --max-cores 1 указывает сколько ядер использовать, полезно если хотите работать за компьютером, но будет сильно дольше. 
```python run.py --keep-frames --keep-fps --max-cores 1 --max-memory 10000``` --max-memory 10000 - ограничивает потребление оперативной памяти до 10гб. 

**Для запуска на GPU добавьте --gpu**

https://github.com/s0md3v/roop/wiki/2.-GPU-Acceleration - как запустить на AMD и mac. 

```python run.py --gpu``` запуск на видеокарте

```python run.py --keep-frames --keep-fps --gpu``` - сохранить папку с фреймами и держать фпс не выше 30 запуск на видеокарте

Добавтье ```git pull``` в началле бат файла, если хотите, чтобы программа при запуске обновлялась. 


_Помните, что только вы несете ответственность за использование эксперементальных технологий. Соблюдайте нормы этики и морали. 
_

**Курс по нейронной сети Vlad Diffusion, от устоновки до апскейла https://clck.ru/34MnrH**

**Хотите быть в курсе всех нейро-тем? Подписывайтесь на мои телеграм каналы по волшебной ссылке - https://t.me/addlist/LQ-fUTyhVjEzYjIy**

