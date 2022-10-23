# Interação Cliente-Servidor com _Sockets_ TCP 

(adaptado dos últimos slides das Aulas Práticas de Sistemas Distribuídos)

(Relação com o trabalho de DNS de _Comunicações por Computador_ - DNS usa TCP como protocolo de transporte de dados)

## -> Porquê TCP?

Como a comunicação deve ser fiável (ou seja, sem perda de dados e com entrega ordenada de mensagens).

## -> O que é um _Socket_?
Sockets são estruturas que permitem 

## -> Paradigma Cliente-Servidor

NORMALMENTE, o cliente inicia o contacto com o servidor.

Para tal, temos de distinguir dois tipos de Sockets: __Server Socket__ (associado ao Servidor) e o __Socket__ (associado ao Cliente), que são os dois extremos da conexão entre o Cliente-Servidor.

Resumidamente, o SErvidor fica à espera de ligações num determinado porto. Quando o cliente se liga ao servidor, é estabelecida uma nova conexão bidirecional.

- Para ler e escrever no Socket: _BufferedReader_, _InputStreamReader_, _PrintWriter_.

### .../ Cliente
```java
// Criar socket e ligação com o servidor
Socket socket = new Socket(String host, int port);
# Abrir canais de escrita e leitura no socket
BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
PrintWriter out = new PrintWriter(socket.getOutputStream());
// Ler e escrever nos canais de acordo com o protocolo de aplicação
while(...) {
  out.println(…);
  out.flush();
  ... = in.readLine();
}
// Fechar socket e respetivos canais
socket.shutdownOutput();
socket.shutdownInput();
socket.close();
```

### .../ Servidor
```java
// Criar novo server socket num dado porto
ServerSocket sSock = new ServerSocket(int port);
// Aceitar conexões indefinidamente (Bloquear até que uma conexão seja estabelecida)
while (true) {
  Socket clSock = sSock.accept();
  BufferedReader in = new BufferedReader(new InputStreamReader(clSock.getInputStream()));
  // Abrir canais de escrita e leitura no socket
  PrintWriter out = new PrintWriter(
  clSock.getOutputStream());
  // Ler e escrever nos canais de acordo com o protocolo da aplicação
  while(...) {
    ... = in.readLine();
    out.println(…);
    out.flush();
  }
  // Fechar socket e respectivos canais
  clSock.shutdownOutput();
  clSock.shutdownInput();
  clSock.close();
}
```
