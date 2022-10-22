### (Guiões 1, 2 e 3)

# 1) Threads & Locks & Exclusão Mutua

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

// Técnica extra: t.sleep(5);
// Colocamos a Thread não funciona durante 5 segundos. Só no final deste período de tempo
```

## Guardar um conjunto de _Threads_ (para serem utilizadas _ao mesmo tempo_)
Por exemplo, queremos queexistam 10 threads a funcioanr simultaneamente.

```java
List<Thread> lt = new ArrayList<>();

for(int i=0; i<10; i++) {
  lt.add(new Thread(new Increment())); // Increment é só um exemplo de uma classe Runnable
}

for(int j=0; j<10; j++){
  lt.get(j).start(); // Inicializamos cada uma das threads
}

for(int m=0; m<10; m++){
  lt.get(m).join(); // O método da Thread pode terminar, mas a Thread continua em memória
}
```

## Locks (Classe _ReentrantLock_)
Os Locks são usados para limitar a entrada a APENAS 1 Thread Simultanea a uma região específica do código.

Quando é feito o _l.lock()_, apenas UMA Thread pode estar a funcionar essa zona. Só quando essa Thread sair da região, é que outra pode entrar.

__VANTAGENS__: (Relembrar caso do Acesso e Modificação de dados de um Banco) Garantimos que quando uma Thraed acede aos dados atualizados da variável/classe, estesnão estão a ser "mexidos" por uma outra Thread. Isto acontece porque as Thraeds partilham memória entre si. Por isso, o controlo da infromação que as Threads "tocam" é Muito Importante!

## Técnicas de _Exclusão Mutua_

Para que os Locks sejam aproveitados ao máximo, estes devem ser colcoados APENAS nas operações Atómicas!
