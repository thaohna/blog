---
layout: post
title: Static Factory Methods
description: Cân nhắc sử dụng static factory methods thay vì constructors, bản dịch Effective Java tiếng Việt
tags: java effective-java static-factory-method
permalink: /static-factory-method/
---

## Cân nhắc sử dụng **static factory methods** thay vì constructors

Thông thường, một lớp cho phép ta lấy về thực thể (instance) của nó thông qua hàm dựng public (public constructors).Ta cũng có thể dùng `static factory method` để làm điều tương tự:

```java
public static Boolean valueOf(boolean b) {
	return b ? Boolean.TRUE : Boolean.FALSE;
}
```

Việc tạo ra một `static factory method` thay vì  hàm dựng public đem lại cho ta sự thuận lợi và cả những bất lợi.

**Thuận lợi đầu tiên đó là, không giống như constructor, static factory method có tên**. Các tham số không đủ tường minh để mô tả mục đích của constructor, trong khi tên của constructor lại bị hạn chế bởi chính tên lớp, điều này làm cho constructor khó sử dụng và dễ gây nhầm lẫn.
