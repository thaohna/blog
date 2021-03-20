Mẫu trang trí giúp ta mở rộng chức năng của một đối tượng một cách linh hoạt hơn khi so với việc tạo ra các phân lớp (subclassing).

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Decorator_UML_class_diagram.svg/800px-Decorator_UML_class_diagram.svg.png)

`Decorator` dùng một đối tượng `Component` (aggregation), đồng thời cũng thừa kế/thực thi `Component`. Lớp `ConcreteComponent` dùng để tạo ra đối tượng gốc, tức đối tượng cần được trang trí. Các đối tượng bọc/trang trí bên ngoài `ConcreteComponent` được tạo ra bằng lớp `ConcreteDecorator`.

## Mô phỏng quy trình gọi hàm

![img](https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0107-01.png)

<br/><br/>

## Cài đặt

<hr>

`Pizza.java` đại diện cho `Component`

```java
public abstract class Pizza {

     public abstract double gia();
     public abstract String moTa();
}
```

<br/>

`PizzaDecorator.java` đại diện cho `Decorator`

```java
public class PizzaDecorator extends Pizza{

    private Pizza pizza;

    public PizzaDecorator(Pizza pizza) {
        this.pizza = pizza;
    }

    @Override
    public double gia() {
        return pizza.gia();
    }

    @Override
    public String moTa() {
        return pizza.moTa();
    }
}
```

<br/>

`PizzaThuong.java` đại diện cho `ConcreteComponent`

```java
public class PizzaThuong extends Pizza{

    @Override
    public double gia() {
        return 5;
    }

    @Override
    public String moTa() {
        return " Pizza thường";
    }
}
```

<br/>

`PhoMai.java`, `SotCaChua.java`, `RauCu.java` đại diện cho `ConcreteDecorator`

```java
public class PhoMai extends PizzaDecorator{
    
    public PhoMai(Pizza pizza) {
        super(pizza);
    }

    @Override
    public double gia() {
        return super.gia() + 0.7;
    }

    @Override
    public String moTa() {
        return super.moTa() + ", Sốt Phô Mai";
    }
}
```

```java
public class SotCaChua extends PizzaDecorator{
    
    public SotCaChua(Pizza pizza) {
        super(pizza);
    }

    @Override
    public double gia() {
        return super.gia() + 0.5;
    }

    @Override
    public String moTa() {
        return super.moTa() + ", Sốt Cà Chua";
    }
}
```

```java
public class RauCu extends PizzaDecorator{
    
    public RauCu(Pizza pizza) {
       super(pizza);
    }

    @Override
    public double gia() {
        return super.gia() + 0.3;
    }

    @Override
    public String moTa() {
        return super.moTa() + ", Rau Củ";
    }
}
```

<br/><br/>

## Khởi chạy

<hr>

```java
public class PizzaMaker {

    public static void main(String[] args) {

        Pizza pizzaRauCuSotCaChua = 
            new RauCu(new PhoMai(new SotCaChua(new PizzaThuong())));

        System.out.println("Giá pizza này là: "
                           + pizzaRauCuSotCaChua.gia() + "$"
                           + "\nBao gồm: " 
                           + pizzaRauCuSotCaChua.moTa());
    }
}
```

<br/>

<br/>

## Kết quả

<hr>

<br/>

```
Giá pizza này là: 6.5 $
Bao gồm:  Pizza thường, Sốt Cà Chua, Sốt Phô Mai, Rau Củ
```

