---
toc: false
layout: post
description: Criando um script de teste de carga favorita.
categories: [carga, k6]
title: Como escrever um plano de teste de carga
comments: true
---
##### _Por Nicole van der Hoeven_

Como escrever um plano de teste de carga


Muitas vezes as pessoas começam o teste de carga criando um script em sua ferramenta de teste de carga favorita, mas um bom teste de carga começa antes disso. Planejar um teste de carga pode parecer um exercício tedioso, mas é essencial para garantir o sucesso de seu teste.

Um plano de teste deve responder por que, o quê, quem, quando e como o teste será realizado.

Um bom plano de teste, especialmente para teste de carga, inclui os seguintes componentes:

    Requisitos
    Alcance
    Critério de entrada
    Modelagem de carga de trabalho
    Monitoramento de servidor
    Teste de duplas
    Cenários de teste

Vamos mergulhar em cada um deles, mas primeiro, uma nota sobre o formato de um plano de teste.
Formato do plano de teste

Os planos de teste são tradicionalmente apresentados como um documento, mas não existe uma regra rígida e rápida. Em vez disso, a extensão de um plano de teste e o nível de detalhes em que ele é aplicado devem ser ajustados de acordo com a complexidade do projeto e os antecedentes das partes interessadas.

As equipes que usam metodologias Agile podem não ter um plano de teste formal, mas eu diria que todas as equipes ainda devem ter algum tipo de plano, seja um documento do Word ou uma lista de marcadores. Planos escritos esclarecem e comunicam a intenção, e o teste pode ser um exercício caro e infrutífero sem um consenso sobre sua intenção.

A documentação técnica pode ser difícil de digerir e entender, e isso é perigoso quando se trata de desenvolvimento e teste de software, em que é imperativo que todas as partes interessadas estejam na mesma página sobre o estado de um aplicativo.

Paul McLean, um engenheiro de desempenho, tem uma solução criativa para isso. Ele cria um vídeo complementar para cada relatório técnico, dando às partes interessadas a opção de ler o relatório escrito para obter detalhes, mas assistir ao vídeo para obter uma explicação mais detalhada e detalhada.

Aqui está um exemplo de um vídeo complementar que ele criou para um plano de teste:
Requisitos

Tudo começa com requisitos. Até que os requisitos sejam identificados, o teste de carga só pode ser sem objetivo e explicativo, e quaisquer gargalos de desempenho detectados serão acidentais.

Os requisitos informam todas as etapas do processo de teste de carga. Por que estamos fazendo testes de carga? O que exatamente queremos testar? Como saberemos quando um teste foi aprovado ou reprovado? Como saberemos se o desempenho do aplicativo é bom o suficiente para entrar em produção? O que significa “bom o suficiente”?

Essa é uma parte tão importante do processo de planejamento que achei que merecia sua própria postagem no blog. Veja aqui: Comece com o porquê: como escrever requisitos para o teste de carga da API . Embora eu mencione especificamente o teste de carga da API, os princípios se aplicam ao teste de carga em geral.
Alcance

Na Flood, usamos uma metodologia de desenvolvimento de produto chamada Shape Up para nos manter no caminho certo enquanto criamos novos recursos. Os projetos no Shape Up são chamados de “trabalho modelado” e uma das propriedades básicas do trabalho modelado é que ele é limitado.

    … Trabalho modelado [também] indica o que não fazer. Diz à equipe onde parar. Existe um apetite específico - a quantidade de tempo que a equipe pode dedicar ao projeto. Concluir o projeto dentro desse período de tempo fixo requer limitar o escopo e deixar coisas específicas de fora.- Ryan Singer, Shape Up: Stop Running in Circles and Ship Work that Matters

Definir o escopo é definir limites. As prioridades de negócios precisam ser pesadas em relação às limitações de recursos (número de pessoas disponíveis para fazer o trabalho e tempo disponível) para que o teste forneça o valor máximo.

Algumas considerações de escopo incluem:

    Recursos específicos ou transações principais a serem testadas
    Tipos de testes incluídos (teste de componente vs teste de ponta a ponta)
    Cenários de teste (teste de pico de carga vs recuperação de desastre)
    Aplicativos incluídos no teste

Como acontece com a maioria das coisas na fase de planejamento, o escopo é algo que pode mudar durante o teste, quando surgem circunstâncias inesperadas ou quando as prioridades mudam. Mas ainda é uma boa prática definir o escopo no início e atualizá-lo conforme ele muda.

