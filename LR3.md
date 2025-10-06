# Лабораторная работа №3
## Тема лабортатоной работы: Объединения и перечисления
##  Задача 1- указатель на объединение
### Постановка задачи
Напишите программу, которая использует указатель на некоторое объединение (union). Создайте и проинициализи
руйте переменные в объединении через указатель, затем выведите их значения на экран.
### Математическая модель 
Отсутствует
### Список идентификаторов
| Имя |Тип|Смысл|
|-----|---|-----|
|user1|union User|Экземпляр объединения User|
### Код программы
```c
#include <stdio.h>
int birth(int x)
{
    return 2025-x;
}

union User
{
    char name[20];
    char surname[20];
    int (*year)(int);//указатель на функцию
};

int main(void)
{
    
    union User user1;
    // Инициализируем поле name
    snprintf(user1.name,sizeof(user1.name),"Ольга");
    printf("Имя: %s\n",user1.name);

    snprintf(user1.surname,sizeof(user1.surname),"Петрова");
    printf("Фамилия: %s \n",user1.surname);

    user1.year=birth;

    int age=1956;
    int res=user1.year(age);//Вызов функции через указатель
    printf("Возраст:%d\n",res);

    return 0;
}
```
### Результаты
<img width="307" height="153" alt="1" src="https://github.com/user-attachments/assets/92c1de39-8ad4-4ed7-a000-428c414a05f1" />

##  Задача 2- побайтовая распечатка числа
### Постановка задачи
 Напишите программу,которая использует объединение(union)для побайтовой распечатки значения переменной типа
 unsigned long. Каждый байт должен быть выведен отдельно через указатель на char.
### Математическая модель
Отсутствует
### Список идентификаторов
| Имя |Тип|Смысл|
|-----|---|-----|
|data|union BytePr|Экземпляр объединения BytePr|
|*str|unsigned char|Строка -указатель, хранящая ссылку на значение тип строка|
### Код программы
```c
#include <stdio.h>
union BytePr
{
    unsigned long  val;
    unsigned char bytes[sizeof(unsigned long)];
};

int main (void)
{
    union BytePr data;
    data.val =0x123456;//Пример значения

    unsigned char *str=(unsigned char *)&data.val;//строка-указатель, хранящая ссылку на значение типа строка

    printf("Побайтовое представление unsigned long (size = %zu байт): \n",sizeof(unsigned long));
    for (size_t i=0; i<sizeof(unsigned long); i++)
    {
        printf("Byte %zu: 0x%02X\n",i,*(str+i));
    }
    return 0;
}
```
### Результаты
<img width="515" height="142" alt="2" src="https://github.com/user-attachments/assets/8f61166d-faf8-4260-872d-99c1b5483951" />

## Задача 3- перечисление дней недели
### Постановка задачи:
 Создайте перечислимый тип данных (enum) для семи дней недели. Реализуйте программу, которая выводит на экран
 значения каждого дня недели как целое число.
### Математическая модель 
 Отсутствует
### Список идентификаторов
Отсутсвует
### Код программы
```c
#include <stdio.h>
enum DayOfWeek
{
    Monday=1,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday,
    Sunday
};

int main(void)
{
    printf("Monday: %d \n", Monday);
    printf("Tuesday: %d \n", Tuesday);
    printf("Wednesday: %d \n", Wednesday);
    printf("Thursday: %d \n", Thursday);
    printf("Friday: %d \n", Friday);
    printf("Saturday: %d \n", Saturday);
    printf("Sunday: %d \n", Sunday);

    return 0;
}
```
### Результаты
<img width="310" height="217" alt="3" src="https://github.com/user-attachments/assets/3da00d49-dd59-4480-ba67-6aa37499a87e" />
## Задача 4- размеченное объединение
### Постановка задачи:
 Создайте размеченное объединение (union), которое заключено в структуру. Структура должна также содержать пе
речисление (enum), служащее индикатором того, какой тип данных хранится в объединении на текущий момент. Со
здайте динамический массив таких структур и реализуйте функцию для распечатки их содержимого на экран.
### Математическая модель
Отсутствует
### Список идентификаторов
| Имя |Тип|Смысл|
|-----|---|-----|
|array|struct TaggedUnion|Экземпляр структуры TaggedUnion|
|size|size_t|Количество элементов массива|

