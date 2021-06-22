---
title: "Testes de Mutação: O Que São e Como Tornam A Cobertura de Código Relevante"
ref: mutation
lang: pt
layout: post
author: Carlos Schults
permalink: /pt/testes-de-mutacao/
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1595528879/mutation/mutation-testing-1038x437.jpg
description: Aprenda como testes de mutação podem ajudar você a tornar cobertura de código em uma métrica útil, garantindo a qualidade dos seus testes de unidade.
original: https://blog.ncrunch.net/post/mutation-testing-code-coverage.aspx
tags:
- testes-de-software
- testes-unitarios
- testes-automatizados
- cobertura-de-codigo
- testes-de-mutacao
- tdd
---

![]({{ page.img }})

<span>Photo by <a href="https://unsplash.com/@wocintechchat?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Christina @ wocintechchat.com</a> on <a href="https://unsplash.com/s/photos/software-testing?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>

*NOTA: Este post foi originalmente escrito para o blog da NCrunch. Você pode ler o [artigo original, em inglês, no site deles]({{ page.original }}).*

Sou fascinado com o conceito de testes de mutação desde que os conheci. Pensei finalmente ter encontrado a resposta para tantos problemas que tive ao escrever testes. Com os testes de mutação, agora eu tinha uma maneira de realmente confiar em meus testes. Finalmente, a cobertura de código tinha significado novamente.

Então, fiquei atônito ao perceber que muito poucos desenvolvedores compartilhavam meu interesse em testes de mutação. Na verdade, ouso dizer que a maioria dos desenvolvedores ainda nem sequer ouviu falar sobre isso. E isso é uma pena porque eles - e nós, como uma indústria - estamos perdendo tantos benefícios.

Portanto, este posto é minha humilde tentativa de remediar a situação. Vou começar por explicar os atuais dilemas que os desenvolvedores enfrentam em relação à confiabilidade dos testes que escrevem. Em seguida, vou prosseguir para lhe mostrar como os testes de mutação são a resposta a estes dilemas. Explicarei o que é, como pode tornar seus testes mais confiáveis, e como pode transformar a cobertura de código na valiosa métrica que deve ser.

## O problema: a confiabilidade dos testes

Ao aprender sobre [testes unitários][1] - ou testes automatizados em geral - a maioria das pessoas fará a mesma pergunta ou uma pergunta semelhante: Como sei que meus testes estão corretos? Essa é uma preocupação legítima. Se seus testes não são confiáveis, então talvez você esteja melhor sem nenhum teste.

Então, qual é a resposta? Como as pessoas lidam com o problema da confiabilidade dos testes sem depender de testes de mutação?

## Tornando os testes confiáveis sem testes de mutação

Há técnicas que os desenvolvedores empregam para melhorar a confiabilidade de seus testes, e cobriremos brevemente algumas delas nesta seção. Se você tem experiência com testes unitários, provavelmente está familiarizado com essas técnicas. Vamos lá.

### Manter os testes simples

A primeira técnica que cobriremos aqui para melhorar a confiabilidade de seus testes é apenas mantê-los simples. E por "simples" quero dizer com menos complexidade ciclomática. Quanto menor a [complexidade ciclomática][2] de um determinado código, mais provável é que ele realmente faz o que você pensa que faz. O código simples é mais fácil de entender, que é uma propriedade que você definitivamente quer que seus testes unitários tenham.

Mantenha o código de teste simples ao ponto de ser óbvio. Isso significa, por exemplo, evitar loops ou estruturas de decisão. Além disso, evite fazer qualquer coisa para computar o resultado esperado (mais sobre isso na próxima seção). Em vez disso, codifique-o de maneira fixa.

### Não Duplique o Código de Implementação

Digamos que você esteja praticando o [Coding Kata dos números romanos][3]. Resista à tentação de gerar automaticamente os valores esperados ("I" para 1, "II" para 2, e assim por diante). Em vez disso, codifique os valores de forma fixa. Se a repetição realmente o incomoda e sua ferramenta de teste o permite, use testes parametrizados.

Por que isso seria um problema? Simples: Quanto mais sofisticado for o código de teste, mais provável é que seja uma duplicação do código de produção. Se este for o caso, você pode ter o azar de se encontrar na situação em que seu código de produção está errado (não resolve o problema como deveria fazer), mas os testes passam. Esse é um dos piores cenários possíveis. É ainda pior do que não ter nenhum teste.

### Garanta que você veja o teste falhar

Garantir que cada teste falhe pelo menos uma vez antes de ser aprovado. Se você vê o teste falhar quando acha que deveria estar falhando e vice-versa, isso é um sinal de que você está se movendo na direção certa. Não garante nada, mas diminui a probabilidade de o teste estar passando devido a uma coincidência.

Como fazer isso? Assim que você chegar à fase verde, danifique o código de implementação de tal maneira que um ou mais testes devem falhar. Você poderia inverter os condicionantes, substituir strings ou literais numéricos por valores aleatórios, ou mesmo apagar um if. Se você conseguir sabotar o código de produção e se safar, isso não é um bom sinal. Seu conjunto de testes ou está errado ou incompleto. Em certo sentido, você está testando os testes.

