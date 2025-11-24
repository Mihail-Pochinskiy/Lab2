## Отчет по лабораторной работе № 1

#### № группы: `ПМ-2502`

#### Выполнил: `Починский Михаил Михайлович`

#### Вариант: `16`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Алгоритм](#3-алгоритм)
- [Программа](#4-программа)
- [Анализ правильности решения](#5-анализ-правильности-решения)

### 1. Постановка задачи

> #### Задача 1.
> Проанализоровать данную в задании последовательность, найти закономерность и написать алгорит для вывода первых n ее элементов

> #### Задача 2.
> Среди натуральных чисел, не превышающих 10<sup>6</sup>, найдите количество чисел, соответствующих маске “2*?7?”, которые имеют ровно 4 различных делителя."?" заменяет ровно одну любую цифру, "*" заменяет последовательность цифр любой длины (включая пустую последовательность)

> #### Задача 3.
> Число n называется счастливым, если при повторном вычислении суммы квадратов его цифр процесс в итоге приведет к 1. Если процесс никогда не достигает 1 и входит в цикл, число считается несчастливым. Определить, является ли заданное число n счастливым (выведите “YES”/“NO”)

> #### Задача 4.
> Дан массив из n чисел. Переставьте элементы так, чтобы все соседи имели разные остатки от деления на 3, и выведите получившуюся перестановку. Если это невозможно – выведите "NO"

### 2. Входные и выходные данные
#### Задача 1
    Данные на вход: натуральное число n
    Данные на выход: последовательность n элементов массива
  
#### Задача 2
    Данные на вход: отсутствуют
    Данные на выход: натуральное число - количество искомых чисел
  
#### Задача 3
    Данные на вход: натуральное число n
    Данные на выход: строка `YES` или `NO`
  
#### Задача 4
    Данные на вход: первая сторка - натуральное число n, вторая строка - n элементов массива
    Дынные на выход: последовательность n элементов массива

  
### 3. Алгоритм
#### Алгоритм выполнения задачи 1
1. Ввод данных:

   Программа считывает натуральное число - n
2. Анализ решения:

   Представим, что индексы начинаются с 2. Тогда на на месте с индексом m должен стоять наибольший простой делитель числа. В частном случае, если m - простое число, то будет стоять само m. Для этого, если m - составное число, ищем наибольший делитель числа и, если он простой, то возвращаем его, а если нет - повторяем данную операцию уже для него
3. Вывод результата:

   На экран выводится n первых чисел последовательности

#### Алгоритм выполнения задачи 2
1. Ввод данных:

   Входные данные отсутствуют
2. Анализ решения:

   Для того, чтобы число имело ровно 4 делителя, он должно иметь вид либо p<sup>3</sup> либо pq, где p и q - различные простые числа. Поэтому надо перебрать все простые числа до 100 и проверить, соответствует ли маске p<sup>3</sup>, а затем перебрать все простые p до 10<sup>6</sup> и для каждого из них перебрать все простые q меньшие p, так, чтобы pq было меньше 10<sup>6</sup> и проверить, удовлетворяют ли маске pq.
3. Вывод результата:

   На экран выводится n - количество чисел, удовлетворяющих маске

#### Алгоритм выполнения задачи 3
1. Ввод данных:

   Программа считывает натуральное число - n
2. Анализ решения:

   Будем считать, что n ≤ 2<sup>31</sup>-1. Тогда n имеет не более 10 разрядов, и, следовательно сумма квадратов цифр n не превосходит 10*9<sup>2</sup> < 1000. Значит, если цикл существует, то он гарантированно буде длины не более 1000. Тогда можно записывать значения, получаемые в результате нахождения суммы квадратов цифр числа, в массив длины  1001. И при очередной итерации проверять, равен ли результат 1. Если да - вывести `YES`, иначе - проверить, встречалось ли это значение ранее. Если да - мы попали в цикл, и выводим `NO`, если нет - продолжаем дальше.
3. Вывод результата:

   На экран выводится строка `YES` или `NO`

#### Алгоритм выполнения задачи 4
1. Ввод данных:

   Программа считывает натуральное число - n, затем массив n целых чисел
2. Анализ решения:

   Найдем количество каждого из остатков по модулю 3. Если максимум из них больше, чем целая часть от $\frac{n+1}{2}$, то выполнить перестановку невозможно. В обратном случае, на первое место ставим первое число, дающее остаток по модулю 3, равный наиболее встечающемуся в массиве, а остальные места заполняем значениями массива длины n-1, который упорядочен аналогичным образом так, чтобы стоящий в нем на первом месте элемент имел отличный остаток по модулю 3.
3. Вывод результата:

   На экран выводится массив n элементов отсортированного массива или строка `NO`


### 4. Программа
#### Задача 1
```java
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;

    public static void main(String[] args) {
        int n= in.nextInt();

        for (int i=0; i<n; i++){
            System.out.print(maxDivisor(i+2) + " ");
        }
    }

    public static int maxDivisor(int n){
        for (int i=n/2; i>1; i--){
            if (n%i==0)
                return maxDivisor(i);
        }
        return n;
    }
}
```

#### Задача 2
```java
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;
    public static int [] primes= new int[80000];

    public static void main(String[] args) {
        primes();

        int kNumbers=0;
        int limit1=100;
        int limit2=1;
        for (int i=0; i<6; i++)
            limit2*=10;

        for (int i=0; primes[i]<limit1; i++){
            int cube=i*i*i;
            String s= ""+cube;
            if (cube>2000 && s.charAt(0)=='2' && s.charAt(s.length()-1)=='7')
                kNumbers++;
        }
        for (int i=0; primes[i]!=0 && primes[i]<limit2; i++){
            int p=primes[i];
            for (int j=0; j<i; j++){
                int prod=p*primes[j];
                String s= ""+prod;
                if (prod>2000 && prod<limit2 && s.charAt(0)=='2' && s.charAt(s.length()-1)=='7')
                    kNumbers++;
            }
        }

        System.out.println(kNumbers);
    }

    public static void primes(){
        int limit=1;
        for (int i=0; i<6; i++)
            limit*=10;
        for (int i=0; i<80000; i++)
            primes[i]=0;

        int kPrimes=1;
        primes[0]=2;
        for (int i=3; i<=limit; i+=2){
            boolean fl=false;
            for (int j=0; !fl && j<kPrimes; j++)
                fl=(i%primes[j]==0);
            if (!fl){
                primes[kPrimes]=i;
                kPrimes++;
            }
        }
    }
}
```

#### Задача 3
```java
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;

    public static void main(String[] args) {
        int n= in.nextInt();
        int [] value = new int[1001];
        for (int i=0; i<1001; i++)
            value[i]=0;
        value[0]=n;
        boolean fl=true;
        for (int i=1; fl && i<1001; i++){
            n=squareDigitsOfNumber(n);
            if (n==1){
                System.out.println("YES");
                break;
            }
            else {
                for (int j=0; fl && j<i; j++)
                    fl=(value[j]!=n);
            }

            if (fl)
                value[i]=n;
        }
        if (!fl)
            System.out.println("NO");
    }

    public static int squareDigitsOfNumber(int n){
        int ans=0;
        while (n>0){
            int ost=n%10;
            ans+=(ost*ost);
            n/=10;
        }
        return ans;
    }
}
```

#### Задача 4
```java
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;

    public static void main(String[] args) {
        int n= in.nextInt();
        int [] mas= new int[n];
        for (int i=0; i<n; i++)
            mas[i]= in.nextInt();

        int [] ost= new int[3];
        for (int i=0; i<n; i++)
            ost[mas[i]%3]++;
        int max=0;
        if (ost[1]>ost[max])
            max=1;
        if (ost[2]>ost[max])
            max=2;

        if (ost[max]>(n+1)/2)
            System.out.println("NO");
        else {
            int [] sortMas=sortMassiveMod3(mas, -1);
            for (int i=0; i<n; i++)
                mas[i]=sortMas[i];

            for (int i=0; i<n; i++)
                System.out.print(mas[i] + " ");
        }
    }

    public static int [] sortMassiveMod3(int [] massive, int lastOst){
        int n= massive.length;
        System.out.println();
        if (n==1)
            return massive;

        int [] ost= new int[3];
        for (int i=0; i<n; i++)
            ost[massive[i]%3]++;
        int max=0;
        if (ost[1]>ost[max] && lastOst!=1)
            max=1;
        if (ost[2]>ost[max] && lastOst!=2)
            max=2;
        if (lastOst==max){
            if (ost[1]>ost[2])
                max=1;
            else
                max=2;
        }

        int [] ans= new int[n];
        int [] rec= new int [n-1];
        boolean fl=false;
        for (int i=0; i<n; i++){
            if (massive[i]%3!=max || fl){
                if (fl)
                    rec[i-1]=massive[i];
                else
                    rec[i] = massive[i];
            }
            else {
                ans[0]=massive[i];
                fl=true;
            }
        }
        rec= sortMassiveMod3(rec, ans[0]%3);

        for (int i=0; i<n-1; i++)
            ans[i+1]=rec[i];

        return ans;
    }
}
```

### 5. Анализ правильности решения
#### Задача 1
    Input: 10
    Output: 2 3 2 5 3 7 2 3 5 11 

    Input: 20
    Output: 2 3 2 5 3 7 2 3 5 11 3 13 7 5 2 17 3 19 5 7 

#### Задача 2
    Input: -
    Output: 19665

#### Задача 3