### Код программы
```c
#include <stdio.h>
#include <stdlib.h>
// Перечисление для индикации типа данных в объединении
typedef enum
{
    TYPE_INT,
    TYPE_FLOAT,
    TYPE_CHAR
} DataType;

// Объединение с разными типами данных
typedef union 
{
    int i;
    float f;
    char c;
} DataUnion;

// Структура, содержащая объединение и индикатор типа
typedef struct
{
    DataType type;
    DataUnion data;
}TaggedUnion;

// Функция для печати содержимого массива структур
void printTaggedUnionArray(TaggedUnion* arr,size_t size)
{
    for (size_t i=0;i<size;i++)
    {
        printf("Элемент %zu: ",i);
        switch (arr[i].type)
        {
            case TYPE_INT:
                printf("int=%d\n", arr[i].data.i);
                break;
            case TYPE_FLOAT:
                printf("float=%f\n",arr[i].data.f);
                break;
            case TYPE_CHAR:
                printf("char=%c\n",arr[i].data.c);
                break;
            default:
                printf("неизвестный тип\n");
        
        }
    }
}

int main(void)
{
    size_t size=5;

    //Динамическое выделение массива
    TaggedUnion* array=malloc(size*sizeof(TaggedUnion));
    if (!array) {
        perror("malloc failed");
        return 1;
    }

    // Инициализация элементов массива
    array[0].type=TYPE_INT; array[0].data.i=42;
    array[1].type=TYPE_FLOAT; array[1].data.f=3.14f;
    array[2].type=TYPE_CHAR; array[2].data.c='z';
    array[3].type = TYPE_INT;   array[3].data.i = -7;
    array[4].type = TYPE_CHAR;  array[4].data.c = 'z';

    // Печать содержимого
    printTaggedUnionArray(array,size);

    // Освобождение памяти
    free(array);
    return 0;
}
```
### Результаты
<img width="327" height="181" alt="4" src="https://github.com/user-attachments/assets/13227b86-e008-439e-ba3c-dd945a94654e" />
## Задача 5- ввод и хранение данных о студентах
### Постановка задача:
 Создайте структуру, в которой используется объединение для хранения различных типов данных: например, структу
ра с отдельным полем для имени студента и отдельное поле– целое число для его возраста либо строка его возраста
 словами. Реализуйте программу для динамического ввода данных о студентах и вывода их на экран
 ### Математическая модель
 Отсутсвует
 ### Список идентификаторов
 ### Код программы
 ### Результат
 
## Задача 6- управление состояниями системы через enum
### Постановка задача:
 Используйте перечисление (enum) для управления состояниями некоторой условной системы, например, старт, стоп,
 пауза. Напишите программу, которая изменяет состояние системы и выводит текущее состояние на экран.
 ### Математическая модель
 Отсутсвует
 ### Список идентификаторов
| Имя |Тип|Смысл|
|-----|---|-----|
|currentState|enum State|Экземпляр перечисления State|
 ### Код программы
 ```c
#include <stdio.h>

// Объявление перечисления для состояний системы
typedef enum
{
    START,
    STOP,
    PAUSE
} State;

// Функция для вывода текстового описания состояния
void printState(State state)
{
    switch(state)
    {
        case START:
            printf("Состояние: START (старт)\n");
            break;
        case STOP:
            printf("Состояние: STOP (стоп)\n");
            break;
        case PAUSE:
            printf("Состояние: PAUSE (пауза)\n");
            break;
        default:
        printf("Неизвестное состояние\n");
    }
}
int main(void)
{
    State currentState=STOP;// начальное состояние

    printState (currentState);

    // Изменяем состояние на старт
    currentState=START;
    printState(currentState);

    // Изменяем состояние на паузу
    currentState = PAUSE;
    printState(currentState);

    // Изменяем состояние на стоп
    currentState = STOP;
    printState(currentState);

    return 0;
}

```
 ### Результат
 
 <img width="301" height="170" alt="6" src="https://github.com/user-attachments/assets/24012cdd-a003-4814-aefb-0e638c455bf7" />





