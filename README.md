# Практическая работа 1
## Информация о студенте
### Федькина Полина Дмитриевна 1 курс, ПОО (Информатика и искусственный интеллект в образовании)
## Установка рабочей среды
<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/71c5a871-82bb-431c-a6f7-39a26bb3c227" >

## Задача 1
### Текст программы
```C
#include <math.h>
#include <stdio.h>
int main(void)
{
    const double PI= 3.1415926;
    double r1 = 1.524;/*радиус орбиты Марса астрономичеких единиц*/
    double r2 = 1.0;/*радиус орбиты Земли в астрономических единицах*/
    double T1=687.0;/*период обращения Марса вокруг Солнца в сутках*/
    double T2=365.256;/*период обращения Земли вокруг Солнца в сутках*/
    double w1=2.0*PI/T1;
    double w2=2.0*PI/T2;
    double t0 = 0.0;/*в днях*/
    double tizm=10.0;/*дней*/
    for (double t=t0;t<=1000.0;t+=tizm)
    {
        double x=r1*cos(w1*t) - r2*cos(w2*t);
        double y=r1*sin(w1*t) - r2*sin(w2*t);
        printf("В момент времени %.1f сут. x=%.2f,\n",t,x);
        printf("y=%.2f.\n",y);
    }

    return 0;

}
```
### Результаты
<img width="337" height="487" alt="Image" src="https://github.com/user-attachments/assets/f74ec542-cc67-4bcf-afcd-390e8aec6d5c" />

## Задача 2.1
### Текст программы

```C
#include <stdio.h>
#include <math.h>
double f(double x)
{
    return exp(x+2.0);
}
int main(void)
{
    double a,b;
    int n;
    printf("Введите n,a,b: \n");
    scanf("%d",&n);
    scanf("%lf",&a);
    scanf("%lf",&b);
    if (a>b)
    {
        printf("ERROR\n");
        return 1;
        
    }
    if (n<=0)
    {
        printf("ERROR\n");
        return 1;
    }
    double h=(b-a)/n;
    printf("%f\n",h);
    double suma=0.5*(f(a)+f(b));
    for (double i=1;i<n;++i)
    {
        double x=a+i*h;
        suma+=f(x);
    }
    double integral=h*suma;
    printf("Приближенное значение интеграла = %15g\n",integral);
    return 0;
}
```
### Результат

<img width="1197" height="273" alt="Image" src="https://github.com/user-attachments/assets/ada28313-c2b9-4bc1-9a4d-fc7640ac6545" />

## Задача 2.2
### Текст программы
```C
#include <stdio.h>
#include <math.h>
double f (double x)
{
    return exp(x+2.0);
}
int main(void)
{
    double a,b;
    int n;

    printf("Введите n(четное),a,b\n");
    scanf("%d",&n);
    scanf("%lf",&a);
    scanf("%lf",&b);

    if (a>b)
    {
      printf ("ERROR\n");
      return 1;
    }
    
    if (n<=0)
    {
      printf ("ERROR\n") ; 
      return 1;
    }
    if (n%2!=0)
    {
      printf ("ERROR\n") ;
      return 1; 
    }
    double h=(b-a)/n;
    printf("%lf\n",h);
    double suma=f(a)+f(b);

    for (int i=1;i<n;i+=2)
    {
      double x=a+i*h;
      suma=suma+4.0*f(x);
    }
    for (int i=2;i<n;i+=2)
    {
        double x=a+i*h;
        suma=suma+2.0*f(x);
    }
    double integral=(h/3)*suma;
    printf("Значение интеграла: %15g",integral);
    return 0;
}
```

### Результат

<img width="1203" height="330" alt="Image" src="https://github.com/user-attachments/assets/4a116ffc-770d-4b86-ba14-136635637c20" />

## Задача 2.3
### Решение задачи аналитикой
$$\int_a^b e^{x+2} dx= F(b)-F(a)$$
$$\int_0^1 e^{x+2}= F(1)-F(0)=e^{1+2}-e^{2+0}=20.08554-7.38906=12.69648$$

