
## Criação de uma Thread

```java
public class SayHello implements Runnable {
 public void run() {
 System.out.println("Hello from a thread!");
 }
}

public class Main {
 public static void main(String args[]) {
 Thread t = new Thread(new SayHello());
 t.start();
 t.join(); // Bloqueia até a thread terminar.
 }
}
```
