### Single-Responsibility Principle
Bir Sınıfın ya da fonksiyonun,metodun tek bir görevi, sorumluluğu olmalıdır. Başka sınıfların görevlerini gerçekleştirmemelidir.

### Open-Closed Principle
Open-Closed prensibi kısacası bir programın,applicationun veya objelerin ya da entitylerin geliştirilmeye açık ancak değiştirmeye kapalı olduğunu belirtir. İnterface ve abstract sınıflar kullanılarak istenen eklemeler yapılabilir.

### Liskov Substitution Principle

```java
using System;

namespace LiskovSubstitutionPrinciple
{
    public interface IAirConditionable
    {
        string OpenAirConditioning();
    }

    public abstract class Car
    {
        public string Run()
        {
            return "Araba çalıştırıldı.";
        }
    }

    public class Ferrari : Car, IAirConditionable
    {
        public string OpenAirConditioning()
        {
            return "Klima açıldı.";
        }
    }

    public class Murat131 : Car
    {
    }

}
Klima özelliğini sadece Ferrari için implemente ettiğimizden dolayı, hiç kimse Murat131 için OpenAirConditioning metotuna erişemiyecek ve herhangi bir problem ile karılaşılmayacaktır.
```

### Interface Segregation Principle
Nesneler, ihtiyaç duymadıkları metotların bulunduğu Interface’lere bağlı olmaya zorlanmamalıdır. 
Single Responsibility Principle ilkesinin Interface üzerine uygulanması!

<img align="center" width="400" height="500" src="https://www.turkayurkmez.com/wp-content/images/092613_1556_ArayzlerinA4.png">

### Dependency Inversion Principle
Üst seviye (High-Level) sınıflar alt seviye (Low-Level) sınıflara bağlı olmamalıdır, aralarındaki ilişki abstraction veya interface kullanarak sağlanmalıdır,
Abstraction detaylara bağlı olmamalıdır, aksine detaylar abstraction'lara bağlı olmalıdır.

```java
ILogger adında bir interface tanımlayalım ve FileLogger & DBLogger class'larını bu interface'den implement edelim.

public interface ILogger  
{
    void Log();
}
 
public class FileLogger : ILogger
{
    public string Message { get; set; }
    public void Log()
    {
        //File Log
    }
}
 
public class DBLogger : ILogger
{
    public string Message { get; set; }
     
    public void Log()
    {
        //Database Log
    }
}

Ve son olarak da LogManager class'ını sadece ILogger interface'ine bağlı hale getirmek kalıyor. Böylelikle ILogger'den implement olmuş bütün class'lar LogManager tarafından kullanılabilecektir.

public class LogManager 
{
    private ILogger _logger;
    public LogManager(ILogger logger)
    {
        _logger = logger;
    }
 
    public void Log()
    {
        _logger.Log();
    }
}
```

