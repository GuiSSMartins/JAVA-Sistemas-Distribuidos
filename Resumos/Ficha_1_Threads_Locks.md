# 1) Threads & Locks

## Criação de _APENAS uma Thread_

```java
public class SayHello implements Runnable {
  // A função "run" é ativada com a respetiva Thread que a implementa
  public void run() {
    // Colocamos o que quisermos
  } }

public class Main {
  public static void main(String args[]) {
    Thread t = new Thread(new SayHello());
    t.start(); // Inicia uma thread (!!! Não esquecer de fazer "new" à classe Thread !!!)
    t.join(); // O método da Thread pode terminar, MAS a Thread CONTINUA em MEMÓRIA
  }
}
```

## Guardar um conjunto de _Threads_ (para serem utilizadas _ao mesmo tempo_)

