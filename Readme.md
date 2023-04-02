# Инструкция по работе с Git и удалёнными репозиториями

## Что такое git?
**Git** — распределённая система управления версиями. Проект был создан Линусом Торвальдсом для управления разработкой ядра Linux, первая версия выпущена 7 апреля 2005 года. На сегодняшний день его поддерживает Джунио Хамано.

## Подготовка репозитория
Для создания нового репозитория используется команда **git init**. Команду **git init** выполняют только один раз для первоначальной настройки нового репозитория. Выполнение команды приведет к созданию нового подкаталога .git в вашем рабочем каталоге. Кроме того, будет создана новая главная ветка.

## Создание коммитов

### Добавление файла к коммиту
Для добавления файла к будущему коммиту используется команда *git add*. Для этого в терминале с папкой-репозиторием необходимо написать *git add <название файла>*.

## Создание коммитов
В **Git** и других системах управления версиями концепция сохранения проработана более детально, чем в текстовых процессорах или других традиционных приложениях для редактирования файлов. Традиционный термин «сохранение» в программировании синонимичен понятию коммита в **Git**. Коммит в Git является эквивалентом сохранения. Традиционное сохранение — это операция файловой системы, которая используется для перезаписи существующего файла или записи нового. В отличие от нее, коммит Git выполняется над набором файлов и каталогов.

## git add

Команда **git add** добавляет изменение из рабочего каталога в раздел проиндексированных файлов. Она сообщает **Git**, что вы хотите включить изменения в конкретном файле в следующий коммит. Однако на самом деле команда **git add** не оказывает существенного влияния на репозиторий: изменения регистрируются в нем только после выполнения команды **git commit**.

Наряду с этими командами вам понадобится команда **git status**, которая показывает состояние рабочего каталога и раздела проиндексированных файлов.

## Перемещение между коммитами

Для перемещения между коммитами используется команда **git checkout <хэш коммита>**.

## Ветки в git

Ветвление стало неотъемлемой частью командной разработки, потому что оно дает возможность работать над разными версиями исходного кода. Основной идеей ветвления является отклонение от основного кода и продолжение работы независимо от него. Также это удобно в тестировании отдельного функционала, потому что позволяет работать над новой частью кода, не беспокоясь о поломке чего-то в рабочей версии.

### Создание веток

Чтобы добавить ветку мы используем команду:

    git branch <name of new branch>

После данной операции ветка уже была создана, но вы по-прежнему находитесь в прежней ветке. Если вы планируете переместиться на другую ветку, в том числе только что созданную, необходимо использовать команду:

    git checkout <name of branch>

### Слияние веток и разрешение конфликтов

Ветвление позволяет разделять рабочий процесс, оптимизировать тестирование и написание нового кода. Однако после того, как разработчик убедился, что написанный им кусок кода готов и его можно отправить к остальной части итоговой версии, удобно переместить его в основную ветку. Такой подход дает возможность получить к концу разработки проекта целый продукт в одном месте.
Для этого в Git предусмотрено слияние — перенос изменений с одной ветки на другую. Однако сливаемая ветка (под этим определением мы подразумеваем ветку, у которой берем изменения для «вливания» их в другую ветвь) никак не меняется и остается в прежнем состоянии. Такие преобразования мы получаем, применив команду:

    git merge <name of merged branch>

Операция может привести к появлению конфликтов при попытке слить ветки. Это вызвано тем, что изменения удаляют или переписывают информацию в существующих файлах. При попытке некорректного слияния **Git** останавливает выполнение команды, чтобы вы могли разрешить конфликт.

Также стоит упомянуть о существовании ключей, предназначенных специально для работы с конфликтами:

- abort — прерывает слияние и возвращает все к началу
- continue — продолжает слияние после разрешения конфликта

Решить конфликт можно двумя способами:

- Вручную разрешить файловый конфликт. Для этого нужно самим изменить файлы, с которыми возникли проблемы. Мы получим файлы такими, какими и представляли их при попытке слияния.
- Выбрать более подходящий файл, а от второго отказаться.

### Удаление веток

Удаление веток не такой простой процесс, как может показаться. Можно случайно удалить несохраненные изменения в исходном коде, что приведет к нежелательным последствиям. Поэтому здесь нужно действовать осторожно. С операцией удаления над ветками справляется уже привычная команда **git branch** с параметром -d:

    git branch -d <name of branch>

Для корректного удаления нужно помнить несколько правил, чтобы не получить ошибки:
- **Нельзя удалить ветку, в которой вы находитесь.** Git выкинет ошибку и не произведет удаление. Следовательно, нужно перейти на другую ветку.
- **Git не позволит удалить ветку, у которой есть несохраненные изменения.** Так мы избегаем ситуации, когда часть написанного кода будет безвозвратно утеряна. Если же мы уверены, что изменения в этой версии не нужны и их можно смело удалять, то вместо флага -d используем -D.