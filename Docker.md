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

# Para adicionar o Docker Compose ao seu projeto com Java 17, PostgreSQL, MySQL e Spring Boot, você pode seguir os seguintes passos:

1. Instale o Docker e o Docker Compose em seu sistema.

2. Crie um arquivo `Dockerfile` na raiz do seu projeto com o seguinte conteúdo:

3. ```Docker
   FROM openjdk:17-jdk
   
   ADD target/[nome-do-seu-projeto].jar [nome-do-seu-projeto].jar
   
   EXPOSE 8080
   
   ENTRYPOINT ["java", "-jar", "[nome-do-seu-projeto].jar"]
   ```

   

4. Crie um arquivo `docker-compose.yml` na raiz do seu projeto com o seguinte conteúdo:

5. ```dockerfile
   version: '3'
   
   services:
     app:
       build: .
       image: nome-da-sua-imagem
       ports:
         - "8080:8080"
       depends_on:
         - postgres
         - mysql
       environment:
         - DATABASE_URL=jdbc:postgresql://postgres:5432/[nome-do-seu-banco]
         - MYSQL_DATABASE_URL=jdbc:mysql://mysql:3306/[nome-do-seu-banco]
     postgres:
       image: postgres:12
       environment:
         POSTGRES_USER: usuario
         POSTGRES_PASSWORD: senha
         POSTGRES_DB: nome-do-banco-de-dados
       ports:
         - "5432:5432"
     mysql:
       image: mysql:8
       environment:
         MYSQL_USER: usuario
         MYSQL_PASSWORD: senha
         MYSQL_DATABASE: nome-do-banco-de-dados
       ports:
         - "3306:3306"
   
   ```

   

6. Certifique-se de que as dependências do Spring Boot estejam configuradas no arquivo `pom.xml` do seu projeto:

7. ```java
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

   

8. Execute o seguinte comando para construir a imagem Docker do seu projeto:

9. ```
   docker-compose build
   
   ```

10. Execute o seguinte comando para criar e iniciar os containers:

11. ```
    docker-compose up
    ```

    

12. Seu projeto estará disponível em `http://localhost:8080`.

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