É importante, no entanto, podar com intenção . Mantendo nossos objetivos em mente, podemos manter nosso trabalho alinhado com nossas intenções.
Critério de entrada

Ocasionalmente, pode ser solicitado que você faça o teste de carga de um aplicativo que não está pronto para o teste de carga. Isso acontece com mais frequência do que você pensa. Embora seja verdade que o Teste de Desempenho é algo que deve ser incorporado a todo o desenvolvimento de software desde o início, isso não se aplica ao Teste de Carga. O teste de carga é apenas uma atividade que cai sob o guarda-chuva mais amplo de teste de desempenho.

Os critérios de entrada são condições que você precisa cumprir antes de o teste realmente começar. É uma boa ideia ter essas condições comunicadas com antecedência, para que todos saibam o que precisa ser configurado antes que você possa fazer seu trabalho.
Teste funcional: o aplicativo funciona?

O teste de carga não pode ser realizado de forma realista até que pelo menos a funcionalidade principal tenha sido testada e os defeitos de alta gravidade corrigidos. Dependendo do tipo de teste de carga que você deseja executar, você também pode especificar que o UAT foi executado, já que não faz sentido fazer um teste de carga de ponta a ponta com 1000 usuários se não funcionar para um usuário.
Ambiente de teste de carga: é semelhante à produção?

O teste não funcional tem requisitos mais rígidos para um ambiente do que o teste funcional, e você pode ter que defender essa causa. Para o teste de carga, não é suficiente ter um ambiente de preparação de aplicativos que seja uma máquina virtual com um quarto do tamanho do ambiente de produção. É importante chegar o mais próximo possível de um ambiente semelhante ao de produção em termos de capacidade (memória, CPU), base de código (o build real que será implantado) e integrações com outros ambientes ou servidores (se dentro do escopo de teste).

O teste de carga não é linear: um tempo de resposta de 5 segundos em um servidor com metade da capacidade do servidor de produção não equivale necessariamente a um tempo de resposta de 2,5 segundos em produção.

Este também é o momento de pensar sobre seus injetores de carga. Eles estarão no local ou na nuvem? Um bom critério de entrada é a disponibilidade das máquinas na rede certa e com as ferramentas certas instaladas. Se você estiver usando ferramentas comerciais, o provisionamento de licença deve ser um critério. Que tipo de capacidade seus scripts de teste de carga exigirão?
Suporte: Há pessoas disponíveis com experiência nos componentes principais?

O teste de carga é uma atividade da equipe. Quando um teste de carga envolve várias equipes de aplicativos, é importante solicitar a disponibilidade de pessoas-chave nessas equipes durante o teste. Freqüentemente, como testadores de carga, somos vistos como trabalhando de forma independente, mas a verdade não poderia estar mais longe disso. O teste de carga é um esporte de equipe. Precisamos de suporte de:

analistas de negócios que serão capazes de nos dizer como as coisas devem funcionar e quais são as prioridades atuais

    desenvolvedores que podemos consultar quando o código de baixo desempenho precisa ser otimizado
    testadores funcionais que podem nos mostrar como o aplicativo funciona
    Engenheiros DevOps que podem nos ajudar a provisionar e monitorar servidores

e muitos mais!

‍
Dados de teste: você tem dados fictícios para os usuários virtuais interagirem?

Depois de ter uma cópia o mais próxima possível do ambiente de produção, lembre-se de que ainda é uma cópia limpa, o que pode não ser realista. Se houver bancos de dados em produção, quantos dados eles contêm? O servidor de aplicativos pode responder de forma diferente quando seu banco de dados de teste está vazio em comparação com quando deve lidar com gigabytes de dados no banco de dados de produção.

Usar dados de produção para fins de teste pode ser perigoso, para não mencionar ilegal, em certas circunstâncias. Para evitar isso, você pode limpar dados confidenciais ou gerar seus próprios, injetando registros em um banco de dados ou escrevendo um script de automação para criar dados no front-end. Se você escrever um script, poderá reutilizar partes dele posteriormente para o teste de carga.
Modelagem de Carga de Trabalho

Um modelo de carga de trabalho é um esquema que descreve o perfil de carga para um determinado cenário de teste e envolve determinar quais (as transações principais), quanto (a distribuição de carga entre as transações) e quando (tempo de carga) testar.

A modelagem de carga de trabalho pode ser a parte mais difícil do processo de teste porque envolve descobrir como o script de teste de carga pode imitar melhor o que está realmente acontecendo na produção. Também pode ser o mais crítico.

