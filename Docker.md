# Oque é docker em palavras simples?

Docker é uma plataforma de containerização que permite que você empacote seu código, configurações e dependências em um container, que é como uma caixa virtual que pode ser facilmente movida de um ambiente para outro. Isso é útil porque garante que o seu código irá funcionar da mesma maneira em qualquer lugar, independentemente do sistema operacional ou configuração do ambiente.

Usando Docker, é possível criar imagens que são como modelos de containers prontos para serem usados. Essas imagens podem ser compartilhadas com outras pessoas, o que facilita a colaboração em projetos de código aberto ou o desenvolvimento de aplicações em equipe. Além disso, o Docker permite que você gerencie facilmente vários containers em execução no mesmo host, o que é útil para aplicações distribuídas ou em nuvem.	

# Como baixar o docker no Windows

Para baixar o Docker no Windows, siga os seguintes passos:

1. Acesse o site do Docker (https://www.docker.com/) e clique no botão "Get Docker" na página inicial.
2. Clique no botão "Download for Windows" na página seguinte.
3. Clique no botão "Download from Docker Hub" para baixar o instalador do Docker.
4. Quando o download terminar, clique duas vezes no instalador para iniciar o processo de instalação.
5. Siga as instruções na tela para completar a instalação do Docker.
6. Quando a instalação estiver concluída, inicie o Docker clicando no ícone do Docker na área de trabalho ou na barra de tarefas.
7. Siga as instruções na tela para configurar o Docker e começar a usá-lo.

É importante notar que o Docker requer o Windows 10 Pro ou Enterprise com Hyper-V ativado. Se você não tiver o Windows 10 Pro ou Enterprise, poderá usar o Docker Toolbox, que é uma versão antiga do Docker que funciona em sistemas operacionais mais antigos. No entanto, o Docker Toolbox não é tão rápido ou eficiente quanto o Docker para Windows e não é recomendado para uso em produção.

# Oque é  Dockerfile ?

O Dockerfile é um arquivo de texto que contém as instruções necessárias para construir uma imagem Docker. Ele é usado pelo comando `docker build` para criar uma imagem Docker a partir de um projeto específico.

Um Dockerfile geralmente começa com uma instrução `FROM`, que especifica qual imagem de base deve ser usada para criar a imagem. Em seguida, podem ser adicionadas instruções adicionais para instalar pacotes, copiar arquivos e configurar o container.

# Para adicionar Docker ao seu projeto Java com JDK 17 e PostgreSQL, siga os seguintes passos:

1. Instale o Docker em sua máquina, seguindo as instruções da documentação do Docker.

2. Crie um arquivo chamado "Dockerfile" na raiz do seu projeto Java. Este arquivo irá conter as instruções para construir a imagem Docker do seu projeto.

3. Adicione as seguintes instruções ao seu Dockerfile:

4. ```
   FROM openjdk:17-jdk
   RUN apt-get update && apt-get install -y postgresql-client
   ADD target/nome-do-seu-projeto.jar nome-do-seu-projeto.jar
   EXPOSE 8080
   ENTRYPOINT ["java","-jar","nome-do-seu-projeto.jar"]
   
   ```

   

5. Substitua "nome-do-seu-projeto" pelo nome do arquivo JAR do seu projeto.

6. Abra o terminal e navegue até a raiz do seu projeto.

7. Execute o comando "docker build -t nome-da-sua-imagem ." para construir a imagem Docker do seu projeto. Substitua "nome-da-sua-imagem" pelo nome que você deseja dar à sua imagem.

8. Execute o comando "docker run -p 8080:8080 nome-da-sua-imagem" para iniciar o container Docker do seu projeto e expor a porta 8080 do container para a porta 8080 da máquina host.

9. Acesse a URL "[http://localhost:8080](http://localhost:8080/)" para verificar se o seu projeto está funcionando corretamente no container Docker.

É importante notar que esses são apenas alguns passos gerais para adicionar Docker ao seu projeto Java com JDK 17 e PostgreSQL e que o processo pode variar de acordo com o seu projeto específico e as opções de configuração do Docker.

# Para subir uma imagem Docker no Docker Hub usando o terminal, siga os seguintes passos:

Crie uma conta no Docker Hub se você ainda não tiver uma. É possível criar uma conta gratuita ou pagar por uma conta premium, dependendo das suas necessidades.

Abra o terminal e faça login na sua conta do Docker Hub usando o comando:

```
docker login
```

Para subir uma imagem Docker no Docker Hub usando o terminal, siga os seguintes passos:

Crie uma conta no Docker Hub se você ainda não tiver uma. É possível criar uma conta gratuita ou pagar por uma conta premium, dependendo das suas necessidades.

Abra o terminal e faça login na sua conta do Docker Hub usando o comando:

```
Copy code
docker login
```

Será solicitado que você informe o seu nome de usuário e senha do Docker Hub.

Navegue até a pasta que contém a imagem Docker que você deseja subir.

Dê um nome à sua imagem usando o comando:

```
docker tag nome-da-sua-imagem nome-de-usuario/nome-da-sua-imagem:tag
```

Substitua "nome-da-sua-imagem" pelo nome da imagem local e "nome-de-usuario" pelo seu nome de usuário no Docker Hub. Você também pode adicionar uma tag à sua imagem, como "latest" ou "versão-1.0", para ajudar a identificar diferentes versões da imagem.

Envie a imagem para o Docker Hub usando o comando:

```
docker push nome-de-usuario/nome-da-sua-imagem:tag
```

Isso pode levar algum tempo, dependendo do tamanho da imagem e da velocidade da sua conexão com a internet.

Verifique se a imagem foi enviada corretamente acessando



# Oque é docker-compose?

O Docker Compose é uma ferramenta para criar e gerenciar aplicações compostas por múltiplos containers Docker. Ele permite que você defina todos os containers, volumes de dados e outros recursos necessários para a sua aplicação em um único arquivo de configuração, facilitando o gerenciamento e o deploy da aplicação em diferentes ambientes.

Para usar o Docker Compose, você precisa criar um arquivo de configuração chamado "docker-compose.yml", que define as configurações de todos os containers, volumes e outros recursos da sua aplicação. Cada seção do arquivo de configuração representa um container e inclui informações como a imagem Docker a ser usada, as portas expostas, as variáveis de ambiente e os volumes de dados.

Uma vez que o arquivo de configuração estiver pronto, basta executar o comando "docker-compose up" para iniciar todos os containers da aplicação. O Docker Compose também oferece comandos para parar, reiniciar e gerenciar os containers da aplicação de maneira mais fácil.

O Docker Compose é uma ferramenta muito útil para desenvolvimento e teste de aplicações compostas por múltiplos containers, pois permite que você configure e gerencie facilmente todos os containers em um único lugar. Além disso, o Docker Compose é compatível com várias plataformas, incluindo Windows, Linux e macOS, o que o torna uma opção versátil para gerenciamento de aplicações Docker.

# Para criar um projeto Java com Dockerfile e Docker Compose com PostgreSQL e MySQL, siga os seguintes passos:

Crie um arquivo Dockerfile para a aplicação Java. Adicione as instruções para instalar o Java 17, baixar o projeto Maven e construir a aplicação. Por exemplo:

```Docker
FROM maven:3.6.3-openjdk-17 as build

COPY . /app
WORKDIR /app

RUN mvn clean install

FROM openjdk:17-jdk-slim

COPY --from=build /app/target/*.jar /app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar"]

```

Crie um arquivo Dockerfile para cada banco de dados e adicione as instruções para instalar e iniciar os bancos de dados. Por exemplo, se você estiver usando o PostgreSQL e o MySQL, os seus arquivos Dockerfile poderiam ser algo como:

Arquivo Dockerfile para PostgreSQL:

```
FROM postgres:latest

ENV POSTGRES_DB nome-do-seu-banco-de-dados-postgres
ENV POSTGRES_USER nome-do-seu-usuario
ENV POSTGRES_PASSWORD sua-senha

EXPOSE 5432

```

Arquivo Dockerfile para MySQL:

```
FROM mysql:latest

ENV MYSQL_DATABASE nome-do-seu-banco-de-dados-mysql
ENV MYSQL_USER nome-do-seu-usuario
ENV MYSQL_PASSWORD sua-senha
ENV MYSQL_ROOT_PASSWORD sua-senha-de-root

EXPOSE 3306

```

Crie um arquivo docker-compose.yml que defina os três containers da aplicação: os dois bancos de dados e o container da aplicação Java. No arquivo de configuração, defina as dependências entre os containers e as portas expostas para cada um deles. Por exemplo:

```dockerfile
version: '3'
services:
  db-postgres:
    build:
      context: .
      dockerfile: Dockerfile-postgres
    container_name: db-postgres
    ports:
      - "5432:5432"
  db-mysql:
    build:
      context: .
      dockerfile: Dockerfile-mysql
    container_name: db-mysql
    ports:
      - "3306:3306"
  app:
    build:
      context: .
      dockerfile: Dockerfile-app
    container_name: app
    depends_on:
      - db-postgres
      - db-mysql
    ports:
      - "8080:8080"

```

Defina as dependências entre os containers. No exemplo acima, o container da aplicação depende dos dois bancos de dados, o que significa que eles devem ser iniciados primeiro.

Defina as portas expostas para cada um dos containers. No exemplo acima, a porta 8080 do container da aplicação Java é exposta para a porta 8080 da máquina host. Isso significa que a aplicação poderá ser acessada pelo navegador na URL "localhost:8080".

Salve o arquivo docker-compose.yml.



Certifique-se de que as dependências do Spring Boot estejam configuradas no arquivo `pom.xml` do seu projeto:

```java
<dependencies>
  ...
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
  </dependency>
  <dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
  </dependency>
  <dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
  </dependency>
  ...
</dependencies>

```



Para criar uma imagem Docker de um projeto que já possui um Dockerfile e um Docker Compose, siga os seguintes passos:

- Acesse a pasta do projeto pelo terminal.

- Execute o comando "docker-compose build" para construir as imagens dos containers da aplicação. O comando irá ler as instruções dos arquivos Dockerfile e criar as imagens correspondentes.

- Verifique se as imagens foram criadas com o comando "docker images". Devem aparecer na lista as imagens dos containers da aplicação, incluindo a imagem da aplicação Java, do PostgreSQL e do MySQL.

- Se desejar, você pode dar um nome e uma tag à imagem da aplicação Java com o comando "docker tag [nome-da-imagem] [nome-do-repositorio]:[tag]". Por exemplo:

- ```
  docker tag app meu-repositorio/app:1.0
  ```

- Se quiser enviar a imagem para o Docker Hub ou outro repositório de imagens, execute o comando "docker push [nome-do-repositorio]:[tag]". Por exemplo:

- ```
  docker push meu-repositorio/app:1.0
  ```

  Agora, a imagem da aplicação Java está disponível no Docker Hub ou no repositório de imagens que você escolheu. Você pode usá-la para criar containers da aplicação em qualquer máquina com o Docker instalado.

  

Observação: você deve substituir [nome-do-seu-projeto], [nome-do-seu-banco], [nome-do-usuario] e [senha-do-usuario] pelos valores adequados para o seu projeto. Além disso, é importante garantir que o arquivo `application.properties` ou `application.yml` do seu projeto tenha as configurações de banco de dados corretas para se conectar ao PostgreSQL e ao MySQL.

# Configuraçoes application.properties para postgreSql e MySQL.



## Para configurar o Spring Boot para se conectar ao PostgreSQL e ao MySQL, você pode adicionar as seguintes propriedades ao arquivo `application.properties` do seu projeto:



Para o PostgreSQL:

```
spring.datasource.url=jdbc:postgresql://[host]:[porta]/[nome-do-banco]
spring.datasource.username=[nome-do-usuario]
spring.datasource.password=[senha-do-usuario]
spring.datasource.driver-class-name=org.postgresql.Driver

```



Para o MySQL:

```
spring.datasource.url=jdbc:mysql://[host]:[porta]/[nome-do-banco]
spring.datasource.username=[nome-do-usuario]
spring.datasource.password=[senha-do-usuario]
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

```

Observação: você deve substituir [host], [porta], [nome-do-banco], [nome-do-usuario] e [senha-do-usuario] pelos valores adequados para o seu banco de dados. Além disso, é importante garantir que o driver JDBC do banco de dados esteja incluído como uma dependência do projeto.

## Se você estiver usando o arquivo `application.yml`, as propriedades devem ser adicionadas da seguinte forma:

Para o PostgreSQL:

```
spring:
  datasource:
    url: jdbc:postgresql://[host]:[porta]/[nome-do-banco]
    username: [nome-do-usuario]
    password: [senha-do-usuario]
    driver-class-name: org.postgresql.Driver

```

Para o MySQL:

```
spring:
  datasource:
    url: jdbc:mysql://[host]:[porta]/[nome-do-banco]
    username: [nome-do-usuario]
    password: [senha-do-usuario]
    driver-class-name: com.mysql.cj.jdbc.Driver

```

Observação: assim como no arquivo `application.properties`, você deve substituir [host], [porta], [nome-do-banco], [nome-do-usuario] e [senha-do-usuario] pelos valores adequados para o seu banco de dados. Além disso, é importante garantir que o driver JDBC do banco de dados esteja incluído como uma dependência do projeto.

## Tenho que ter a pasta dockerFile se eu tiver a docker compose?

O arquivo Dockerfile é usado para construir uma imagem Docker a partir de um projeto. Ele contém as instruções para o Docker construir a imagem do seu projeto, incluindo as configurações de sistema, bibliotecas e pacotes necessários, além de definir o ponto de entrada da sua aplicação.

Já o arquivo docker-compose.yml é usado para definir e executar aplicações multi-container usando o Docker Compose. Ele contém as configurações dos containers que serão executados, incluindo as imagens Docker que serão usadas, as variáveis de ambiente e os volumes de dados compartilhados entre os containers.

Portanto, é possível que você precise de ambos os arquivos, dependendo da estrutura e das necessidades do seu projeto. O arquivo Dockerfile é usado para construir a imagem Docker do seu projeto, enquanto o arquivo docker-compose.yml é usado para gerenciar e executar os containers da sua aplicação.



