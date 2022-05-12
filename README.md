# -Understanding-JVM

## Код для исследования

```java
// После запуска программы класс JvmComprehension передаётся в подсистему загрузчиков класса ClassLoader
// и после успешной загрузки переместиться в Metaspace для хранения данных о классе JvmComprehension.
public class JvmComprehension {

    // В момент вызова метода main в Stack Memory создаётся новый фрейм main.
    public static void main(String[] args) {
        
        //1) В фрейме main создается переменная i типа int со значением 1.
        int i = 1;
        
        //2) В Heap (куче) создается объект типа Object а во фрейме main создается переменная o, 
        // которой присваивается ссылка на этот объект. 
        Object o = new Object(); 
        
        //3) В Heap (куче) создается объект типа Integer а во фрейме main создается переменная ii, 
        // которой присваивается ссылка на этот объект. 
        Integer ii = 2;    
        
        //4) В момент вызова метода printAll в Stack Memory создаётся новый фрейм printAll выше предыдущего,
        // в котором запишутся переменные Object o и Integer ii и передадутся ссылки на эти объекты из кучи,
        // и в фрейме printAll создасться переменная i типа int со значением 1.
        printAll(o, i, ii);    
        
        //7.1) В момент вызова метода println в Stack Memory создастся новый фрейм println выше предыдущего,
        // в котором запишется переменная String и передасться ссылка на этот объект из кучи со значением "finished".
        //7.2) После завершения метода println, фрейм println будет удалён из Stack Memory.
        System.out.println("finished"); 
        //7.3) После завершения метода main, фрейм main будет удалён из Stack Memory.
        
        // Удаление фреймов из Stack Memory происходит атвтомотически после завершения метода.
        // Удаление объектов из Heap (кучи) происходит с помощью Garbage Collector, по принципу подсчёта ссылок 
        // и обхода графа достижимых объектов. Обычно для сборки мусора происходит приостановка программы.
        // Garbage Collector выполняет свою работу на протяжении работы всей программы.
    }
    
    private static void printAll(Object o, int i, Integer ii) {
    
        //5) В Heap (куче) создается объект типа Integer а во фрейме printAll создается переменная uselessVar, 
        // которой присваивается ссылка на этот объект. 
        Integer uselessVar = 700;  
        
        //6.1) В момент вызова метода println в Stack Memory создастся новый фрейм println выше предыдущего,
        // в котором запишутся переменные Object o и Integer ii и передадутся ссылки на эти объекты из кучи,
        // и в фрейме printAll создасться переменная i типа int со значением 1.
        //6.2) В момент вызова метода toString в Stack Memory создастся новый фрейм toString выше предыдущего,
        // в котором запишется переменная Object o и передасться ссылка на этот объект из кучи,
        // после завершения метода toString, фрейм toString будет удалён из Stack Memory.
        //6.3) После завершения метода println, фрейм println будет удалён из Stack Memory.
        System.out.println(o.toString() + i + ii);  
        //6.4) После завершения метода printAll, фрейм printAll будет удалён из Stack Memory.
    }
}


```
