### Conceito
- Mensageria é a ideia de que dois sistemas ou serviços(de sistemas diferentes ou não) vão se comunicar através de troca de mensagens.
 - A troca de mensagens por mensageria funciona de forma assíncrona. Ou seja, eu não preciso ter uma resposta imediata para o envio das mensagens, logo os sistemas e serviços envolvidos não precisam estar online ou prontamente disponíveis ao mesmo tempo.

### Exemplo
##### 1. **Imagine que temos dois sistemas que precisam se comunicar por mensageria**:
- **Sistema #1**: Sistema de gestão de frotas que envia mensagem de eventos de danos e roubo de carga. Na mensageria o sistema ou serviço que envia a mensagem é chamado de **publisher**. ^b6cbde
- **Sistema #2**: Sistema de tratamento de ocorrências de danos e roubo de carga. Na mensageria o sistema ou serviço que consome as mensagens é chamado de **consumer**.

Lembrando que o sistema que envia a mensagem não precisa esperar a resposta do sistema que irá receber, consumir(ler) a mensagem para continuar funcionando.

##### 1.1. **E como seria o envio da mensagem pelo sistema #1?**
	O sistema #1 envia a mensagem para um tópico ou fila específicos para essa mensagem no broker, que no nosso exemplo será o Azure Service Bus, aqui o **sistema #1** assume o papel de “publisher”.

- **E o que são as mensagens, tópicos, filas e broker?**
	- ***Mensagens***: são estruturas de dados, que possuem uma fila ou tópico de destino, os dados podem ser qualquer categoria de informação, incluindo dados estruturados codificados com os formatos comuns, como os seguintes: JSON, XML, Apache Avro, Plain Text.
	- ***Broker***: é um servidor de mensagens gerenciado por tópicos, filas e assinaturas.
	- **Tópico** é onde uma mensagem recebida pode ser distribuída para várias assinaturas(subscriptions), ou seja, uma única mensagem pode ser distribuída para vários serviços e sistemas, fornecendo uma forma de comunicação de um para muitos.
	- ***Fila***: é onde as mensagens são mantidas até que o sistema ou serviço esteja disponível para recebê-las e processá-las. Filas são frequentemente usadas para comunicação ponto a ponto, ou seja, de um para um, apenas um serviço ou sistema recebe e processa cada mensagem.
	- ***Assinaturas***: é onde um sistema ou serviço selecionam mensagens específicas de um fluxo de mensagens enviadas.

##### **1.2. E como acontece o consumo da mensagem pelo sistema #2?**
	O sistema #2 assume o papel de "consumer" e o consumo da mensagem pode ser feito por meio de:

- **Tópicos e assinaturas:** As mensagens são recebidas no tópico específico de destino e distribuídas para várias assinaturas(subscription) onde temos a escalabilidade das mensagens, ou seja, uma única mensagem podendo ser consumida por diversos sistemas e serviços.

	![[Mensageria 3 receptores.png]]

		No contexto de tópicos e assinaturas, o sistema #2 acessa Azure Service Bus e se conecta com a assinatura do tópico específico da mensagem de ocorrência de danos e roubo de cargas.
- **Filas**: As filas oferecem entregas de mensagens First In, First Out (FIFO) para um ou mais serviços ou sistemas concorrentes. Ou seja, apenas um sistema ou serviço recebe e processa cada mensagem.
	![[Mensageria enviando.png]]

		Nesse contexto, o sistema #2 acessa Azure Service Bus e se conecta com a fila específica da mensagem de ocorrência de danos e roubo de cargas.

E são essas as formas que o **sistema #2** pode fazer o consumo das mensagens enviados pelo **sistema #1**.

## Principais vantagens
	 Bacana esse negócio de mensageria, mas quais as vantagens de utilizarmos mensageria?

Uma das principais vantagem que a mensageria oferece é o desacoplamento das aplicações, ou seja, as aplicações não precisam estar online ou prontamente disponíveis ao mesmo tempo, e também se torna indiferente a linguagem em que as aplicações foram desenvolvidas.

- **Outras vantagens da mensageria são:**
	- **Responsividade**: em fluxos que envolvem muitas tarefas, o uso de mensagens faz com que nossa aplicação seja mais responsiva, liberando o usuário de esperar até que todas as tarefas sejam concluídas;
	- **Escalabilidade**: maior desempenho, ao poder termos várias instâncias processando as mensagens, aumentamos a capacidade da aplicação;
	- **Confiabilidade**: diante da queda de um dos sistemas ou serviços não temos a perda de informações.


## Mapa mental - Resumo
![[Mapa mental mensageria.png]]