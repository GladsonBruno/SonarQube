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

O primeiro passo ao fazer gestão de qualidade do código fonte é definir qual desses pontos técnicos são mais importantes. Em seguida, com base na situação atual do projeto, estabelecer um plano para a melhoria contínua da qualidade do código fonte do projeto.



# Como o SonarQube funciona?

O SonarQube possui uma arquitetura bastante simples e flexível que é constituída por três componentes:

- Um conjunto de analisadores de código fonte que são acionados por demanda.

- Um banco de dados para mantêm os resultados de análises.

- Uma ferramenta *Web* para exibir painéis de qualidade de código sobre projetos, bugs, vulnerabilidades e etc.

  

Com esses componentes o SonarQube embarca as melhores ferramentas para analisar violações de regras de qualidade, bugs em potencial, cobertura de testes de unidade, violações de segurança, entre outros.



# Instalando o SonarQube



