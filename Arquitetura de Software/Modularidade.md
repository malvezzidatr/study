A modularidade é a prática de dividir um sistema em componentes menores, chamados módulos, que podem ser desenvolvidos, mantidos e compreendidos de maneira independente. Um sistema modular oferece melhor manutenibilidade, escalabilidade e facilita a colaboração entre equipes.

#### **Coesão**
**Coesão** refere-se ao grau em que os elementos dentro de um módulo estão relacionados e trabalham juntos para cumprir uma única responsabilidade. Alta coesão é desejável, pois significa que um módulo faz apenas uma coisa e faz bem. Baixa coesão, por outro lado, indica que um módulo tem responsabilidades mal definidas ou múltiplas, o que pode dificultar a compreensão e a manutenção.

- **Alta coesão**: Um módulo tem uma única responsabilidade bem definida. Exemplo: Um módulo que gerencia apenas a autenticação de usuários.
- **Baixa coesão**: Um módulo tem responsabilidades diversas e mal relacionadas. Exemplo: Um módulo que lida com autenticação, envio de e-mails e geração de relatórios.

**Tipos de coesão**:

1. **Coesão Funcional**: Quando todas as partes de um módulo trabalham juntas para executar uma função específica. É o tipo de coesão mais desejável.
2. **Coesão Sequencial**: Quando a saída de uma parte do módulo é a entrada da próxima, como em um pipeline de dados.
3. **Coesão Comunicacional**: Quando as partes de um módulo operam em conjunto sobre o mesmo conjunto de dados.
4. **Coesão Lógica**: Quando as partes de um módulo são agrupadas porque realizam tarefas logicamente relacionadas, mas podem ser executadas separadamente.
5. **Coesão Temporal**: Quando as partes de um módulo são executadas ao mesmo tempo, por exemplo, ao inicializar o sistema.

#### **Acoplamento**
**Acoplamento** mede o grau de interdependência entre módulos. Em uma boa arquitetura modular, o acoplamento deve ser baixo, o que significa que os módulos podem ser alterados, substituídos ou reutilizados com o mínimo de impacto em outros módulos.

**Tipos de acoplamento**:

1. **Acoplamento de Dados**: O nível mais fraco de acoplamento, onde os módulos compartilham apenas dados simples, como parâmetros primitivos.
2. **Acoplamento de Controle**: Quando um módulo controla o comportamento de outro, por exemplo, passando um sinal que altera o fluxo de execução.
3. **Acoplamento de Conteúdo**: O nível mais forte de acoplamento, onde um módulo acessa diretamente os dados internos de outro módulo, o que deve ser evitado.

- **Baixo acoplamento**: Módulos interagem principalmente por meio de interfaces bem definidas e compartilham o mínimo de dependências.
- **Alto acoplamento**: Módulos dependem diretamente dos detalhes de implementação um do outro, dificultando modificações e manutenções.

#### **Abstração**

**Abstração** envolve esconder os detalhes de implementação de um módulo e expor apenas o que é necessário para a interação com outros módulos. O uso de abstrações adequadas reduz o acoplamento entre os módulos, facilitando a evolução e a manutenção do sistema.

- **Interface**: Um meio comum de aplicar abstração é através da definição de interfaces. Elas descrevem o que o módulo faz sem revelar como isso é feito, permitindo substituições ou mudanças internas sem afetar os consumidores do módulo.

Exemplo:

- Em um sistema de pagamento, o módulo de pagamento pode oferecer uma interface para processar transações, mas como os pagamentos são processados internamente (via PayPal, Stripe, etc.) está oculto.

#### **Instabilidade**

**Instabilidade** é uma medida da probabilidade de um módulo sofrer alterações devido a mudanças em outros módulos. Quanto mais instável um módulo, maior a probabilidade de ele ser impactado por alterações externas. Um módulo instável tende a depender fortemente de outros e, por isso, é suscetível a mudanças no sistema.

- **Módulo estável**: Um módulo estável tem poucas ou nenhuma dependência de outros módulos. Normalmente, são módulos centrais ou utilitários que não precisam ser alterados com frequência.
- **Módulo instável**: Um módulo instável depende de muitos outros módulos e pode ser frequentemente impactado por mudanças externas.

#### **Distância da Sequência Principal**

A **Sequência Principal** (ou _Main Sequence_) é um conceito que se refere ao equilíbrio ideal entre **instabilidade** e **abstração**. A ideia é que um módulo ideal deve ser parcialmente abstrato (não completamente detalhado) e parcialmente instável (tendo algumas dependências externas controláveis).

- A fórmula para medir a distância da sequência principal é:  
    **Distância = |A + I - 1|**  
    Onde:
    - `A` é a medida de abstração (quanto um módulo está focado na definição de interfaces, em vez de implementações detalhadas).
    - `I` é a medida de instabilidade (quantas dependências um módulo tem).

Módulos próximos à sequência principal têm um bom equilíbrio entre abstração e instabilidade, tornando-os fáceis de manter e evoluir. Módulos distantes da sequência podem ser excessivamente dependentes ou excessivamente abstratos, dificultando sua utilização.

#### **Conascência**

**Conascência** é um termo que descreve o nível de dependência que um módulo tem sobre os detalhes de outro módulo. Quanto mais dependente um módulo é dos detalhes internos de outro, maior a conascência. A conascência é dividida em diferentes níveis de dependência:

1. **Conascência de Nome**: Quando um módulo depende de nomes específicos (como nomes de variáveis ou métodos) em outro módulo.
2. **Conascência de Tipo**: Quando um módulo depende de tipos de dados específicos definidos por outro módulo.
3. **Conascência de Algoritmo**: Quando um módulo depende da lógica interna de funcionamento de outro módulo.

A redução da conascência é desejável, pois permite que as partes do sistema sejam mais independentes e fáceis de alterar.