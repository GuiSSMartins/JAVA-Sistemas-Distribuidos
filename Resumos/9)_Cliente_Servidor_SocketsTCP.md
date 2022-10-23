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
# Criar socket e ligação com o servidor
Socket socket = new Socket(address, port);
# Abrir canais de escrita e leitura no socket
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
PrintWriter out = new PrintWriter(socket.getOutputStream());
# Ler e escrever nos canais de acordo com o protocolo de aplicação
while(...) {
  out.println(…);
  out.flush();
  ... = in.readLine();
}
# Fechar socket e respetivos canais
socket.shutdownOutput();
socket.shutdownInput();
socket.close();
```

### .../ Servidor
