# Простой способ сделать Deep Fake Видео в 1 клик. 

**ВИДЕО ГАЙД - https://youtu.be/87Xw2DM0ROI
**

## Colab
Google Colab для запуска бесплатно и онлайн : https://colab.research.google.com/github/FurkanGozukara/Stable-Diffusion/blob/main/ColabNotebooks/1_click_deep_fake_for_free_by_SECourses.ipynb



## Подготовка к запуск локально

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


### Step 5 : Установка Deep Fake Roop для запуска на CPU

https://github.com/s0md3v/roop основной репозиторий

Выполните по очередите эти команды

```

git clone https://github.com/s0md3v/roop

cd roop

python -m venv venv

cd venv

cd Scripts

activate

cd..
cd..

pip install -r requirements.txt

```

**Установка Deep Fake Roop для запуска на GPU**

Выполните по очередите эти команды

```
git clone https://github.com/s0md3v/roop

cd roop

python -m venv venv

cd venv

cd Scripts

activate

cd..
cd..

pip install -r requirements.txt
pip uninstall onnxruntime onnxruntime-gpu
pip install torch torchvision torchaudio --force-reinstall --index-url https://download.pytorch.org/whl/cu118
pip install onnxruntime-gpu

```



Скачайте файл модели и положите в корень папки : https://huggingface.co/MonsterMMORPG/SECourses/resolve/main/inswapper_128.onnx

**Делаем запуск удобным**

Создайте текстовой файл и назовите его start.bat, со следуюзщим содержимым:
```
@echo off

git pull

rem Активируем виртуальную среду
python -m venv venv
call venv\Scripts\activate.bat

rem Запускаем файл run.py
python run.py --keep-frames --keep-fps --gpu
```

Измените последнюю строку с помощью блакнота чтобы задать желаемые аргументы запуска с GPU или на CPU. 

```python run.py``` - стандартный запуск

```python run.py --keep-frames --keep-fps ``` - сохранить папку с фреймами и держать фпс не выше 30

```python run.py --keep-frames --keep-fps --max-cores 1``` --max-cores 1 указывает сколько ядер использовать, полезно если хотите работать за компьютером, но будет сильно дольше. 
```python run.py --keep-frames --keep-fps --max-cores 1 --max-memory 10000``` --max-memory 10000 - ограничивает потребление оперативной памяти до 10гб. 

**Для запуска на GPU добавьте --gpu**

https://github.com/s0md3v/roop/wiki/2.-GPU-Acceleration - как запустить на AMD и mac. 

```python run.py --gpu``` запуск на видеокарте

```python run.py --keep-frames --keep-fps --gpu``` - сохранить папку с фреймами и держать фпс не выше 30 запуск на видеокарте

```python run.py --keep-frames --keep-fps --gpu --gpu-threads 6``` - --gpu-threads позволяет ограничить потребление видеокарты, значение 6 - потребляет примерно 8 Gb, --gpu-threads 16 - 20 Gb.

Добавтье ```git pull``` в началле бат файла, если хотите, чтобы программа при запуске обновлялась автоматически. 

**Улучшаем качество ДипФейков**

Открываем Vlad Diffusion на вкладке Process или Automatic1111 на вкладке Extras

Далее переходим на вкладку Process Folder для Влада или Batch from directory для SD
Указываем нашу папку с обработанными кадрами, просто копируйте путь из проводника. Ниже вставляйте путь еще раз, только добавляйте в конце /out, это будет выходная папка. 

Ползунок Resize ставим в положение 1, нам не нужно сейчас увеличить размер кадра, хотя в некоторых случаях вам это может пригодится. 
Апскейлеры оставляем на None, а самые нижние ползунки CodeFormer visibility и CodeFormer weight  ставим на 1. 

Запускаем генерацию. Через некоторое время когда работа Кодформера завершится, мы получим значительно более четкие и красивые лица. 
Конечно им еще не помешает легкая постобработка в программе для монтажа, чтобы смягчить края, но результат уже будет потрясющим.

Для того чтобы собрать кадры обратно в файл можно воспользоваться любым видеоредактором, либо же использовать простую команду ffmpeg которую мне подсказал ChatGPT.
Просто зайдите в папку где лежат ваши кадры, введите в адресную строку cmd, затем ниже следующую команду

```ffmpeg -framerate 30 -i %04d-0000.png -c:v libx264 -pix_fmt yuv420p without_sound.mp4``` - обратите внимание, фреймрейт должен соответствовать вашему изначальному видео, т.к. вам надо будет отдельно синхронизировать потом кадры и звук из изначального видео. Я для этого тоже использую команду ffmpeg

```ffmpeg -i without_sound.mp4 -i me_with_Sound.mp4 -c:v copy -map 0:v:0 -map 1:a:0 -shortest final_with_sound.mp4``` эта команда добавляет звук из нашего изначального файла в новый созданный

Если у вас сложности с этими командами, просто откройте ChatGPT, я использую китайский аналог - https://chatbot.theb.ai/ и прямо напишите вашу задачу там, и укажите все названия ваших исходников ```Команда ffmpeg win 10 которая собирает кадры 0001-0000.png -  0773-0000.png в видео с частатой 30 кадров в секунду``` таким образом для вас будет создана команда которую вам останется просто скопировать в командную строку. 


_Помните, что только вы несете ответственность за использование эксперементальных технологий, одной из которой является приложение roop. Соблюдайте нормы этики и морали, а так же законы той страны, в которой находитесь, в некоторых странах создание дипфейков может быть преступлением._

**Курс по нейронной сети Vlad Diffusion, от устоновки до апскейла https://clck.ru/34MnrH**

**Эксклюзивы для подписчиков, записи стримов, секретные гайды, доступ в закрытый чат и многое другое только на бусти - https://boosty.to/neuro_art**

**Хотите быть в курсе всех нейро-тем? Подписывайтесь на мои телеграм каналы по волшебной ссылке - https://t.me/addlist/LQ-fUTyhVjEzYjIy**

