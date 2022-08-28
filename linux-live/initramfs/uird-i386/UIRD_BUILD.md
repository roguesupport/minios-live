## 1. Клонируем репозиторий
    git clone --recursive https://github.com/neobht/uird.git
## 2. Устанавливаем зависимости, необходимые для сборки dracut

Проще всего установить src пакет dracut для вашего дистрибутива.
### Приблизительный список:
    * make
    * pkg-config
    * kmod
    * gcc
    * glibc
    * linux-api-headers
## 3. Собираем busybox
    cd ./uird
    ./make_busybox.sh
## 4. Собираем dracut
    ./make_dracut.sh
  
  Ищем подходящий конфиг в **uird/configs/uird_configs**
  
  Если нет подходящего, то создаём новый.

## 5. Собираем UIRD
    ./mkuird ИМЯ_КОНФИГА
### Например:
    ./mkuird MagOS

В корне каталога **uird** появится файл **uird.ИМЯ_КОНФИГА.cpio.xz**, это и есть ваш UIRD.

### Ошибки
Сообщения при сборке вроде:

    * modinfo: ERROR: Module ext3 not found.
  
Не являются ошибкой, скорее всего указанный модуль встроен в ядро.
### Ключи и параметры
    * -k kernel - имя ядра, под который собирается UIRD (для текущего ядра указывать не нужно)
    * -m /path/dir - каталог с модулями ядра (по умолчанию дефолтное значение для дистра, обычно это /lib/modules)
    * -e список,модулей_ядра,бинарников, которые нужно исключить при сборке UIRD (смотрите mkuird.cfg)
    * -с file.cfg - конфиг вместо дефолтного mkuird.cfg

### Примечание 
Если после выполнения **./mkuird** в корне каталога **uird** не появится файл **uird.ИМЯ_КОНФИГА.cpio.xz**, то смотрите лог на предмет ошибок дракута:

    * dracut_magos.log
  
В файле 

    * not_found.log
  
можно посмотреть ненайденные при сборке бинарники, обычно они предоставляют расширенный функционал для UIRD.
Если в списке будут бинарники, функционал которых нужен вам в UIRD, то бинарник нужно установить, и UIRD пересобрать.