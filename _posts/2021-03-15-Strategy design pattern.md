---
layout: post
title: Strategy pattern okokok
description: Mẫu thiết kế Strategy pattern
tags: java design-pattern
permalink: /strategy-pattern/
---

## Làm sao để tạo một ứng dụng mô phỏng vịt?
------


<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0002-01.png" alt="img"  />

<br/><br/>
## Nhưng giờ ta cần vịt BAY được
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0003-01.png" alt="Images"  />

<br/><br/>
## Có điều khủng khiếp đã xảy ra
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0004-01.png" alt="Images"  />

<br/><br/>
## Vì không phải vịt nào cũng bay được
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0004-03.png" alt="Images"  />

<br/><br/>
## Có nên thừa kế chăng?
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0005-01.png" alt="Images"  />

<br/><br/>
## Dùng Interface thì sao?
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0006-01.png" alt="Images"  />

<br/><br/>
## Như thế sẽ rất khó bảo trì
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0007-01.png" alt="Images"  />

<br/><br/>
## Đã đến lúc dùng tới Strategy pattern
------

<br/>
<img src="https://learning.oreilly.com/library/view/head-first-design/9781492077992/assets/f0022-01.png" alt="img"  />

<br/><br/>
## Cài đặt
------

<br/>
`Duck`

```java
public abstract class Duck {
	FlyBehavior flyBehavior;
	QuackBehavior quackBehavior;
 
	public Duck() {
	}
 
	public void setFlyBehavior (FlyBehavior fb) {
		flyBehavior = fb;
	}
 
	public void setQuackBehavior(QuackBehavior qb) {
		quackBehavior = qb;
	}
 
	abstract void display();
 
	public void performFly() {
		flyBehavior.fly();
	}
 
	public void performQuack() {
		quackBehavior.quack();
	}
    
 	public void swim() {
		System.out.println("All ducks float, even decoys!");
	}
}
```
<br/>
`FlyBehavior`

```java
public interface FlyBehavior {
	public void fly();
}
```
<br/>
`QuackBehavior`

```java
public interface QuackBehavior {
	public void quack();
}
```
<br/>
`FlyWithWings`

```java
public class FlyWithWings implements FlyBehavior {
	public void fly() {
		System.out.println("I'm flying!!");
	}
}
```
<br/>
`FlyNoWay`

```java
public class FlyNoWay implements FlyBehavior {
	public void fly() {
		System.out.println("I can't fly");
	}
}
```
<br/>
`FlyRocketPowered`

```java
public class FlyRocketPowered implements FlyBehavior {
	public void fly() {
		System.out.println("I'm flying with a rocket");
	}
}
```
<br/>
`FakeQuack`

```java
public class FakeQuack implements QuackBehavior {
	public void quack() {
		System.out.println("Qwak");
	}
}
```
<br/>
`MuteQuack`

```java
public class MuteQuack implements QuackBehavior {
	public void quack() {
		System.out.println("<< Silence >>");
	}
}
```
<br/>
`Quack`

```java
public class Quack implements QuackBehavior {
	public void quack() {
		System.out.println("Quack");
	}
}
```
<br/>
`Squeak`

```java
public class Squeak implements QuackBehavior {
	public void quack() {
		System.out.println("Squeak");
	}
}
```
<br/>
`MallardDuck`

```java
public class MallardDuck extends Duck {
 	
    public MallardDuck() {
 		quackBehavior = new Quack();
         flyBehavior = new FlyWithWings();
	}
 
	public void display() {
		System.out.println("I'm a real Mallard duck");
	}
}
```
<br/>
`RedHeadDuck`

```java
public class RedHeadDuck extends Duck {
 
	public RedHeadDuck() {
		flyBehavior = new FlyWithWings();
		quackBehavior = new Quack();
	}
 
	public void display() {
		System.out.println("I'm a real Red Headed duck");
	}
}
```
<br/>
`RubberDuck`

```java
public class RubberDuck extends Duck {
    
	public RubberDuck() {
		flyBehavior = new FlyNoWay();
		quackBehavior = new Squeak();
	}
    
	public void display() {
		System.out.println("I'm a rubber duckie");
	}
}
```
<br/>
`ModelDuck`

```java
public class ModelDuck extends Duck {
    
	public ModelDuck() {
		flyBehavior = new FlyNoWay();
		quackBehavior = new Quack();
	}
    
	public void display() {
		System.out.println("I'm a model duck");
	}
}
```

<br/><br/>
## Khởi chạy
------

<br/>
```java
public class MiniDuckSimulator {
 
	public static void main(String[] args) {

		MallardDuck	mallard = new MallardDuck();
		RubberDuck	rubberDuckie = new RubberDuck();
		DecoyDuck	decoy = new DecoyDuck();
 
		ModelDuck	model = new ModelDuck();

		mallard.performQuack();
		rubberDuckie.performQuack();
		decoy.performQuack();
   
		model.performFly();	
		model.setFlyBehavior(new FlyRocketPowered());
		model.performFly();
	}
}
```


<br/><br/>
*Từ cuốn [Head First Design Pattern](https://www.oreilly.com/library/view/head-first-design/9781492077992/)*.

<br/><br/>