## Задача 3
### Текст программы
```C
#include <stdio.h>
int p(int n)
{
    if ((n==0)||(n==1)||(n==2))
    {
        return 1;
    }
    else
    {
        return p(n-2)+p(n-3);
    }
}
int main(void)
{
    int m;
    printf("Напишите число m: \n");
    scanf("%d",&m);
    for (int i=0;p(i)<=m;i++)
    {
        printf(" %d ",p(i));
    }
    return 0;
}
```
### Результат

<img width="1193" height="218" alt="Image" src="https://github.com/user-attachments/assets/3cdcdc8d-bf3d-460c-8b41-45842d530c12" />


## Задача 4
### Текст программы
```C
#include <stdio.h>
int main (void)
{
    int sm=0;
    int num;
    printf("Введите num (положительное):\n");
    scanf("%d",&num);
    while (num>0)
    {
        sm+=num%10;
        num=num/10;
    }
    printf("%d",sm);
}
```
### Результат

<img width="1195" height="202" alt="Image" src="https://github.com/user-attachments/assets/5bdb04bf-ada0-4f40-b6e6-609424e5a8a0" />
 
## Задача 1. Массивы
### Текст программы
```C
#include <stdio.h>
int main (void)
{
    int x[2];
    int y[2];
    int a;
    int sm=0;
    int count=0;
    printf("Введите a,b: \n");

    for (int i=0;i<2;i++)
    {
        scanf("%d",&a);
        x[i]=a;
    }
    printf("x: ");
    for (int i=0;i<2;i++)
    {
            printf("%d ",x[i]);
    }
    printf("\ny: ");
    for (int i=0;i<2;i++)
    {
        y[i]=x[i]*x[i];
        sm=sm+y[i];
        
    }
    for (int i=0;i<2;i++)
    {
            printf("%d ",y[i]);
    }
    printf("Среднее арифметическое = %d\n",sm/2);
    for (int i=0;i<2;i++)
    {
        if (sm/2<y[i])
        {
            count=count+1;
        }
    }
    printf("Количество элементов, больших среднеарифметического: %d",count);
    return 0;
}
```
### Результат

<img width="1172" height="282" alt="Image" src="https://github.com/user-attachments/assets/2d77fded-7fa2-4837-8a57-8ae60e203021" />
 
## Задача 2. Массивы
### Текст программы
```C
#include <stdio.h>
int main(void)
{
    int num;
    float elem;
    printf("Введите кол-во элементов в массиве: \n");
    scanf("%d",&num);
    float x[num];
    float y[num];
    for (int i=0;i<num;i++)
    {
        printf("Введите элемент массива': \n");
        scanf("%f",&elem);
        x[i]=elem;
    }
    printf("\nСтарый массив: ");
    for (int i=0;i<num;i++)
    {
        printf("%f, ",x[i]);
    }
    for (int i=0;i<num;i++)
    {
        y[i]=x[num-i-1];
    }
    printf("\nНовый  массив: ");
    for (int i=0;i<num;i++)
    {
        printf("%f, ",y[i]);
    }
    return 0;
}
```
### Результат 

<img width="563" height="412" alt="Image" src="https://github.com/user-attachments/assets/123b2185-a745-4008-8307-19da06cb6eb4" />

## Задача 3. Массив
### Текст программы
```C
#include <stdio.h>
int main (void)
{
    int A[3][3]={{1,2,3},{4,5,6},{7,8,9}};
    int B[3][3]={{0,0,0},{0,0,0},{0,0,0}};
    for (int i=0;i<3;i++)
    {
        for (int j=0;j<3;j++)
        {
            B[j][i]=A[i][j];
        }
    }
    printf("A: \n");
    for (int i=0;i<3;i++)
    {
        for (int j=0;j<3;j++)
        {
            printf("%d ",A[i][j]);
        }
        putchar('\n');
    }
    printf("B: \n");
    for (int i=0;i<3;i++)
    {
        for (int j=0;j<3;j++)
        {
            printf("%d ",B[i][j]);
        }
        putchar('\n');
    }
    return 0;
}
```

