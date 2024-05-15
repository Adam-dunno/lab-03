## HOMEWORK 3


# Задание 1

Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории `formatter_lib`. В этой директории находятся файлы для статической библиотеки `formatter`. Создайте `CMakeList.txt` в директории `formatter_lib`, с помощью которого можно будет собирать статическую библиотеку formatter


```
$ sudo apt install cmake - устанавливаем пакет cmake
```




```
$ echo "# lab-03" >> README.md
$ git init
$ git add README.md
$ git commit -m "fork"
$ git remote add origin https://github.com/Adam-dunno/lab-03.git
$ git push -u origin master
```


```
$ git checkout -b lab
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```


Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter)

add_library(formatter STATIC formatter.cpp)
target_include_directories(formatter PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

- Команда cmake_minimum_required указывает подходящую минимальную версию Cmake
- Команды set(CMAKE_CXX_STANDARD 11), set(CMAKE_CXX_STANDARD_REQUIRED ON) устанавливают значения стандартных переменных в Cmake(в данном случае CMAKE_CXX_STANDARD и CMAKE_CXX_STANDARD_REQUIRED)
- Команда project(formatter) создает проект formatter, к которому можно подключать библиотеки, исполняемы файлы и т.д.
- Команда add_library(formatter STATIC formatter.cpp) создает статическую библиотеку из указываемых файлов
- Команда target_include_directories связывает библиотеку formatter и CMAKE_CURRENT_SOURCE_DIR

```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add formatter.h
$ git commit -m "added formatter.h"
$ git push origin lab
$ git add formatter.cpp
$ git commit -m "added formatter.cpp"
$ git push origin lab

```

```

[lab be466e5] added CMakeLists.txt
 1 file changed, 9 insertions(+)
 create mode 100644 formatter_lib/CMakeLists.txt
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 522 bytes | 522.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   d9b725b..be466e5  lab -> lab
[lab 8c9ee1d] added formatter.h
 1 file changed, 5 insertions(+)
 create mode 100644 formatter_lib/formatter.h
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 445 bytes | 445.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   be466e5..8c9ee1d  lab -> lab
[lab 05af4d6] added formatter.cpp
 1 file changed, 10 insertions(+)
 create mode 100644 formatter_lib/formatter.cpp
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 507 bytes | 507.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   8c9ee1d..05af4d6  lab -> lab


```




Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build

```



```
-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/adam/lab-03/formatter_lib/_build
[ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
[100%] Linking CXX static library libformatter.a
[100%] Built target formatter

```


# Задание 2

У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием `CMakeList.txt` для статической библиотеки formatter, ваш руководитель поручает заняться созданием `CMakeList.txt` для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```
Содержимое файла CMakeLists.txt:


```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(formatter_ex)

add_library(formatter_ex STATIC formatter_ex.cpp)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter)
target_include_directories(formatter_ex PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex formatter)
```

- Команда add_subdirectory(../formatter_lib formatter) включает в сборку директорию с библиотекой formatter
- Команда target_link_libraries(formatter_ex formatter) связывает библиотеку formatter с formatter_ex


```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add formatter_ex.h
$ git commit -m "added formatter_ex.h"
$ git push origin lab
$ git add formatter_ex.cpp
$ git commit -m "added formatter_ex.cpp"
$ git push origin lab
```

```
[lab be466e5] added CMakeLists.txt
 1 file changed, 9 insertions(+)
 create mode 100644 formatter_lib/CMakeLists.txt
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 522 bytes | 522.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   d9b725b..be466e5  lab -> lab
[lab 8c9ee1d] added formatter.h
 1 file changed, 5 insertions(+)
 create mode 100644 formatter_lib/formatter.h
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 445 bytes | 445.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   be466e5..8c9ee1d  lab -> lab
[lab 05af4d6] added formatter.cpp
 1 file changed, 10 insertions(+)
 create mode 100644 formatter_lib/formatter.cpp
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 507 bytes | 507.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Adam-dunno/lab-03.git
   8c9ee1d..05af4d6  lab -> lab

```



Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```


```
-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/adam/lab-03/formatter_ex_lib/_build
[ 25%] Building CXX object formatter/CMakeFiles/formatter.dir/formatter.cpp.o
[ 50%] Linking CXX static library libformatter.a
[ 50%] Built target formatter
[ 75%] Building CXX object CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[100%] Linking CXX static library libformatter_ex.a
[100%] Built target formatter_ex

```


# Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек. Чтобы продемонстрировать как работать с библиотекой `formatter_ex`, вам необходимо создать два `CMakeList.txt` для двух простых приложений:

- `hello_world`, которое использует библиотеку `formatter_ex`;
- `solver`, приложение которое испольует статические библиотеки `formatter_ex` и `solver_lib`

Удачной стажировки!

### solver.cpp

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```


Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_lib)

add_library(solver_lib STATIC solver.cpp)
target_include_directories(solver_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```



```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add solver.h
$ git commit -m "added solver.h"
$ git push origin lab
$ git add solver.cpp
$ git commit -m "added solver.cpp"
$ git push origin lab
```



```

[lab 370cfac] added CMakeLists.txt
 1 file changed, 9 insertions(+)
 create mode 100644 solver_lib/CMakeLists.txt
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 507 bytes | 169.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   99bd5a2..370cfac  lab -> lab
[lab b2513f8] added solver.h
 1 file changed, 3 insertions(+)
 create mode 100644 solver_lib/solver.h
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 395 bytes | 395.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   370cfac..b2513f8  lab -> lab
[lab 8124c3a] added solver.cpp
 1 file changed, 16 insertions(+)
 create mode 100644 solver_lib/solver.cpp
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 562 bytes | 562.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   b2513f8..8124c3a  lab -> lab



```




Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```



```

-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/adam/lab-03/solver_lib/_build
[ 50%] Building CXX object CMakeFiles/solver_lib.dir/solver.cpp.o
[100%] Linking CXX static library libsolver_lib.a
[100%] Built target solver_lib



```




### solver_example

```
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(solver_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib ${CMAKE_CURRENT_BINARY_DIR}/solver_lib)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)

add_executable(example equation.cpp)

target_link_libraries(example solver_lib formatter_ex)
```



```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add equation.cpp
$ git commit -m "added equation.cpp"
$ git push origin lab
```


```

[lab 7d72f39] added CMakeLists.txt
 1 file changed, 13 insertions(+)
 create mode 100644 solver_application/CMakeLists.txt
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 558 bytes | 558.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   8124c3a..7d72f39  lab -> lab
[lab 8ecbb04] added equation.cpp
 1 file changed, 30 insertions(+)
 create mode 100644 solver_application/equation.cpp
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 578 bytes | 578.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   7d72f39..8ecbb04  lab -> lab


```




Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```




```

-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/adam/lab-03/solver_application/_build
[ 12%] Building CXX object formatter_ex/formatter/CMakeFiles/formatter.dir/formatter.cpp.o
[ 25%] Linking CXX static library libformatter.a
[ 25%] Built target formatter
[ 37%] Building CXX object solver_lib/CMakeFiles/solver_lib.dir/solver.cpp.o
[ 50%] Linking CXX static library libsolver_lib.a
[ 50%] Built target solver_lib
[ 62%] Building CXX object formatter_ex/CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[ 75%] Linking CXX static library libformatter_ex.a
[ 75%] Built target formatter_ex
[ 87%] Building CXX object CMakeFiles/example.dir/equation.cpp.o
[100%] Linking CXX executable example
[100%] Built target example


```

Демонстрируем исполнение программы:
```
$ cmake --build _build --target example
$ ./_build/example
```


```

Consolidate compiler generated dependencies of target formatter
[ 25%] Built target formatter
Consolidate compiler generated dependencies of target solver_lib
[ 50%] Built target solver_lib
Consolidate compiler generated dependencies of target formatter_ex
[ 75%] Built target formatter_ex
Consolidate compiler generated dependencies of target example
[100%] Built target example



```




### hello_world.cpp

```
$ git checkout -b lab
$ cat >> CMakeLists.txt << EOF
> EOF
$ nano CMakeLists.txt
```

Содержимое файла CMakeLists.txt:

```
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(hello_world_example)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex_lib ${CMAKE_CURRENT_BINARY_DIR}/formatter_ex)
add_executable(example hello_world.cpp)

target_link_libraries(example formatter_ex)
```



```
$ git add CMakeLists.txt
$ git commit -m "added CMakeLists.txt"
$ git push origin lab
$ git add hello_world.cpp
$ git commit -m "added hello_world.cpp"
$ git push origin lab
```



```

[lab 69c8231] added CMakeLists.txt
 1 file changed, 11 insertions(+)
 create mode 100644 hello_world_application/CMakeLists.txt
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 3 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 555 bytes | 555.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   8ecbb04..69c8231  lab -> lab
[lab f24ca0e] added hello_world.cpp
 1 file changed, 8 insertions(+)
 create mode 100644 hello_world_application/hello_world.cpp
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 3 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 449 bytes | 449.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/Adam-dunno/lab-03.git
   69c8231..f24ca0e  lab -> lab


```



Проверяем работоспособность CMake:
```
$ cmake -H. -B_build
$ cmake --build _build
```



```
-- The C compiler identification is GNU 11.4.0
-- The CXX compiler identification is GNU 11.4.0
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/adam/lab-03/hello_world_application/_build
[ 16%] Building CXX object formatter_ex/formatter/CMakeFiles/formatter.dir/formatter.cpp.o
[ 33%] Linking CXX static library libformatter.a
[ 33%] Built target formatter
[ 50%] Building CXX object formatter_ex/CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
[ 66%] Linking CXX static library libformatter_ex.a
[ 66%] Built target formatter_ex
[ 83%] Building CXX object CMakeFiles/example.dir/hello_world.cpp.o
[100%] Linking CXX executable example
[100%] Built target example


```

Демонстрируем исполнение программы:
```
$ cmake --build _build --target example
$ ./_build/example
```




```

Consolidate compiler generated dependencies of target formatter
[ 33%] Built target formatter
Consolidate compiler generated dependencies of target formatter_ex
[ 66%] Built target formatter_ex
Consolidate compiler generated dependencies of target example
[100%] Built target example
-------------------------
hello, world!
-------------------------


```



