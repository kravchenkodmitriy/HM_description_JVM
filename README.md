# Описание строк кода со строны JVM

Пример кода:  

```java
    public class JvmComprehension {
    
    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
    }
```

```mermaid
flowchart TB  
    A[.java]--> B[javac 'java compiler']
    B[javac 'java compiler']==> C[.class 'байт-код']
    C[.class 'байт-код']==> D[JVM]
    D[JVM]==> E[Операционная система]
```
[![](https://mermaid.ink/img/pako:eNp9j01qwzAQha8iZuNNnAMYEmiabApdtXQjZTFIcuMi2UGWW0oINFl02xv0DC40kJb-XGF0o8jEWbYzi3m8-d7irUBWSkMGuake5AKdZ9cTUbI4Z3x4h_c4T9Mxm_BOSpZ0h8nKLgujXTI_kn99R6MxO-dDabCuWUJv1NJH2Kb0ST_0fgr_A3T5Kb-4uezRo-7cGadX-qVdeKI2PNM-8t9x2_DCwob2YRO2tKMvavskDMBqZ7FQseqq8wT4hbZaQBal0jk2xgsQ5TqizVKh1zNV-MpBlqOp9QCw8dXVYykh867RJ2ha4K1D21PrAwz5hfM)](https://mermaid-js.github.io/mermaid-live-editor/edit/#pako:eNp9j01qwzAQha8iZuNNnAMYEmiabApdtXQjZTFIcuMi2UGWW0oINFl02xv0DC40kJb-XGF0o8jEWbYzi3m8-d7irUBWSkMGuake5AKdZ9cTUbI4Z3x4h_c4T9Mxm_BOSpZ0h8nKLgujXTI_kn99R6MxO-dDabCuWUJv1NJH2Kb0ST_0fgr_A3T5Kb-4uezRo-7cGadX-qVdeKI2PNM-8t9x2_DCwob2YRO2tKMvavskDMBqZ7FQseqq8wT4hbZaQBal0jk2xgsQ5TqizVKh1zNV-MpBlqOp9QCw8dXVYykh867RJ2ha4K1D21PrAwz5hfM)

При запуске JVM происходит загрузка файлов Java в область памяти для 
дальнейшего его использования. Подается сигнал в ClassLoader который получает строку 
по которой можно распознать файл. По умолчанию сть 3 ClassLoader: 
1. Application ClassLoader
2. Platform ClassLoader
3. Bootstrap ClassLoader
  
Разбираемся по строкам пример который указан выше.
1. Подгружается класс в ClassLoader, далее выделяестя память в 
Metaspace (можно задать параметрами MetaspaceSize=N, MaxMetespace=N, по умолчанию размер не ограничен)
2. В момент вызова метода создается фрейм(кадр) в стеке
3. Метод main создает область в стеке (фрем в котором хранится все что происходит в текущем методе)
4. 1 строка ***"int i = 1;"*** занесение данных в Stack Memory.
5. 2 Строка выделение(резервирование) в куче(heap) места под объект. Далее
передается ссылка переменной "о" и занесении ее в стек.
6. 3 Строка ***"Integer ii = 2;"*** занесение данных в Stack Memory.
7. 4 Строка В момент вызова метода создается фрем в стеке.
8. 5 Строка ***"Integer uselessVar = 700;"*** занесение данных в Stack Memory.
9. 6 Строка создание нового фрейма в стеке куда передастся значение переменных.
10. 7 Строка создание нового фрейма в стеке куда будет передано значение переменной.



