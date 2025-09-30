# Лабораторная работа №2
## Тема лабораторной работы: Структуры
##  Задача 1- создать структуру с указателем на функцию
### Постановка задачи:
Создайте структуру, одно из полей которой является указателем на функцию. Вызовите эту функцию через имя переменной структуры и поле указателя на функцию
### Математическая модель 
Отсутствует
### Список идентификаторов

|    Имя    |     Тип      |                                       Смысл                                            |
|-----------|--------------|----------------------------------------------------------------------------------------|
| student1  |struct Student|                Переменная, являющаяся единичным экземпляром структуры Student          |
|    old    |      int     |                           Год рождения (промежуточная переменная)                      |
|    res    |      int     |Результирующая переменная, в которой происходит вызов функциичерез указатель в структуре|
### Код программы
```c
#include <stdio.h>
int date_of_birth(int a)
{
    int b=2025;
    return b-a;
}
struct Student
    {
        char first_name[20];
        char second_name[20];
        int (*age)(int);//указатель на функцию
    };

int main(void)
{
    struct Student student1=
    {
        .first_name=("Ольга"),
        .second_name=("Петрова"),
        .age=date_of_birth
    };
    int old=1980;
    int res=student1.age(old);//вызов функции через указатель в структуре
    printf("Имя и фамилия: %s,%s\n",student1.first_name,student1.second_name);
    printf("Возраст: %d\n",res);
    return 0;
}
```
### Результаты выполненной работы
<img width="301" height="93" alt="1" src="https://github.com/user-attachments/assets/c8b38f6f-a778-4c38-a15c-a5e37356ea59" />

##  Задача 2- структура для вектора в трёхмерном пространстве
### Постановка задачи:
 Реализуйте структуру для вектора в 3D пространстве и добавьте следующие функции:
 • Скалярное умножение векторов;
 • Векторное произведение;
 • Модуль вектора;
 • Распечатка вектора.
 Вструктуре также должно быть поле для хранения имени вектора
### Математическая модель 


Скалярное произведение векторов: 

<img width="302" height="51" alt="Cpr" src="https://github.com/user-attachments/assets/9c85f446-3723-4815-a413-b2d71186ed6c" />

Векторное произведение:  

<img width="532" height="41" alt="Vpr" src="https://github.com/user-attachments/assets/86127e46-5a22-40d0-95aa-741c3e5e1129" />

где a,b - вектора, а нижние индексы 1 и 2 соответсвиуют координатам a и b соотсветственно. Данную формулу можно вывести, если представить координаты в определитель.В отчете представлен конечный вариант формулы.

Модуль вектора: 
<img width="185" height="32" alt="mod" src="https://github.com/user-attachments/assets/8ab24574-fda3-4830-bae9-77634258d2b9" />

### Список идентификаторов
|    Имя    |     Тип      |                                       Смысл                                            |
|-----------|--------------|----------------------------------------------------------------------------------------|
|     v1    |struct Vector |                Переменная, являющаяся единичным экземпляром структуры Vector           |
|     v2    |struct Vector |                Переменная, являющаяся единичным экземпляром структуры Vector           |
|     v3    |struct Vector |Локальная переменная, являющаяся единичным экземпляром структуры Vector в ф-ции vect_pr |
| xc,yc,zc  |    double    |                 Локальные переменные вектора в ф-ции mod_vect                          |
| res_scl_pr|    double    |        Результирующая переменная скалярного произведения 2-х векторов                  |
|  res_mod  |    double    |                      Результирующая переменная модуля вектора                          |

### Код программы
```c
#include <stdio.h>
#include <math.h>

struct Vector
{
    char name[20];
    double x,y,z;
};
double scl_pr(struct Vector v1,struct Vector v2)
{
    return v1.x*v2.x+v1.y*v2.y+v1.z*v2.z;
}
struct Vector vect_pr(struct Vector v1,struct Vector v2)
{
    struct Vector v3={"EF",
        (v1.y*v2.z-v2.y*v1.z),
        (v1.x*v2.z-v2.x*v1.z),
        (v1.x*v2.y-v2.x*v1.y)
    };
    return v3;
}
double mod_vect(struct Vector v)
{
    double xc=v.x;
    double yc=v.y;
    double zc=v.z;

    return sqrt(xc*xc+yc*yc+zc*zc);
}
struct Vector pechat (struct Vector v)
{
    printf("Координаты вектора %s равны (%lf, %lf, %lf)\n",v.name,v.x, v.y, v.z);
}
int main(void)
{
    struct Vector v1={"AB",1.0,2.5,3.6};
    struct Vector v2={"CD",3.5,4.2,0.0};

    double res_scl_pr=scl_pr(v1,v2);
    struct Vector v3=vect_pr(v1,v2);
    double res_mod=mod_vect(v1);
    
    printf("Cкалярное произвдение векторов AB,CD равно: %lf\n",res_scl_pr);
    printf("Векторное произвдение векторов AB,CD равно %s координаты (%lf, %lf, %lf) \n",v3.name,v3.x,v3.y,v3.z);
    printf("Модуль вектора AB равен:  %lf\n",res_mod);
    pechat (v1);
    pechat (v2);

    return 0;
}
```
### Результаты

