---
layout: post
title: Observer pattern
description: Mẫu thiết kế Observer pattern
tags: java design-pattern
permalink: /observer-pattern/
---

> 'Mẫu thiết kế Người theo dõi' xác định rõ sự phụ thuộc một-nhiều giữa các đối tượng, vậy nên khi một đối tượng thay đổi trạng thái thì tất cả các đối tượng phụ thuộc nó đều biết được và cập nhật tự động. - GOF

<br/>

Mẫu thiết kế này xoay quanh hai khái niệm `subject` (chủ thể) và `observer` (người theo dõi). Trong ví dụ mô phỏng quy trình làm việc giữa trung tâm khí tượng và đài phát thanh dưới đây, `subject - TrungTamKhiTuong.java` sẽ đóng vai trò 'một', còn `observer - Vov.java` đóng vai trò 'nhiều'.

<br/><br/>

## Ví dụ bằng java

<hr>

<br/>

`Subject.java`

```java
public interface Subject {
    void registerObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}
```

<br/>

`Observer.java`

```java
public interface Observer {
    void update(float nhietDo, float doAm);
}
```

<br/>

`TrungTamKhiTuong.java`

```java
public class TrungTamKhiTuong implements Subject {
    
	private float nhietDo;
    private float doAm;
    
    private List<Observer> observers = new ArrayList<Observer>();

    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }

    @Override
    public void removeObserver(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer: observers) {
            observer.update(this.nhietDo, this.doAm);
        }
    }

    // giả lập thông số
    public void setThongSo(float nhietDo, float doAm) {
        this.nhietDo = nhietDo;
        this.doAm = doAm;
        notifyObservers();
    }
}
```

<br/>

`Vov.java`

```java
package trungtamkhituong;

public class Vov implements Observer{

    private float nhietDo;
    private float doAm;

    private TrungTamKhiTuong trungTamKhiTuong;

    public Vov(TrungTamKhiTuong trungTamKhiTuong) {
        this.trungTamKhiTuong = trungTamKhiTuong;
        this.trungTamKhiTuong.registerObserver(this);
    }

    @Override
    public void update(float nhietDo, float doAm) {
        this.nhietDo = nhietDo;
        this.doAm = doAm;
        banTinDuBaoThoiTiet();
    }

    public void banTinDuBaoThoiTiet() {
        System.out.println("Nhiệt độ hôm nay là " +
                this.nhietDo + " độ C, độ ẩm " + this.doAm + "%" );
    }
}

```

<br/><br/>

## Khởi chạy

<hr>

```java
public class KhoiChay {

    public static void main(String[] args) {

        TrungTamKhiTuong trungTamKhiTuong = new TrungTamKhiTuong();
        Vov vov = new Vov(trungTamKhiTuong);
        
        trungTamKhiTuong.setThongSo(32.3f, 46f);
        trungTamKhiTuong.setThongSo(16.5f, 72f);
    }
}
```

<br/><br/>

### Kết quả

<hr>
<br/>

```
Nhiệt độ hôm nay là 32.3 độ C, độ ẩm 46.0%
Nhiệt độ hôm nay là 16.5 độ C, độ ẩm 72.0%
```



