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





