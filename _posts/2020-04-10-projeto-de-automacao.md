---
toc: true
layout: post
description: Existem diversos pontos para a validade da qualidade do projeto
categories: [QA, teste, projeto]
title:  Projeto de automação para qualidade do software
---

# Projeto de automação para qualidade do software

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/projeto_de_bdd.png)

Existem diversos pontos para a validade da qualidade do projeto, o que mais se identifica com usuário é o BDD (Behavior Driven Development) Desenvolvimento Guiado a Comportamento, usando essa técnica podemos identificar falhas mais reais e são corrigidas instantaneamente, devido sua agilidade e forma de aplicar. 

# **Por que usar BDD e qual sua estratégia?**

O BDD ajuda a analisar o comportamento a ser realizado pelo usuário, sendo mais humana e tendo a visão em que o usuário esta, isso da mais clareza na analise economizando tempo. 

Sendo uma documentação viva e com especificação clara. Escrevendo os critérios de aceite, ajuda no desenvolvimento do contexto "Done", assim facilita as entregas. Colocando o processo de qualidade junto com o desenvolvimento. 

O uso dela é iniciado no dia da planning, neste dia temos que tirar nossas dividas, é um ótimo dia para conhecer mais sobre o produto e as regras. Quando não temos uma user story bem definida, tentamos melhora-la e criando um  contexto melhor sobre critérios de aceite em cada task.

No período do desenvolvimento o Dev e o QA, seguem desenvolvendo juntos pois a criação das features também ajuda o dev a compreender melhor no que será desenvolvido, usando o conceito de CI/CD para ajudar e deixar mais ágil. Aplicando o versionamento de código e a utilização de Docker, facilita na hora de validação em pequenos casos de testes.

Temos como palavras chaves para realizarmos uma estratégia; Given, When, Then

```gherkin
 'Given' é a condição  estado, parâmetros relevantes para o cenário especifico. 

 'When' é uma mudança de estado, o que queremos testar

 'Then' é o resultado esperado
```

Seguindo essas palavras chaves temos como exemplo;

```gherkin
###TRANSPBACK001
  Scenario: Cadastrar Transportadora Pessoa Jurídica 
    When eu estou logado no sistema Backoffice do Carguero "qadev@teste.net" "senha"
    And eu estou na tela de Criação da Transportadora do BackOffice
    And eu visualizo todos os campos desabilitados da transportadora do backoffice exceto o tipo de documento
    And eu habilito o tipo de documento como CNPJ da transportadora no sistema BackOffice
    And eu visualizo todos os campos desabilitados da transportadora do backoffice exceto o tipo de documento e CNPJ
    And eu informo o CNPJ da transportadora no sistema BackOffice
    And eu informo os demais dados obrigatórios do documento da transportadora no sistema BackOffice
    And eu informo os dados obrigatórios do contato da transportadora no sistema BackOffice
    And eu informo os dados obrigatórios do endereço da transportadora no sistema BackOffice
    And eu anexo o comprovante de endereço da transportadora no sistema BackOffice
    And eu adiciono informações bancárias da transportadora no sistema BackOffice
    And eu adiciono uma validação Sintegra da transportadora no sistema BackOffice
    And eu adiciono uma validação da Receita Federal da transportadora no sistema BackOffice
    And eu adiciono uma validação ANTT da transportadora no sistema BackOffice
    And eu clico no botão de salvar os dados da transportadora no sistema BackOffice
    Then eu recebo a mensagem de salvo com sucesso da transportadora no sistema BackOffice
    And eu sou redirecionado para tela de listagem de da transportadora do sistema BackOffice
```

Do que usarmos validações demoradas como Excel, usando o BDD temos uma formatação mais clara e objetiva. São vários casos de teste dentro de um único arquivo (daquele contexto), isso ajuda no suporte e no final conseguimos rodar mais rápido. 

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/plano.png)



# Na **Pratica**

Depois da Planning, ja temos o entendimento do produto, seguimos com a construção do cenário de teste usando o BDD.

 **Criando o cenário de teste usando Cucumber.**
 Na imagem temos a estrutura de automação de testes seguindo com cenários de testes e em cada cenário tem os casos de testes. Dividindo em situações diferentes e por ordem.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/Cucumber.png)

Aqui temos os casos de testes.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/casos_de_testes.jpeg)

Mostrando mais casos de testes

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/Mostrandomaiscasosdetestes.jpeg)

**Criando automação para validação**
Aqui foi usado webdriverIO (uma ferramenta em javascript para automação de testes, utilizando API do selenium, sendo rápido e fácil). Na imagem temos a estrutura do webdriverIO para rodar os testes.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/conf.WEBDRIVERIO.png)



 Usando um padrão de projeto, ajuda a dar suporte nos testes. Usando PAGE OBJECTS, classificando cada elemento da pagina WEB.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/PageO.png)

 Em steps, é onde escrito o código para rodar cada caso teste e sendo guiado pela feature.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/steps.jpeg)

 No final temos o ALLURE, onde temos um dashbord construído em html, mostrando detalhadamente cada caso de teste, se passaram ou não.

![]({{ site.baseurl }}/images/2020-04-10-projeto-de-automacao/allure.jpeg)

Isso tudo foi criando para uma plataforma de grande porte, sendo utilizado na parte WEB, APP e API.

Quando usamos user story com o BDD, para construção de casos de teste, facilita a manutenção e torna o processo mais rápido.

# **LINKS**

[Projeto BDD](https://www.belatrixsf.com/whitepapers/project-behavior-driven-development/) 

[BDD and Cucumber](https://dev.to/bushraalam/bdd-and-cucumber-24di)

[Modelo Pratico](https://github.com/Rodscaloppe/Olxx)

[Vamos falar de BDD - Behaviour Driven Development](https://medium.com/@danilow86/vamos-falar-de-bdd-behaviour-driven-development-18d6dc4cc038)

[O que é BDD-Behaviour Driven Development? Entenda](https://www.youtube.com/watch?v=HH-m46ldctw)

[Teste Unitário, TDD e BDD – Qual a diferença?](https://dev.to/shadowlik/teste-unitario-tdd-e-bdd-qual-a-diferenca-39e)