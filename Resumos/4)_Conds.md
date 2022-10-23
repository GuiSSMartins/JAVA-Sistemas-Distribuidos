(Guiões 4, 5 e 6)

# 4) Uso de Locks em _Condicionais_ (_if-then-else, while, for_...)

A partir deste momento, vamos voltar a usar algumas das noções lecionadas em SO ("_here we go again..._") sobre a comunição entre Clientes e Servidores, nomeadamente a relação e os cuidados a ter com os __Readers__ e com os __Writers__, e ,por fim, os __SINAIS__ (para ).

## -> Variáveis de Condição

Permitem que thraeds suspendam/retomem a sua execução __dentro de secções críticas__, de acordo com uma dada condição.

__ATENÇÃO__: Lock NÃO é um conjunto de Threads!!! É apenas algo que limita a entrada a apenas 1 thread de cada vez na região crítica que limita.

```java
Lock l = new ReentrantLock();
Condition c = l.newCondition(); // para gerir os sinais para este lock
c.await(); // "unlocks" o lock & a Thread atual fica em espera até que seja notificada para retomar execução

// Ativar as threads suspensas:
c.signalAll(); // ativar todas as thraeds suspensas para resumirem a sua execução
c.signal(); // notifica uma thread para resumir a sua execução
```

Temos de ter em conta (pensar sempre numa ideia intuitiva):
- Enquanto houverem _Writers_ ativos, o READER não pode ler coisas;
- Mas para um WRITER escrever algo, não podem coexistir outros Writers e Readers ativos.
