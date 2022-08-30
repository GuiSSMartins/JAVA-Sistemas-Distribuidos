# Código mais importante para JAVA (em Sistemas Distribuídos)

Código Inicial (ler argumentos
```java
public class Main {
    public static void main(String[] args) {
        
        // Para ler os vários argumentos recebidos, usamos uma iteração
        int length = args.length();
        for (int i=0; i<length; i++) {
             System.out.println(args[i]);
        }
    }
}
```

Hierarquia: "extends"   Carro -> Toyota extends Carro

ORDENAR dados de uma lista
```java
public class PlayerAgeComparator implements Comparator<Player> {
    public int compare(Player firstPlayer, Player secondPlayer) {
       return Integer.compare(firstPlayer.getAge(), secondPlayer.getAge());
    }
}
```

"Lançar" EXCEÇÕES específicas:
```java
throw
```

"Apanhar" EXCEÇÕES - Threads
```java
try {
    threads[i].join();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

Escrever Novas Exceções:

Ler ficheiros:
```java
p
```

Parsing de dados de ficheiros:


Leitura de _Input_:


Escrita num ficheiro de Output:


_StringBuffer_ é "thread-safe" (e, por isso, mais lento)

## 

## Estruturas/Structs para armazenar dados

- ArrayList (um array em forma de lista) 
- HashMap
- 

## Collectors

```java
Map<String, Aluno>
```
