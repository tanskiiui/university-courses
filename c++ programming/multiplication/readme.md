# Умножение чисел

Эта задача предназначена для знакомства с тестирующей системой. Вам предстоит реализовать функцию `Multiply`, которая перемножает 2 числа, в файле `multiplication.h`. Перед тем как приступить настройте окружение согласно инструкции на вики.

### Структура задачи

В каждой задаче обычно есть как минимум 3 файла:

* `CMakeLists.txt` --- cmake-файл для сборки задачи.
* `test.cpp` --- сами тесты для задачи.
* `*.h` --- некоторый .h файл, в котором вы должны реализовать то, что требуется в условии задачи (в данном случае `multiplication.h`).

Вам разрешено изменять только файлы, содержащие решение задачи, в противном случае система не примет вашу посылку.
Когда вы делаете посылку, система запускает `test.cpp`, и в случае успешного завершения
задача вам засчитывается.

Обратите внимание, что в некоторых задачах `test.cpp` может либо вообще не содержать тестов, либо содержать не все тесты, которые будут на сервере --- об этом всегда сообщается в условии задачи.
В этом случае вы сами должны написать тесты и протестировать всю реализованную функциональность.

### Сборка

Для новичков мы рекомендуем использовать Visual Studio Code. Сборка с его использованием разобрана в инструкции на странице курса. Здесь
приведены инструкции для использования из консоли.

#### Linux & OSX

Создадим директорию со сборкой:
```
# В директории shad-cpp0.
mkdir build
cd build
```

Запустим cmake:

```
cmake ..
```

Если на этом шаге вы получаете странные ошибки, проверьте что вы создали директорию `build` в корне репозитория, а не в директории с задачей.

При этом будет выведена некоторая служебная информация, в частности используемый компилятор. Для корректной сборки необходим `g++` версии не ниже 7.1 или `clang++` версии не ниже 5.0.

Наконец, соберем нашу задачу `test.cpp`:
```
make test_multiplication
```

Все задачи включены в один проект, поэтому если вы попытаетесь собрать проект целиком, могут возникнуть ошибки. Поэтому при сборке нужно указывать конкретный исполняемый файл, который вам нужен.

Теперь в `build` есть исполняемый файл test_multiplication, который и нужно запустить.

Обратите внимание, что помимо этого на сервере также осуществляется тестирование с включенными санитайзерами, которые проверяют наличие неопределенного поведения и некорректной работы с памятью
в программе. Осуществить такую сборку просто:
```
mkdir asan_build
cd asan_build
cmake -DCMAKE_BUILD_TYPE=ASAN ..
make test_multiplication
```

Если вы реализуете решение в этой задаче просто как `a * b` (без приведения к `int64_t`), то тесты в asan-сборке должны упасть с соответствующим сообщением о переполнении.

#### Windows

Если вы используете mingw и cygwin, то все шаги такие же, разве что asan сборку вы сделать не сможете. Чтобы работать из Visual Studio 2017, сделайте следующее:

1. Выберите Open Folder и откройте папку с задачей.
2. Зайдите в Cmake/Change Cmake Settings.
3. В тех конфигурациях, которые вам нужны, поменяйте содержимое buildRoot на "${workspaceRoot}\\\\build".
4. Теперь вы можете использовать Cmake/Build all для сборки. Запускать из Visual Studio (без дебага) неудобно, это лучше делать из терминала. В директории с задачей после
сборки должна появиться папка build, где и находится исполняемый файл.

Обратите внимание, что компилятор MSVC может давать иные предупреждения/ошибки компиляции, чем те, которые вы можете получить на сервере, где используется gcc.

### Примечания

Обратите внимание, что в реальности в .h файлах не пишутся реализации функций и классов, но для простоты в задачах первых семинаров вам нужно будет писать реализации в .h файлах.