<img width="893" height="157" alt="2" src="https://github.com/user-attachments/assets/f6edb551-f824-480c-9d62-e07b08f71f54" />

## Задача 3- вычисление комплексной экспоненты
### Постановка задачи:
Используя структуру для представления комплексного числа,вычислите комплексную экспоненту e^z для числа 𝑧 ∈ ℂ.
Формула экспоненты
<img width="320" height="66" alt="Ф1" src="https://github.com/user-attachments/assets/c3253d3d-ce87-4a0b-9b2a-65f7a33415e2" />

### Математическая модель 
<img width="320" height="66" alt="Ф1" src="https://github.com/user-attachments/assets/b719d279-f00b-4495-bc78-7a8c94d21b62" />
Сложение двух комплексных чисел

<img width="272" height="37" alt="С1" src="https://github.com/user-attachments/assets/07db752c-4700-46c9-a2d7-0a2c52251f71" />

Умножение двух комплексных чисел

<img width="346" height="42" alt="У1" src="https://github.com/user-attachments/assets/c0d4d338-f140-4ab5-a175-cea5ac05dd6b" />

Умножение скаляра и комплексного числа

<img width="172" height="51" alt="У2" src="https://github.com/user-attachments/assets/9a9af70b-ed8a-4dac-bd38-c998c3497108" />


### Список идентификаторов
|    Имя    |     Тип      |                                                   Смысл                                                    |
|-----------|--------------|------------------------------------------------------------------------------------------------------------|
|     res   |struct Complex|Локальная переменная (результирующая) для разных функций, являющаяся единичным экземпляром структуры Complex|
|     res   |struct Complex|                    Переменная (результат), являющаяся единичным экземпляром структуры Complex              |
|     z     |struct Complex|                            Переменная, являющаяся единичным экземпляром структуры Complex                  |
|     els   |    int       |                             Локальная переменная (всего количество повторений) в ф-ции expon               |
|     el    |struct Complex|                     Локальная переменная единичный экземпляр структуры Complex                             |
|     sm    |struct Complex|                     Локальная переменная единичный экземпляр структуры Complex (сумма)                     |
|     n     |    int       |                          Переменная, означающая точность полученного результата                            |

### Код программы
```c
#include <stdio.h>

struct Complex
{
    double dey;
    double mni;
};

struct Complex sum (struct Complex a,struct Complex b)
{
    struct Complex res={a.dey+b.dey,a.mni+b.mni};
    return res;
}

struct Complex prois (struct Complex a,struct Complex b)
{
    struct Complex res={a.dey*b.dey-a.mni*b.mni, a.dey*b.mni+b.dey*a.mni};
    return res;
}

struct Complex scal_prois (struct Complex a,double n)
{
    struct Complex res={a.dey*n, a.mni*n};
    return res;
}

struct Complex expon(struct Complex z,int els)
{
    struct Complex sm={1.0, 0.0};//создаем сумму, начальное значение которой 1(по формуле)
    struct Complex el={1.0, 0.0};//следующий элемент последовательности вида: z^n/n!(мы в цикле n==1 возьмем)
    for (int n=1;n<els;n++)
    {
        el=prois(z,el);
        el=scal_prois(el,(float)1/(float)n);
        sm = sum(sm,el);

    }
    return sm;
}

int main (void)
{
    struct Complex z,res;
    int n=30;//число элементов ряда

    printf("Введите действ.  и мнимую части числа z:\n");
    scanf("%lf %lf", &z.dey,&z.mni)!=2;
    res=expon(z,n);

    printf("e^(%.6f+%.6fi)=%.6f+%.6fi\n",z.dey,z.mni,res.dey,res.mni);
    return 0;

}
```
### Результат

<img width="496" height="106" alt="3" src="https://github.com/user-attachments/assets/feb98291-f608-4788-9388-8d9a3a58d62f" />

##  Задача 4- Структура с битовыми полями для даты
### Постановка задачи:
Используя битовые поля в структуре C, создайте структуру для хранения даты (например, даты рождения)
### Математическая модель 
Отсутствует
### Список идентификаторов
|    Имя    |     Тип      |                                                   Смысл                                                    |
|-----------|--------------|------------------------------------------------------------------------------------------------------------|
|   birth   |struct Complex|                            Переменная, являющаяся единичным экземпляром структуры Complex                  |

