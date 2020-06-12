# Introdução

Neste workshop abordaremos a ferramenta SonarQube e como ela pode ser útil para a análise e melhoria de qualidade de código de suas aplicações.



# O que é SonarQube?

O SonarQube é uma plataforma de código aberto desenvolvida pela SonarSource, ele é usado por equipes de desenvolvimento para o gerenciamento da qualidade de código fonte.

O SonarQube fornece análise e integração totalmente automatizadas com Maven, Ant, Gradle, MSBuild e ferramentas de integração contínua ( Atlassian Bamboo, Jenkins, Hudson, etc).

Atualmente a versão gratuita do SonarQube (Community Edition) fornece suporte para 15 linguagens de programação distintas.





# Por que gerenciar a qualidade do código fonte?

Para responder essa pergunta leve em consideração a seguinte citação:

*“Um programa bem escrito é um programa em que o custo de implementação de um recurso é constante ao longo de toda a vida do programa” – Itay Maman*

Como uma introdução rápida, esta é a melhor definição de qualidade de código fonte. Fica ainda mais forte quando colocado o contrário: *um programa mal escrito é um programa onde o custo de implementação de uma característica cresce ao longo do tempo.*

Com isso podemos compreender a importância da qualidade de código fonte.



# Como gerenciar a qualidade do código fonte?

Existem alguns pontos técnicos que devem ser analisados quando se faz a análise de código fonte de um projeto sendo eles:

- Descumprimento dos padrões de codificação e de melhores práticas
- Duplicadas de código
- Componentes complexos ou/e má distribuição dos componentes entre complexidade
- Baixa cobertura de código, testes unitários, especialmente na parte complexa do programa
- Possíveis *bugs*

O SonarQube é capaz de identificar esses dentre outros problemas que podem afetar a qualidade do código fonte de uma aplicação.

O primeiro passo ao fazer gestão de qualidade do código fonte é definir qual desses pontos técnicos são mais importantes. 

Em seguida, com base na situação atual do projeto, estabelecer um plano para a melhoria contínua da qualidade do código fonte do projeto.



# Como o SonarQube funciona?

O SonarQube possui uma arquitetura bastante simples e flexível que é constituída por três componentes:

- Um conjunto de analisadores de código fonte que são acionados por demanda.

- Um banco de dados para mantêm os resultados de análises.

- Uma ferramenta *Web* para exibir painéis de qualidade de código sobre projetos, bugs, vulnerabilidades e etc.

  

Com esses componentes o SonarQube embarca as melhores ferramentas para analisar violações de regras de qualidade, bugs em potencial, cobertura de testes de unidade, violações de segurança, entre outros.



# Instalando o SonarQube

A instalação do SonarQube é bem simples.

O único requisito para utilização do SonarQube é possuir a versão correta do Java instalada em sua máquina.

Recomendamos o download da versão 7.8 pois ela é a versão mais recente com suporte para o Java 8, as demais versões existem o Java 11.

Primeiro precisaremos acessar o seguinte este [link]( https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.8.zip) para realizar o download desta versão do SonarQube.  

Após realizar o download extraia o diretório **sonarqube-7.8** do arquivo **.zip** baixado.

Com o diretório **sonarqube-7.8** aberto acesse o diretório **bin**, dentro do diretório **bin** abra o subdiretório correspondente ao seu sistema operacional:

<img src="imagens/exemplo-1.png" style="float: left"/>

Nas versões **Linux** ou **MacOs** execute o arquivo **sonar.sh** para iniciar o SonarQube.

Na versão **Windows** execute o arquivo **StartSonar.bat**, na versão windows também é possível instalar o SonarQube como serviço executando o arquivo **InstallNTService.bat**.

Após iniciar o SonarQube acesse o seguinte endereço para acessar o SonarQube: **http://localhost:9000**.

Com o SonarQube aberto veremos algo semelhante a isso:

<img src="imagens/exemplo-2.png"/>



# Efetuando login no SonarQube

Por padrão o login e senha do SonarQube são:

**Usuário: admin**

**Senha: admin**

Essa senha pode ser alterada posteriormente.

Após efetuar o login no SonarQube veremos a seguinte tela:

<img src="imagens/exemplo-3.png">



Como ainda não criamos nenhum projeto no SonarQube não teremos nenhuma informação de projetos no painel.



# Configurando o SonarScanner do Maven

 O SonarScanner é recomendado como o analisador padrão para projetos Maven. 

Para utilizá-lo é necessário realizar uma configuração global no Maven, para isso precisaremos editar o arquivo **settings.xml** localizado em  **$MAVEN_HOME/conf** ou **~/.m2**  para definir o prefixo do plug-in e, opcionalmente, o URL do servidor SonarQube. 

A configuração final será semelhante a isso:

```xml
<settings>
    <pluginGroups>
        <pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
    </pluginGroups>
    <profiles>
        <profile>
            <id>sonar</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <sonar.host.url>
                  http://localhost:9000
                </sonar.host.url>
            </properties>
        </profile>
     </profiles>
</settings>
```





# Configurando um projeto Maven no SonarQube

Agora iremos configurar nosso primeiro projeto no SonarQube, para isso utilizaremos um projeto de exemplo que pode ser baixado no seguinte **link[ALGUM LINK AQUI]**.

O projeto de exemplo é uma API de produtos feita com Java e SpringBoot utilizando o gerenciador de dependências Maven.

Após extrair o projeto do arquivo **.zip** crie um arquivo chamado **sonar-project.properties** na pasta raiz do projeto com o seguinte conteúdo:

```properties
sonar.projectKey=com.example:api-produtos
sonar.projectVersion=1.0.0
sonar.sources=.
sonar.sourceEncoding=UTF-8
```

A propriedade **sonar.projectKey** define a chave exclusiva do projeto. O valor padrão para projetos Maven é **groupId: artifactId**

A propriedade **sonar.projectVersion** define a versão do projeto.

A propriedade **sonar.sources** define  caminhos separados por vírgula para diretórios que contêm arquivos do projeto.  Quando não fornecido o valor padrão é o diretório base do projeto.

A propriedade **sonar.sourceEncoding** define a codificação do sistema **como UTF-8**.

Para saber mais sobre as propriedades de configuração disponíveis acesse este [link]( https://docs.sonarqube.org/7.8/analysis/analysis-parameters/ ).



Após a criação do arquivo **sonar-project.properties** abra um prompt de comando na pasta raiz do projeto e execute o seguinte comando:

```shell
mvn clean compile sonar:sonar
```

Após alguns minutos nosso projeto será compilado e criado no Sonar Qube.

Para visualizar os projetos criados acesse o seguinte link:  http://localhost:9000/projects



