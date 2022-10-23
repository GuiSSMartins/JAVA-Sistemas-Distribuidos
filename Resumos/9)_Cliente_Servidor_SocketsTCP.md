# Interação Cliente-Servidor com _Sockets_ TCP 

(adaptado dos últimos slides das Aulas Práticas de Sistemas Distribuídos)

(Relação com o trabalho de DNS de _Comunicações por Computador_ - DNS usa TCP como protocolo de transporte de dados)

## -> Porquê TCP?

Como a comunicação deve ser fiável (ou seja, sem perda de dados e com entrega ordenada de mensagens).

## -> Paradigma Cliente-Servidor

NORMALMENTE, o cliente inicia o contacto com o servidor.



## -> O que é um _Socket_?
Sockets são estrturas que permitem 

### .../ Cliente
```java
Socket socket = new Socket(address, port);
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
PrintWriter out = new PrintWriter(socket.getOutputStream());
while(...) {
  out.println(…);
  out.flush();
  ... = in.readLine();
}
socket.shutdownOutput();
socket.shutdownInput();
socket.close();
```

### .../ Servidor