Aqui está meu relato de trabalho em um projeto de corrida de cavalos, onde a modelagem de carga de trabalho era de particular importância: Modelagem de Carga de Trabalho - Preparação para Grandes Eventos como a Copa Melbourne .

Quando você está vendendo apostas para a Copa Melbourne, cada segundo assuntos.
Monitoramento de servidor

Executar um teste de carga sem monitorar a integridade do servidor é como voar às cegas. Você saberá quando pousar com segurança e quando bater, mas mesmo se bater, não saberá por quê - ou como pode evitar na próxima vez. O monitoramento da integridade do servidor é a caixa preta que informará o que deu errado.

Para o teste de carga, você deseja monitorar os servidores de aplicativos que está testando, bem como os geradores de carga que está usando para executar os próprios testes de carga. Isso mesmo; se você não estiver observando com atenção, as máquinas nas quais você executa os testes de carga podem ser os gargalos em si mesmas, causando falhas desnecessárias em seus testes de carga.

Joe Colantonio aborda os fundamentos da utilização de recursos em termos de quatro áreas principais de preocupação:

    CPU
    Memória
    Disco
    Rede

Aqui está outro guia que reuni sobre as métricas básicas, bem como algumas ferramentas que você pode usar para configurar seu monitoramento.

Independentemente de quais métricas você identifica como chave ou quais ferramentas você usa, você vai querer ter certeza de que estão todas configuradas para medir a integridade do servidor antes de executar seus testes de carga.
Duplas de teste

Parte do planejamento estratégico em torno do teste de carga é decidir quais componentes precisam ser testados em conjunto com seus requisitos declarados. Os aplicativos às vezes podem ser complexos o suficiente para que o teste de carga de ponta a ponta não seja viável devido ao número de equipes envolvidas ou ao custo de duplicar a infraestrutura do aplicativo.

Mantê-lo o mais simples possível resultará em menos dependências, portanto, vale a pena considerar a criação de dublês de teste para isolar componentes relevantes. As duplas de teste incluem stubs, simulações e serviços virtuais completos.

‍

Um dublê de teste é aquela parte que substitui um componente complicado que não está dentro do escopo. É uma versão “mais burra” que responde às solicitações o suficiente para permitir que você continue com o teste de carga sem realmente exigir esse componente.

As duplas de teste nos permitem abstrair outros componentes que não queremos testar para que possamos nos concentrar naquele que testamos. O objetivo de um teste duplo é remover as variáveis ​​e ruídos introduzidos por outras partes do aplicativo para que possamos nos concentrar em testar como um componente responde.

Se você deseja investir tempo na criação de um dublê de teste, pode reduzir drasticamente a quantidade de recursos necessária para configurar um ambiente e isolar componentes. Reduzir variáveis ​​em seu teste permite determinar mais rapidamente onde estão os gargalos de desempenho.
Cenários de teste

Um cenário de teste é a descrição de uma situação ou condição contida sob a qual o aplicativo será testado. Um cenário de teste geralmente é baseado em vários casos de teste e inclui um plano de como esses casos de teste serão executados.

Escolher seus cenários de teste significa decidir qual situação tem mais probabilidade de produzir os dados de que você precisa. Empregar vários tipos diferentes de cenários fornecerá a você uma compreensão maior dos recursos de seu aplicativo. Você deve se sentir à vontade para criar seus próprios cenários que são exclusivamente ajustados aos seus requisitos, mas aqui estão alguns cenários comuns para começar. Considere o número de usuários e durações mencionados como diretrizes e não regras.

[Cenarios de teste](https://www.youtube.com/watch?v=EGzoAadzWwM)

Conclusão

Criar um plano de teste pode parecer assustador, mas o processo de redação serve como um prompt para discussões entre sua equipe.

Aqui está uma dica profissional de Scott Moore : depois de criar um modelo com o qual esteja satisfeito, salve-o e reutilize-o em projetos futuros. Modifique-o ao longo do tempo com base no feedback para ver uma melhoria progressiva.

    Construir um conjunto de documentos reutilizáveis ​​e outras entregas (“modelos”) para usar na fase de planejamento inicial e relatório final irá acelerar o seu tempo de inicialização inicial. Recomendo trabalhar ou aprender com outras pessoas com experiência para construir alguns desses modelos.

‍ Em caso de dúvida, lembre-se de que o formato de um plano de teste não é tão importante quanto garantir que seja significativo e compreensível para sua equipe.