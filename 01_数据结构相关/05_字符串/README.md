## 字符串

* （1）将字符串限制只能为字母           
```java
String paragraph = "Hello World !";
StringBuilder word = new StringBuilder();
for (char c : paragraph.toCharArray()) {
    if (Character.isLetter(c)) {  //判断全是字母
        word.append(Character.valueOf(c));
    }
}
```
* (2) 字符串转化小写
```java
paragraph=paragraph.toLowerCase();
```
