### Conceito
- **Docker** é uma plataforma que facilita a criação, o envio e a execução de aplicações em containers. Ele isola o ambiente da aplicação, permitindo que ela funcione da mesma maneira, independentemente de onde seja executada, o que resolve o clássico problema de "funciona na minha máquina, mas não no servidor".
- Docker foi criado para facilitar a entrega contínua, a implementação rápida e a escalabilidade das aplicações. Ele permite a execução de várias instâncias de uma aplicação em um mesmo host, aproveitando ao máximo os recursos disponíveis, como CPU e memória.

### Diferenças entre Containers e Máquinas Virtuais
- **Container**: Compartilha o kernel do sistema operacional do host, tornando-o mais leve e rápido para inicializar. Ele isola a aplicação e suas dependências em um ambiente próprio, garantindo que não haja interferência com outras aplicações rodando no mesmo host.
    - **Leveza**: Containers são mais eficientes em termos de consumo de recursos.
    - **Isolamento**: Cada container roda sua própria instância de aplicação sem interferir em outros.
- **Máquina Virtual (VM)**: Em uma VM, você tem um sistema operacional completo rodando sobre um hipervisor, o que adiciona overhead de recursos, tornando-o mais lento e mais pesado.

### Componentes principais do Docker
- **Imagens**:
    - Uma **imagem** Docker é uma "fotografia" de um sistema de arquivos e suas dependências. As imagens são construídas a partir de camadas, onde cada comando no Dockerfile cria uma nova camada. Essas imagens são imutáveis, e qualquer alteração feita em um container durante a execução não afeta a imagem original.
        
    - Exemplo de comandos no Dockerfile:
        ```dockerfile
		# Usa uma imagem base oficial do Node.js
		FROM node:14
		
		# Define o diretório de trabalho
		WORKDIR /app
		
		# Copia o package.json e instala as dependências
		COPY package*.json ./ RUN npm install
		
		# Copia o restante dos arquivos
		COPY . .
		
		# Expondo a porta da aplicação
		EXPOSE 3000
		
		# Comando para iniciar a aplicação
		CMD ["npm", "start"]
		```
        
- **Containers**:
    - Um **container** é uma instância em execução de uma imagem. Quando você executa um container, ele roda de forma isolada, sem afetar o ambiente host.
    - Os containers podem ser executados, pausados, reiniciados e destruídos a qualquer momento sem perder o conteúdo armazenado na imagem.
    - Comando para executar um container:
        ```bash
        docker run -d -p 3000:3000 --name meu_app_container minha_imagem
        
        Isso cria um container da imagem `minha_imagem` e expõe a porta 3000 para acesso.
        ```
        
- **Dockerfile**:
    - O **Dockerfile** é um script que contém as instruções necessárias para criar uma imagem Docker. Ele define o sistema operacional base, as dependências da aplicação, as variáveis de ambiente e o comando principal que será executado.
- **Docker Compose**:
    - O **Docker Compose** é uma ferramenta que permite definir e rodar aplicações Docker com múltiplos containers. Ele usa um arquivo `docker-compose.yml` para especificar os serviços que compõem a aplicação, como um banco de dados, cache, e a aplicação principal.
        
    - Exemplo de `docker-compose.yml`:
        
        ```yaml
        version: '3'
        services:  
	        app:
		        image: minha_imagem
		        ports:
			        - "3000:3000"
			        - depends_on:
				        - db
			db:
				image: postgres
				environment:
					POSTGRES_PASSWORD: senha_secreta
        ```    
    
    Nesse exemplo, temos dois serviços: a aplicação e um banco de dados PostgreSQL. O Docker Compose garante que o banco de dados esteja pronto antes de iniciar a aplicação.
    
- **Volumes**:
    - **Volumes** são usados para persistir dados fora do ciclo de vida do container. Sem um volume, os dados dentro de um container são temporários e perdidos ao parar ou remover o container. Com volumes, é possível manter dados mesmo após o container ser removido.
        
    - Exemplo de criação de volume:    
        ```bash
		docker run -d -v /meus_dados:/app/dados minha_imagem
		```
        
        Isso mapeia o diretório `/meus_dados` no host para `/app/dados` no container.
        
- **Networking**:
    
    - Docker permite que você crie redes entre containers para facilitar a comunicação entre eles. Existem três tipos principais de redes:
        
        1. **Bridge**: A rede padrão para containers em um host. Os containers podem se comunicar entre si e com o host.
        2. **Host**: Faz o container compartilhar a rede do host, removendo a necessidade de mapeamento de portas.
        3. **Overlay**: Permite a comunicação entre containers em diferentes hosts (usado em orquestração).
    - Comando para criar uma rede bridge:
        ```bash
        docker network create minha_rede
        ```
        

### Comandos importantes

- **`docker build`**: Constrói uma imagem a partir de um Dockerfile.    
    ```bash
    docker build -t minha_aplicacao .
    ```
    Isso cria uma imagem chamada `minha_aplicacao` a partir do diretório atual, onde o Dockerfile está localizado.
    
- **`docker exec`**: Executa um comando dentro de um container em execução.
    ```bash
    docker exec -it meu_container bash
    ```
    Isso abre um terminal `bash` dentro do container `meu_container`.
    
- **`docker logs`**: Exibe os logs de um container em execução.    
    ```bash
    docker logs meu_container
    ```
    
- **`docker inspect`**: Mostra informações detalhadas sobre um container ou imagem.    
    ```bash
    docker inspect meu_container
    ```
    
- **`docker prune`**: Remove containers, imagens e volumes não utilizados para liberar espaço.
    ```bash
    docker system prune -a
    ```
    
- **`docker ps`**: Visualiza quais containeres estão rodando.
	```bash
	docker ps
	```
	
- **`docker ps -a`**: Visualiza quais containeres existem e não estão rodando.
	```bash
	docker ps -a
	```
	
- **`docker image ls`**: Visualiza quais imagens tem baixado.
	```bash
	docker image ls
	```


### Principais vantagens
- **Isolamento**: Cada container roda de forma independente, sem interferir no sistema host ou em outros containers.
- **Eficiência de recursos**: Containers são muito mais leves que máquinas virtuais, consumindo menos memória e CPU.
- **Portabilidade**: Uma aplicação Dockerizada pode rodar em qualquer ambiente que suporte Docker, desde servidores locais até a nuvem.
- **Escalabilidade**: Docker permite a execução de várias instâncias de containers, facilitando o balanceamento de carga e a escalabilidade horizontal.

### Desvantagens
- **Complexidade**: Embora Docker facilite muito o desenvolvimento e a produção, seu ecossistema pode ser complexo para iniciantes, principalmente quando se trata de orquestração (usando ferramentas como Kubernetes).
- **Persistência**: O gerenciamento de dados persistentes pode ser desafiador sem a configuração correta de volumes.