### Код программы
```c
#include <stdio.h>
struct date
{
   unsigned day: 5;
   unsigned month :4;
   unsigned year: 20;
};

int main(void)
{
    struct date birth={31,1,2007};
    printf ("%d, %d, %d", birth.day,birth.month,birth.year);
    return 0;
}
```

### Результаты
<img width="315" height="67" alt="4" src="https://github.com/user-attachments/assets/36ad02d2-8275-4223-b02a-f27d11d9c37a" />

##  Задача 5- реализация двусвязного списка
### Постановка задачи:
Реализуйте структуру и функции для создания и наполнения двусвязного списка, а также функции для его обхода и
 распечатки:
 • Прямой обход списка с выводом значений;
 • Обратный обход списка с выводом значений.
 Это сложная задача- код нужно написать в общем виде, используя указатели void * на произвольные данные, хра
нимые в узлах списка.
### Математическая модель 
Отсутсвует
### Список идентификаторов
| Имя |Тип|Смысл|
|-----|-------------|-----|
|*list|struct Spicok|Переменная, являющаяся ссылкой на кокнкретный единичный экземпляр структцры Spicok|
|  a  |    int      |                Переменная, которая является узлом двусвязного списка             |
|  b  |     int     |                Переменная, которая является узлом двусвязного списка             |
|  c  |     int     |                Переменная, которая является узлом двусвязного списка             |
| *s1 |    char     |                Переменная, которая хранит адрес узла двусвязного списка          |
| *s2 |    char     |                Переменная, которая хранит адрес узла двусвязного списка          |

### Код программы
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Spicok //Структура узла двусвязного списка
{
    void *note;//ссылка текущий узел
    struct Spicok *before;//ссылка на следующий узел
    struct Spicok *next;//ссылка на предыдущий узел
};

struct Spicok* create(void *note, size_t note_size)//создание нового узла с копией данных
{
    struct Spicok *newNote=(struct Spicok*) malloc (sizeof(struct Spicok));
    if (!newNote) return NULL;

    newNote->note=malloc(note_size);
    if (!(newNote->note))
    {
        free(newNote);
        return NULL;
    }

    for (size_t i=0;i<note_size;i++)//Копия данных в новую память
    {
        ((char*)newNote->note)[i]=((char*)note)[i];
    }
    newNote->before=NULL;
    newNote->next=NULL;

    return newNote;
}

void addNote(struct Spicok **head,void *note,size_t note_size)
{
    struct Spicok *newNote=create(note,note_size);
    if (!newNote) return;

    if (*head==NULL)
    {
        *head=newNote;
        return;
    }

    struct Spicok *temp=*head;
    while (temp->next!=NULL)
    {
        temp=temp->next;
    }
    temp->next=newNote;
    newNote->before=temp;
}

//Функция осовобождения памяти списка
void freeList(struct Spicok **head)
{
    struct Spicok *temp=*head;
    while (temp!=NULL)
    {
        struct Spicok *next=temp->next;
        free(temp->note);
        free (temp);
        temp=next;
    }
    *head=NULL;
}

//Пример функции печати для int
void printInt(void *note)
{
    printf("%d ", *(int*)note);
}

//Пример функции печати для строки
void printString (void *note)
{
    printf("%s ",(char*)note);
}
//Пример использования

void forwardTraversal(struct Spicok *head, void (*printFunc)(void *)) {
    struct Spicok *temp = head;
    while (temp) {
        printFunc(temp->note);
        temp = temp->next;
    }
    printf("\n");
}

// Обратный проход: от конца к голове
void backwardTraversal(struct Spicok *head, void (*printFunc)(void *)) {
    if (!head) return;

    struct Spicok *temp = head;
    // Найти последний элемент
    while (temp->next) {
        temp = temp->next;
    }
    // Идти назад по before
    while (temp) {
        printFunc(temp->note);
        temp = temp->before;
    }
    printf("\n");
}

int main(void)
{
    struct Spicok *list=NULL;

    int a=10,b=20,c=30;
    addNote(&list,&a,sizeof(int));
    addNote(&list,&b,sizeof(int));
    addNote(&list,&c,sizeof(int));


    printf("Прямой проход строк: ");
    forwardTraversal(list, printInt);

    printf("Обратный проход строк: ");
    backwardTraversal(list, printInt);
    
    freeList(&list);

    char *s1="Hello";
    char *s2="World";
    addNote(&list,s1,strlen(s1)+1);
    addNote(&list,s2,strlen(s2)+1);

     printf("Прямой проход строк: ");
    forwardTraversal(list, printString);

    printf("Обратный проход строк: ");
    backwardTraversal(list, printString);
    
    freeList(&list);

    return 0;
}
```
### Результаты
<img width="348" height="133" alt="5" src="https://github.com/user-attachments/assets/65339484-2af2-4006-969c-6d1adbea368d" />


### Информация об обучающемся: Федькина Полина Дмитриевна, группа ПОО, 1 курс.


