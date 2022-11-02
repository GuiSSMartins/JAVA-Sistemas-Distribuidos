(Guiões 4, 5 e 6)

# 4 e 5) Uso de Locks em _Condicionais_ (_if-then-else, while, for_...)

A partir deste momento, vamos voltar a usar algumas das noções lecionadas em SO ("_here we go again..._") sobre a comunição entre Clientes e Servidores, nomeadamente a relação e os cuidados a ter com os __Readers__ e com os __Writers__, e ,por fim, os __SINAIS__ (para ).

## -> Variáveis de Condição

Permitem que thraeds suspendam/retomem a sua execução __dentro de secções críticas__, de acordo com uma dada condição.

__ATENÇÃO__: Lock NÃO é um conjunto de Threads!!! É apenas algo que limita a entrada a apenas 1 thread de cada vez na região crítica que limita.

```java
Lock l = new ReentrantLock();
Condition c = l.newCondition(); // para gerir os sinais para este lock
c.await(); // "unlocks" o lock & a Thread atual fica em espera até que seja notificada para retomar execução

// DICA: A conição .wait() deve ser feita dentro de um corpo de um WHILE

// Ativar as threads suspensas:
c.signalAll(); // ativar todas as thraeds suspensas para resumirem a sua execução
c.signal(); // notifica uma thread para resumir a sua execução
```

Temos de ter em conta (pensar sempre numa ideia intuitiva):
- Enquanto houverem _Writers_ ativos, o READER não pode ler coisas;
- Mas para um WRITER escrever algo, não podem coexistir outros Writers e Readers ativos.


## -> Criar um sistema que implemente os Locks em vars. Condicionais

CUIDADO: Nós queremos que uma mesma operação pode ser usadas várias vezes
Uma espécie de Barreira à passagem de threads que impede de mais threads entrarem no processo enquanto outras não tiverem sido atiuvadas.

Fazemos as coisas desta maneira para uma quantidade de threads atuem em processos ao mesmo tempo.


## -> Múltiplas Variáveis de Condição (Ficha 5)

Em vez de estarmos a ter de criar uma Barreira para cada parte do programa onde se quer limitar o número de threads 

### Uso de Armazéns

```java
// Só vamos usar APENAS 1 Lock

// Ver os slides das Multiplas vars de condições
// Para entender melhor a dinâmica de locks, unlocks, awaits, e signalsAlls na parte dos testes dos Clientes

class Warehouse {
  private Lock l = new ReentrantLock(); // lock do armazém

  private Map<String, Product> map =  new HashMap<String, Product>();

  private class Product { 
    Condition c = l.newCondition(); // condition isEmpty ====== condition exlusiva para este produto 
                                    // deve ser criada uma condition para cada produto criado, para que se o signalAll() se aplique no prosuto específico
    int quantity = 0; 
  }

  private Product get(String item) {
    Product p;
    l.lock();
    try {
      p = map.get(item);
      if (p != null) return p;
    }
    finally {
      l.unlock();
    }
    p = new Product();
    map.put(item, p);
    return p;
  }

  // Versão EGOÍSTA - cada cliente tenta apropriar-se dos itens o mais cedo possível
  // Versão um pouco mais sequencial
  // Deve-se evitar esta versão, porque os itens são logo consumidos sem necessidade

  public void supply(String item, int quantity) throws InterruptedException {
    l.lock();
    try {
      Product p = get(item);
      p.quantity += quantity;
      p.c.signalAll();
    }
    finally {
      l.unlock();
    }  
  }

  public void consume(Set<String> items) throws InterruptedException {
    l.lock();  
    try {
      for (String s : items) {
        Product p = get(s);
        while(p.quantity == 0) {
          p.c.await();
        }
        get(s).quantity--;
      }
    }
    finally {
      l.unlock();
    }
  }

  // Versão COOPERATIVA - não reserva itens para clientes que não possam ser satisfeitos no momento (porque faltam alguns)
  // Versão mais Segura
  // Vamos usar a mesma versão do supply

  // Problema: há a possibilidade de STARVATION (de uma tarefa nunca terminar)
  // SOLUÇÂO (ainda não implemntado): problema adicional
  public void consume(Set<String> items) throws InterruptedException {
    HashMap<String, Integer> quantity_desired_items = new HashMap<String, Integer>();
    for (String s : items) { // Vamos calcular a quantidade desejada de cada item
      if (quantity_desired_items.containsKey(s)) {
        Integer n = quantity_desired_items.get(s);
        n++;
        quantity_desired_items.put(s, n);
      }
      else {
        quantity_desired_items.put(s, 1);
      }
    }

    l.lock();  
    int i=0;
    int hash_length = quantity_desired_items.keySet().size();
    try {
      while (i < hash_length) {
        for (String s : quantity_desired_items.keySet()) {
          Integer desired_quantity = quantity_desired_items.get(s);
          Product p = get(s);
          i++;
          while(p.quantity < desired_quantity) {
            p.c.await();
            i=0;
          }
        }
      }
      for (String s : quantity_desired_items.keySet()) {
        Integer desired_quantity = quantity_desired_items.get(s);
        Product p = get(s);
        p.quantity -= desired_quantity;
      }
    }
    finally {
      l.unlock();
    }
  }
}

// Starvation: a sua tarefa nunca consegue ser terminada
```
