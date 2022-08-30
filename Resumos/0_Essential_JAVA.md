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
            "implements"   ->  
            (exemplo)

_Sort_ / ORDENAR dados de uma lista    ->   "implements Comparator< Nome_da_classe >
```java
public class PlayerAgeComparator implements Comparator<Player> {

    // Função para Ordenae por ordem Crescente (naturalmente, sem criação de 
    // Equação: OtherPlayer - Player
    public int compareTo(Player otherPlayer) {
        return Integer.compare(getRanking(), otherPlayer.getRanking());
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
