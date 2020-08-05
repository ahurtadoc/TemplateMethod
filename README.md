# Patrón de diseño "Template Method"

Es un patrón de diseño de **comportamiento** el cual permite definir el **esqueleto** del algoritmo en una **clase base**.
Se usa un **método** como plantilla, de ahí su nombre **"Template Method"**, el cual contendrá todos los **comportamientos** que debe presentar el algoritmo, donde dichas operaciones pueden ser definidas por la clase base, o **implementadas** individualmente por cada clase hija según sus necesidades.

Ejemplo clase base

```java
abstract class Generalization {
    // 1. Standardize the skeleton of an algorithm in a "template" method
    void findSolution() {
        stepOne();
        stepTwo();
        stepThr();
        stepFor();
    }
    // 2. Common implementations of individual steps are defined in base class
    private void stepOne() {
        System.out.println("Generalization.stepOne");
    }
    // 3. Steps requiring peculiar implementations are "placeholders" in the base class
    abstract void stepTwo();
    abstract void stepThr();

   void stepFor() {
        System.out.println( "Generalization.stepFor" );
    }
}
```

Las clases **concretas** pueden sobrescribir los métodos 

```java
stepOne();
stepTwo();
stepThr();
stepFor();
```
Sin embargo, no pueden modificar el método **findSolution()** ya que es la plantilla, que a su vez **obliga** a cada clase concreta a implementar este método. 

Ejemplo clase concreta
```java
class Realization extends Generalization {
    // 4. Derived classes can override placeholder methods
    protected void stepTwo() {
        System.out.println("Realization.stepTwo");
    }

    protected void stepThr() {
        System.out.println( "Realization.stepThree");
    }
     // 5. Derived classes can override implemented methods
    // 6. Derived classes can override and "call back to" base class methods 
    protected void stepFor() {
        System.out.println("Realization.stepFor");
        super.stepFor();
    }
}
```
Ejecución del código
```java
public class TemplateMethodDemo {
    public static void main(String[] args) {
        Generalization algorithm = new Realization();
        algorithm.findSolution();
    }
}
```
