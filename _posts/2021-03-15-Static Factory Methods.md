---
layout: post
title: Static Factory Methods
description: Cân nhắc sử dụng static factory methods thay vì constructors, bản dịch Effective Java tiếng Việt
tags: java effective-java static-factory-method
permalink: /static-factory-method/
---

### Cân nhắc sử dụng **static factory methods** thay vì constructors

Thông thường, lớp dùng một `public contructor` để cho phép ta lấy ra `instance` (thực thể) của nó. Một lớp cũng có thể cung cấp cho ta một `static factory method` để trả về `instance` của lớp đó:

```java
public static Boolean valueOf(boolean b) {
	return b ? Boolean.TRUE : Boolean.FALSE;
}
```

Việc tạo ra một `static factory method` thay vì  `public contructor` đem lại cho ta sự thuận lợi và cả những bất lợi.

**Thuận lợi đầu tiên đó là, không giống như constructor, static factory method có tên**. Các tham số không đủ tường minh để mô tả mục đích của constructor, trong khi tên của constructor lại bị hạn chế bởi chính tên lớp, điều này làm cho constructor khó sử dụng và dễ gây nhầm lẫn.
