# 4) Uso de LOcks em _Condicionais_ (_if-then-else, while, for_...)

A partir deste momento, vamos voltar a usar algumas das noções lecionadas em SO ("_here we go again..._") sobre a comunição entre Clientes e Servidores, nomeadamente a relação e os cuidados a ter com os __Readers__ e com os __Writers__.

```java
Lock l = new ReentrantLock();
Condition c = l.newCondition();
c.await(); // atomically unlocks l and suspends, relocks l on wakeup

// Waking up suspended threads:
c.signalAll(); // all threads
c.signal(); // one thread

// For a READER (#1):
lock() {
  // while(there is a writer)
    wait…
  nr_readers++
}
unlock() {
  nr_readers--
}

// For a WRITER (#2):
lock() {
  // while(there is anyone (writer or reader))
    wait…
  a_writer = true
}
unlock() {
  a_writer = false
}
```

Pelo código podemos perceber que:
- Enquanto houverem _Writers_ ativos, o READER não pode ler coisas;
- Mas não podem coesxistir vaŕios writers e readers, quandio estamos num WRITER
