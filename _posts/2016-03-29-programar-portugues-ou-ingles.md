---
title: Programar em português ou inglês? That's the question!
lang: pt
layout: post
author: Carlos Schults
permalink: /pt/programar-portugues-ou-ingles/
ref: idioma
img: ![](http://res.cloudinary.com/dz5ppacuo/image/upload/v1458429920/portugues-ou-ingles-1038x437_izhi3i.png)
tags: 
- boas práticas
- inglês
---

![](http://res.cloudinary.com/dz5ppacuo/image/upload/v1458429920/portugues-ou-ingles-1038x437_izhi3i.png)

No contexto de boas práticas de desenvolvimento, um ponto que gera controvérsia é a escolha do idioma no qual codificar. Uma rápida busca no Google por "programar em português ou inglês" retorna 535 mil resultados, o que mostra que o tema realmente causa bastante discussão. 
<!--more-->
Recentemente conversei com um colega de trabalho e também com meu chefe a respeito desse assunto. Esse post é consequência dessas conversas e das pesquisas que fiz depois.

Parece ser uma visão bastante comum na nossa área que programar em inglês é a melhor opção. Fabio Akita, grande referência na comunidade Ruby On Rails do Brasil, [inclui codificar em português - ou melhor dizendo, qualquer idioma que não o inglês - na sua lista de piores práticas de desenvolvimento](http://www.akitaonrails.com/2013/03/24/quais-sao-algumas-das-piores-praticas-para-aplicacoes-ruby-on-rails--2):

> Escreva nomes em inglês dentro do seu código. Não me importo se você é brasileiro, italiano, francês ou o que   for. Nomes de classes, de variáveis, de métodos, tudo deve ser em inglês. Estamos num mundo globalizado, não é pensar muito longe que amanhã um americano vai mexer no seu código todo em português. Além do problema de consistência: a sintaxe da linguagem, todas as bibliotecas padrão, é tudo em inglês. É uma enorme dissonância cognitiva ter nomes em português no meio. É como você estar lendo uma revista em português com diversos parágrafos em inglês no meio. Não faz nenhum sentido.

Carlos Brando, outro nome conhecido no mundo Rails, [deu opinião semelhante em um post de 2009](http://nomedojogo.com/2009/02/13/rails-way-3-nomes-de-metodos-e-variaveis-devem-ser-obvios/):

> Embora não exista uma regra escrita para isto, também sou contra nomear variáveis, métodos ou classe em português. Acho que como todo o código já está em inglês, graças as palavras chaves do Ruby, devemos manter absolutamente tudo em inglês também. Isto não é tão difícil assim, já que você pode fazer uso de tradutores e dicionários (online) para encontrar a melhor descrição para eles.

Um exemplo de como esse tema é inflamável: [há cerca de dois anos foi lançada a versão em português do Stack Overflow](http://blog.stackoverflow.com/2014/01/ola-mundo-announcing-stack-overflow-in-portuguese/), famoso site de perguntas e respostas pra programadores. Pare aqui e vá lá dar uma olhada no post. Viu a quantidade de comentários criticando a iniciativa? A controvérsia foi tanta que duas semanas depois a equipe do Stack Overflow publicou um novo post, dessa vez em inglês, justificando a decisão.

Eu acredito que a discussão é necessária e saudável e que existem bons argumentos nos dois lados. Assim, vou  examinar opiniões a favor do uso de cada idioma, e ao final do post, expressar minha conclusão.

## Argumentos a favor do inglês

Um dos argumentos mais comuns usados a favor do inglês é que seria estranho ou feio misturar dois idiomas na codificação. Como as palavras reservadas das linguagens de programação/frameworks/SGBD's já são em inglês, utilizar a língua portuguesa para nomear variáveis e outras coisas acaba gerando híbridos como *getNome*, *ProdutosController*, *clientes.ForEach*, *CodigoNaoEncontradoException* e assim por diante. No trecho citado logo ali acima, Fabio Akita afirma que a mistura dos idiomas causa uma dissonância cognitiva, seria como ler uma página escrita em um idioma e de repente se deparar com parágrafos escrito em outro.

Outro argumento comum, também utilizado pelo Akita no trecho citado, é a possibilidade de um programador não-brasileiro vir a trabalhar no projeto. Imagine um projeto que conte com desenvolvedores da França, Alemanha, Brasil, Estados Unidos. Se cada um resolve programar no seu idioma, a comunicação se tornará impossível, a menos que todos os membros da equipe sejam proficientes nos idiomas de todos os outros membros, o que seria bastante improvável.

Um ponto bem parecido com o anterior é que a utilização do português prejudicaria uma eventual venda do produto para uma empresa de outro país, o que é de fato inegável.

O fato de que o inglês é a língua franca da tecnologia também figura constantemente entre os argumentos dos defensores do uso dessa língua na codificação. Segundo eles, qualquer desenvolvedor que se preze **precisa** ter um domínio avançado da língua inglesa. Sendo assim, o uso da inglês na verdade facilitaria o desenvolvimento, e não o contrário.

Outro ponto interessante a favor do inglês é que os identificadores nesse idioma tendem a ser menores, o que incentiva a um código mais limpo e conciso. Por exemplo, compare *setName* com *atribuirNome*. 

Uma consequência do ponto anterior é que o uso de um único idioma ajuda a consolidar um vocabulário compartilhado entre todos os programadores. *Get* e *Set*, por exemplo, são palavras-chaves familiares para a maioria dos desenvolvedores, por serem extremamente comuns em API's e bibliotecas diversas. Digamos que um programador recém-chegado à sua empresa recebe a tarefa de dar manutenção em uma biblioteca que vocês desenvolveram para trabalhar com XML. Ele provavelmente teria mais facilidade em encontrar um método chamado *GetChildren()* do que se fosse chamado ObterFilhos(). 

Outra vantagem da utilização do inglês seria...que ela melhora o seu conhecimento de inglês. Já que programadores precisam dominar esse idioma de qualquer forma, toda e qualquer oportunidade de praticá-lo é válida.

## Argumentos a favor do português

Um argumento a favor do uso do português é a baixa proficiência em inglês apresentada pelos desenvolvedores brasileiros em geral, e como isso pode prejudicar a comunicação não apenas entre os desenvolvedores, mais também entre os desenvolvedores e as pessoas de negócio:

> Da mesma forma, uma regra de negócio traduzida para o inglês pode ser mal traduzida por quem não domina o idioma. Falsos cognatos existem e podem ser utilizados nessa tradução cotidiana. Imagine que, ao invés de criar classes chamadas Funcionario e Empregador você crie classes chamadas Employee e Employer. Isso seria tão confuso para um desenvolvedor que não domina o inglês, quanto para um desenvolvedor que domina o inglês. Na hora de programar, os termos podem misturar-se.
[Gustavo Gondim](http://www.ventron.com.br/programar-em-portugues-ou-ingles/)

> Eu já vi tantas atrocidades na transliteração de português para inglês usando Google Translator… Na falta da compreensão, pega-se a primeira palavra que aparece. Ou cria-se expressões com termos em inglês usando a sintaxe do português. Confunde-se a forma de usar substantivos, verbos e adjetivos. A língua resultante pode ser inglês de índio, mas não é inglês. O ponto é que em uma equipe que não fala inglês nativamente, usar os termos de negócio em inglês pode complicar até o entendimento entre os programadores.[...]
[Fernando Correia](https://blogdofernandocorreia.wordpress.com/2011/09/21/que-lingua-usar-para-nomes-do-dominio-de-negocio/)

Resumindo: uma equipe que tem domínio superficial do inglês necessariamente produz inglês de baixa qualidade, por não estar ciente das "pegadinhas" que o idioma pode apresentar (por exemplo: falsos cognatos). Mas ainda tem mais: é de conhecimento geral que programadores passam mais tempo lendo código do que escrevendo. E qualquer programador com alguma experiência vai concordar que ler código é bem mais difícil do que escrever. Ao forçar uma equipe sem desenvoltura na língua inglesa a trabalhar com uma base de código escrita nessa língua, estaríamos aumentando a barreira necessária para a compreensão do código, dificultando a manutenção e aumentando a chance de criação de bugs.

O [Tiago Albineli Motta, do blog "Programando Sem Cafeína"](http://programandosemcafeina.blogspot.com.br/2009/03/nomes-de-metodos-e-variaveis-devem-ser.html), traz um argumento bem interessante: de que o uso de idiomas diferentes prejudica a comunicação entre cliente e a equipe de desenvolvimento, principalmente quando o domínio do negócio é bastante específico. Para justificar, ele cita o exemplo de quando trabalhava em uma empresa que estava desenvolvimento um sistema para um laboratório geológico. Como os funcionários do laboratório usavam termos em português e a equipe de desenvolvimento em inglês, havia ruídos na comunicação.

Destaco um trecho interessante abaixo (destaque meu):

> Eis então a pergunta: Será que um código que mistura termos em inglês e português causa mais problemas que os ruídos na comunicação com o cliente? Pode-se alegar que o código nem será mostrado ao usuário, **mas na hora em que o desenvolvedor precisa se comunicar com o cliente, na mente dele ele não está trabalhando com amostras, ele está trabalhando com samples.**

Ainda no tema do domínio, poderíamos imaginar o desenvolvimento de uma aplicação que se integra com a famigerada Nota Fiscal Eletrônica. Como o xml da nota já vem com os campos todos em português, utilizar nomes de variáveis em inglês poderia adicionar um esforço cognitivo desnecessário.

## E a minha opinião?

Acredito ter sido capaz de demonstrar que existem boas opiniões nos dois lados desse debate. Mas e aí? Vocês devem estar se perguntando qual a minha opinião, não é? Ok, não vou ficar em cima do muro. Mas antes, acho necessário fazer algumas considerações importantes.

### O inglês é a língua franca da tecnologia

O inglês é a língua franca da tecnologia. E da ciência, das finanças, e de muitas outras coisas. Todo mundo tem o direito de gostar ou não do idioma que quiser, mas é simplesmente contra produtivo querer brigar com um fato da vida que não vai mudar tão cedo. Eu particularmente acho que deveríamos ser gratos que o "idioma obrigatório" é o inglês, e não o russo, árabe, ou mandarim, por exemplo.

Então, independente do seu posicionamento no debate, aprender inglês é um investimento que vale muito a pena. O que nos leva ao próximo ponto.

### E não é tão difícil de se aprender quanto parece

Estou convencido de que uma enorme inteligência não é requisito para aprender inglês. Muito menos pagar cursos caros em escolas renomadas, ou fazer intercâmbio. Então por que há tantas pessoas que querem aprender inglês e [tão poucas conseguem](http://exame.abril.com.br/brasil/noticias/fluencia-do-brasileiro-no-ingles-so-piora-veja-ranking)?

Em minha opinião, o primeiro motivo é que a maioria dessas pessoas não *querem* realmente. E o segundo...é simplesmente que elas estudam errado, colocando o foco, tempo e energia no lugar onde não deviam.

Em breve vou fazer um post totalmente dedicado ao tema do aprendizado de inglês, onde vou expandir e explicar melhor o parágrafo anterior.

### Seu projeto tem características únicas que não devem ser ignoradas

Seu projeto atual provavelmente tem características únicas, que nem eu, nem o Fabio Akita, nem o Tiago Motta, ou qualquer outra pessoa de fora sabe. Não conhecemos o nível de fluência no inglês da sua equipe, nem o domínio da sua aplicação. 

Também desconhecemos o escopo do seu projeto, se todos os colaboradores são brasileiros ou se há pessoas de outros países,os prospectos de venda da empresa para uma companhia multinacional, etc. 

Ou seja: há uma série de fatores que podem e devem ser levadas em conta no momento de se adotar essa ou aquela prática, essa ou aquela metodologia. Nessas horas, você tem que exercitar o senso crítico: mantenha a mente aberta na hora de ler, pesquisar e conhecer opiniões contrárias, mas use seu bom senso e experiência para filtrar o e decidir o que encaixa com a cultura da sua empresa, equipe e projeto.

### Tentar prever o futuro é anti-ágil.

Eu costumo chamar isso de síndrome do "vai que um dia", pois a conversa geralmente começa assim:

"Vai que um dia o cliente precisa de [insira aqui funcionalidade que o cliente não precisa agora e provavelmente nunca vai precisar]? Vamos fazer!"

E aí já viu: tabelas inúteis são criadas no banco de dados, classes e mais classes e formulários e telas e muito mais lixo entupindo seu projeto. 

Tentar prever toda e qualquer alteração no projeto é anti-ágil. Equipes ágeis dão pequenos passos, implementando as histórias priorizadas pelo cliente e nada mais. Quando os requisitos mudarem (e vão mudar) nós mudamos junto com eles.

Entendeu onde eu quero chegar? "Vai que um dia uma empresa internacional resolve comprar nosso sistema? Vamos fazer todo o código e as tabelas em inglês!"

### Em resumo: bom-senso é a chave

Com base em tudo isso aí que você leu, minha opinião atualmente está assim: tentar utilizar o inglês sempre, **exceto quando há ótimas razões para não utilizá-lo.**

Projetos open-source? Tudo em inglês, *exceto em casos onde há benefícios claros em usar o português*.

Em projetos particulares: se a equipe é fraca no inglês **E/OU** o domínio é muito específico e tem termos e jargões de difícil tradução **E/OU** há riscos claros de prejuízo na comunicação com o cliente, o português provavelmente é a melhor escolha.

Se a situação é o contrário do descrito acima, inglês sem dúvida.

Se desde o começo do projeto existe a certeza que a aplicação será disponibilizada para vários países, vocês vão precisar trabalhar em internacionalização, de tudo: especificações, ajuda, interface gráfica. Nesse caso, também não há motivo para não codificar em inglês.

## E você, o que acha?

Concorda, discorda, prefere não opinar? Deixe um comentário aí em baixo e vamos continuando a conversa!

## Referências 
- [http://pt.stackoverflow.com/questions/301/devo-escrever-meu-programa-em-ingl%C3%AAs-ou-portugu%C3%AAs](http://pt.stackoverflow.com/questions/301/devo-escrever-meu-programa-em-ingl%C3%AAs-ou-portugu%C3%AAs
)
- [http://programandosemcafeina.blogspot.com.br/2009/03/nomes-de-metodos-e-variaveis-devem-ser.html](http://programandosemcafeina.blogspot.com.br/2009/03/nomes-de-metodos-e-variaveis-devem-ser.html)
- [http://nsigustavo.blogspot.com.br/2009/09/que-idioma-devemos-utilizar-em-nosso.html](http://nsigustavo.blogspot.com.br/2009/09/que-idioma-devemos-utilizar-em-nosso.html)
- [https://blogdofernandocorreia.wordpress.com/2011/09/21/que-lingua-usar-para-nomes-do-dominio-de-negocio/](https://blogdofernandocorreia.wordpress.com/2011/09/21/que-lingua-usar-para-nomes-do-dominio-de-negocio/)
- [http://www.dev.mayogax.com/2014/02/a-polemica-questao-do-stack-overflow-em-portugues/](http://www.dev.mayogax.com/2014/02/a-polemica-questao-do-stack-overflow-em-portugues/)
- [http://nomedojogo.com/2009/02/13/rails-way-3-nomes-de-metodos-e-variaveis-devem-ser-obvios/](http://nomedojogo.com/2009/02/13/rails-way-3-nomes-de-metodos-e-variaveis-devem-ser-obvios/)
- [http://www.ventron.com.br/programar-em-portugues-ou-ingles/](http://www.ventron.com.br/programar-em-portugues-ou-ingles/)
