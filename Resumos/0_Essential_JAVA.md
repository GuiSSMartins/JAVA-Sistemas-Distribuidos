# Código mais importante para JAVA (em Sistemas Distribuídos - SD)

-------------------------------------------------------------------

Código Inicial (ler argumentos do comando de execução do programa)
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

----------------------------------------------------------
Coisas mais simples

```java
int[] other = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; // array
for (int i = 0; i < array.length; i++)
    System.out.println(array[i]);
for (int element : array) 

int[][] array = {{  0,  1,  2,  3,  4 },
                 {  5,  6,  7,  8,  9 },
                 { 10, 11, 12, 13, 14 }};
System.out.println(array[1][0]); // 5
```

---------------------------------------------------------
Ler conteúdo do ecrã

```java
Scanner scanner = new Scanner(System.in); // Instantiating a new Scanner object
String line = scanner.nextLine();         // Reading a line
System.out.println(line);                 // Printing out the line
int number = scanner.nextInt();           // We can also read primitive types
```

--------------------------------------------------------------------

Hierarquia: "extends"   Carro -> Toyota extends Carro
            "implements"   ->  
            (exemplo)

Polimorfismo: _Um simples símbolo pode representar diferentes tipos_

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

CRIAR Novas Exceções: (é preciso criar um novo ficheiro para a nova classe com a Exceção que queremos criar)
DICA: Aproveitar ao máximo as propriedades da hierarquia de _Exceptions_ (__extends__)
```java
public class DeviceAlreadyExists extends Exception{
    public DeviceAlreadyExists(String msg){
        super(msg);
    }
}
```

Ler ficheiros:
```java
p
```

Parsing de dados de ficheiros:


Leitura de _Input_:


Escrita num ficheiro de Output:


_StringBuffer_ é "thread-safe" (e, por isso, mais lento)

## 

```java
private Map<String, Item> stock = new HashMap<>();
```

## Estruturas/Structs para armazenar dados

- __ArrayList__ (um array em forma de lista) 
- HashSet - !!! WARNING !!! : Evitar usar; por favor, use uma __HashMap__
- HashMap
- 

## Como criar um _Comparator_ para ordenar _ArrayList_'s e _Streams_

## Collectors

```java
Map<String, Aluno>
```




- EXTRAS
```java
switch (variable) {                 // variable must be of the correct type 
  case 1: doSomething();
    break;                          // don't forget the break
  case 2: doSomethingElse();
    break;
  default: doSomethingDefault();
    break;
}
```

Criar clones de estruturas
```java
public class Light implements Cloneable{
  public Object clone() throws CloneNotSupportedException {
    return super.clone();
  }
}

Light another = light.clone();
```
