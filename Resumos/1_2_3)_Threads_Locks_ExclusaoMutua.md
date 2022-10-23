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
// A Thread deixa de funcionar durante 5 segundos. Só no final deste período de tempo, é que volta a "estar no ativo".
```

## Guardar um conjunto de _Threads_ (para serem utilizadas _ao mesmo tempo_)
Por exemplo, queremos queexistam 10 threads a funcioanr simultaneamente.

```java
List<Thread> lt = new ArrayList<>();

for(int i=0; i<10; i++) {
  lt.add(new Thread(new Increment())); } // Increment é só um exemplo de uma classe Runnable

for(int j=0; j<10; j++){
  lt.get(j).start(); } // Inicializamos cada uma das threads

for(int m=0; m<10; m++){
  lt.get(m).join(); } // O método da Thread pode terminar, mas a Thread continua em memória
```
-------------------------------------

## -> Locks (Classe _ReentrantLock_)
Os Locks são usados para limitar a entrada a APENAS 1 Thread Simultanea a uma região específica do código.

Quando é feito o _l.lock()_, apenas UMA Thread pode estar a funcionar essa zona. Só quando essa Thread sair da região, é que outra pode entrar.

__VANTAGENS__: (Relembrar caso do Acesso e Modificação de dados de um Banco) Garantimos que quando uma Thraed acede aos dados atualizados da variável/classe, estesnão estão a ser "mexidos" por uma outra Thread. Isto acontece porque as Thraeds partilham memória entre si. Por isso, o controlo da infromação que as Threads "tocam" é Muito Importante!

Acessos concorrentes a recursos partilhados

Exemplo de código onde se utilizam as funções:
```java
Lock l = new ReentrantLock();
//...
l.lock();
try{
  // Região Crítica, onde queremos limitar a entrada a 1 Thread de cada vez
} finally {
  l.unlock();
}
```
-----------------------------------------

## -> Técnicas de _Exclusão Mutua_

- __Exclusão Mútua__: propriedade que _garante_ que dois processos ou threads não acedam simultaneamente a um recurso partilhado. 
- __Secção Crítica__: parte do programa onde os recursos _partilhados_ são acedidos. É __FUNDAMENTAL__ proteger estas secção (como a utilização da _Exclusão Mútua_)

Para que os Locks sejam aproveitados ao máximo, estes devem ser colcoados APENAS nas operações Atómicas - __Read e Write__ (como somas OU mudanças de sítio de certos dados)!

Mas a melhor de controlarmos os casos de Read e de Write é utilizarmos uma versão mais específica de Locks.

A classe __ReentrantReadWriteLock__ aumenta mais a concorrência dos programas já que faz a distinção entre os Locks para Read e para Write. 

__ATENÇÃO__: Más escolhas do uso destes Locks podem provocar __Deadlocks__, ou seja, chega a um ponto do programa em que dois locks bloqueiam o programa, já que estes estão à espera de serem _unlocked_.

-------------------------------------

- __l.readLock()__ _ou_ __.unlock()__: lock de Leitura, de acesso _partilhado_ (isto acontece porque, mesmo com muitos Readers, a informação não muda, por isso não faz mal haverem vários Readers a aceder a mesma varíavel/estrutura - são incapapzes de a mudar)
- __l.writeLock().lock()__ _ou_ __.unlock()__: (NOTA: apenas uma Thread tem acesso à secção)

---------------------------------------

__TÉCNICA 1__: Criar um __ReentrantReadWriteLock__ para cada classe onde se quer concorrência.

Quando fazemos a __recolha__ de _locks_, devemos sempre que possível 

Muitos dos dados que queremos aceder, só o devem ser feitos após se terem recolhido todos os locks.