### Результат 

<img width="292" height="297" alt="Image" src="https://github.com/user-attachments/assets/3f1d715a-4935-43b3-94db-af27415c27b0" />

## Задача 4 Массив
### Текст программы
```C
#include <stdio.h>
int main(void)
{
    int num;
    float elem;
    printf("Введите кол-во элементов в массиве: \n");
    scanf("%d",&num);
    float x[num];
    for (int i=0;i<num;i++)
    {
        printf("Введите элемент массива': \n");
        scanf("%f",&elem);
        x[i]=elem;
    }
    printf("\nСтарый массив: ");
    for (int i=0;i<num;i++)
    {
        printf("%f, ",x[i]);
    }
    for (int i=1;i<num;i++)
    {
        for (int j=i; j>0 && x[j-1]>x[j];j--)
        {
            int el=x[j-1];
            x[j-1]=x[j];
            x[j]=el;
        }
    }
    printf("\nОтсортированный массив: ");
    for (int i=0;i<num;i++)
    {
        printf("%f, ",x[i]);
    }
    return 0;
}
```
### Результат

<img width="637" height="408" alt="Image" src="https://github.com/user-attachments/assets/f0fccf52-4855-4599-bede-b51fac6c80a3" />

## Задача 5.1 Массив
### Текст программы
```C
#include <stdio.h>
int main (void)
{
    int num;
    int elem;
    printf("Введите кол-во элементов в массиве: \n");
    scanf("%d",&num);
    int x[num];
    int y[num];
    int k;
    for (int i=0;i<num;i++)
    {
        printf("Введите элемент массива': \n");
        scanf("%d",&elem);
        x[i]=elem;
    }
    printf("\nMассив: ");
    for (int i=0;i<num;i++)
    {
        printf("%d, ",x[i]);
    }
    for (int i=0;i<num;i++)
    {
        y[i]=x[num-1-i];
    }
    for (int i=0;i<num;i++)
    {
        if (y[i]==x[i])
        {
            k=k+1;
        }
    }
    if (k==num)
    {
        printf("Данный массив палиндром!\n");
    }
    else
    {printf("Данный массив НЕ является палиндромом!\n");}
}
```
### Результат

<img width="428" height="386" alt="Image" src="https://github.com/user-attachments/assets/d466d87a-e55d-4539-b8c1-16143f67a031" />

<img width="562" height="402" alt="Image" src="https://github.com/user-attachments/assets/5e3a4bcc-a733-49ec-874d-c8ccbbaafa2b" />


## Задание 5.2. Массив
### Текст программы
```C
#include <stdio.h>
int main (void)
{
    int num;
    int elem;
    printf("Введите кол-во элементов в массиве: \n");
    scanf("%d",&num);
    int x[num];
    for (int i=0;i<num;i++)
    {
        printf("Введите элемент массива': \n");
        scanf("%d",&elem);
        x[i]=elem;
    }
    printf("\nMассив: ");
    for (int i=0;i<num;i++)
    {
        printf("%d, ",x[i]);
    }
    for (int i=1;i<num;i++)
    {
        for (int j=i;j>0 && x[j-1]>x[j];j--)
        {
            int el=x[j-1];
            x[j-1]=x[j];
            x[j]=el;
        }
    }
    if (x[0]==x[num-1])
    {
        printf("Все числа в массиве одинаковы!\n");
    }
    else
    {
        printf("Втoрой по величине элемент в массиве: %d\n",x[num-2]);
    }
    return 0;
}
```
### Результат

<img width="582" height="401" alt="Image" src="https://github.com/user-attachments/assets/233b19b9-7ca9-4fba-aedf-9ad2b0dfeb2f" />

<img width="517" height="391" alt="Image" src="https://github.com/user-attachments/assets/e700786e-fb60-4799-9504-822465510733" />