Desenvolvedores que empregam [TDD (desenvolvimento orientado a testes)][4] já fazem isso, por definição. Uma vez que você escreve um teste falho e depois procede para que ele seja aprovado, você está vendo o teste falhar. É claro, o teste deve falhar da maneira esperada. Isso significa que se você estiver realizando uma asserção, o teste deve falhar devido a uma falha na asserção e não, digamos, porque o método sob teste lança uma exceção. Sim, isto é melhor do que nada, mas ainda assim pode não ser suficiente. Como um teste unitário representa um caso de uso único, é totalmente possível introduzir um defeito no código de produção de tal forma que este teste em particular ainda passe.

## Temos que fazer melhor: É Aí Que Entra o Teste de Mutação

Então, você acabou de aplicar a técnica descrita na última seção. Ótimo! Não é perfeita, porém. Aí vem um problema. Você não pode simplesmente inserir muitos defeitos e executar os testes, pois não seria capaz de identificar qual defeito foi responsável pelo fracasso dos testes. A maneira correta de fazer isso é inserir um único defeito deliberado, executar todos os testes, verificar seu resultado e _então_ reverter a mudança. Depois disso, você pode introduzir outro erro, executar todos os testes novamente, verificar o resultado, reverter a mudança...e repetir, muitas vezes. Nem precisa dizer que tal abordagem é extremamente lenta, entediante e propensa a erros.

É aí que entram os testes de mutação.

### O que é teste de mutação, afinal?

O teste de mutação é nada mais, nada menos, do que automatizar todo o processo de "sabotar o código de produção e executar testes para ver se eles falham" que você acabou de ver. Para usar o teste de mutação, você precisa de um framework, ou ferramenta, de teste de mutação. O framework irá alterar o código de produção, introduzindo defeitos que são chamados de "mutações". Para cada mutação introduzida, o framework executará novamente o conjunto de testes unitários. Se todos os testes forem aprovados, dizemos que a mutação sobreviveu. Isso é uma coisa ruim. Significa que ou seu conjunto de testes está faltando ou os testes existentes estão errados.

Se, por outro lado, um ou mais testes falharem, isso significa que a mutação foi morta, o que é uma coisa boa. A ferramenta repetirá esse processo até que se teste a parte relevante da base de código. Quando tudo estiver feito, você poderá verificar os resultados, que conterão o número de mutações introduzidas, assim como a proporção de mutantes sobreviventes vs. mutantes mortos.

### Os testes de mutação melhoram a cobertura do código

Um dos tópicos mais controversos no mundo dos testes de unidade é o argumento sobre a cobertura de código. Alguns desenvolvedores dizem que chegar à cobertura total é essencial; outros argumentarão que é uma métrica inútil. Quem está certo?

Primeiro de tudo, é preciso entender que esta questão não é preto no branco. Como é o caso de praticamente tudo em software, há alguma nuance. É claro que a cobertura de código não é inútil. Saber que sua base de código tem, digamos, 10% de cobertura de teste é definitivamente um dado útil. Tal cobertura é muito baixa: ver a barra verde não lhes oferecerá nenhuma confiança. Isso não quer dizer que ter 100% de cobertura é necessariamente uma coisa boa em si mesmo. Você poderia ter testes que não têm afirmações, por exemplo. Sim, este é um exemplo elaborado, mas algo assim poderia (e às vezes acontece) acontecer.

Uma ocorrência mais comum seria ter apenas testes que não exercitam suficientemente os caminhos no software. Em resumo: baixa cobertura de código é definitivamente uma coisa ruim, mas alta (ou total) cobertura de código não é _necessariamente_ uma coisa boa, uma vez que não diz nada sobre a qualidade dos testes na suíte.

Como os testes de mutação verificam a qualidade da suíte de testes, é a peça que falta no quebra-cabeça. Se sua base de código tem uma alta cobertura de código e os resultados dos testes de mutação mostram que a maioria ou todas as mutações introduzidas estão sendo mortas, então sorria! Você provavelmente tem uma ótima suíte de teste no lugar!

## Testes de Mutação Abrace Hoje

No post de hoje, falamos sobre o problema da confiabilidade dos testes, depois procedemos a uma revisão de algumas técnicas e diretrizes que você pode usar para superar esse desafio. Finalmente, vimos como o teste de mutação é a abordagem superior para resolver esse problema.

Eis o seguinte: As técnicas que abordamos são boas diretrizes a serem seguidas ao escrever testes unitários. Seus testes serão beneficiados por cumpri-los, quer você empregue ou não testes de mutação. Mas as diretrizes só podem levá-lo até agora. Elas dependem muito da força de vontade e disciplina humanas, e todos nós temos quantidades limitadas delas. A fim de levar a qualidade de seus testes ao próximo nível, você precisa adotar a automação.

São necessários apenas alguns minutos de pesquisa no Google para encontrar uma ferramenta de teste de mutação para a plataforma de sua preferência. Faça isso hoje e comece a aproveitar os benefícios que os testes de mutação podem oferecer a você e à sua equipe!

[1]: https://carlosschults.net/pt/testes-unitarios-iniciantes-parte1/
[2]: https://pt.wikipedia.org/wiki/Complexidade_ciclom%C3%A1tica
[3]: https://codingdojo.org/kata/RomanNumerals/
[4]: https://carlosschults.net/pt/testes-unitarios-csharp-intro-tdd/