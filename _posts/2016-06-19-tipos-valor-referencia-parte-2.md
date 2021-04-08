---
title: Tipos de valor e referência em C#, Parte 2 - Por que DateTime não pode ser nulo?
ref: types2
lang: pt
layout: post
permalink: /pt/tipos-valor-referencia-em-csharp-parte-2/
author: Carlos Schults
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1466341001/csharp-min_buiizq.png
tags:
- csharp
- iniciantes
- orientacao-a-objetos
- tipagem
---

![](https://res.cloudinary.com/dz5ppacuo/image/upload/v1466341001/csharp-min_buiizq.png)

"Por que uma variável DateTime não pode receber `null`?" Esta é uma pergunta que vive aparecendo no *StackOverflow* e site similares. Às vezes escrita de modo um pouco diferente, às vezes com um tipo diferente, mas no fundo é a mesma dúvida. O que é natural, se você considerar que provavelmente milhares de pessoas entram na área a cada ano.
<!--more-->

A resposta curta é: porque DateTime/int/float/etc é um **tipo de valor**, e tipos de valor não podem nunca receber `null`. Apenas tipos de referência podem.

Legal, mas...por quê?

Em algum momento os projetistas do C# tiveram que tomar essa decisão. Eles deliberadamente decidiram que tipos de valor não poderiam receber `null`. Será que tem alguma coisa que naturalmente impede isso? Talvez tenha algo a ver com a pilha e a heap?

Eu acho que antes de tentarmos responder essas questões, seria interessar voltar um passo e pensar um pouco sobre outra questão.

## O que exatamente é null?

Você provavelmente pensa em `null` como uma maneira de representar uma informação que está faltando. Algo desconhecido, ausente ou irrelevante. Talvez um dado que não está onde deveria *ainda*, mas talvez esteja no futuro.

Lembra do meu [post anterior sobre tipos de valor e referência](https://carlosschults.net/pt/tipos-valor-referencia-em-csharp/)? Nele nós vimos que uma variável de um tipo de referência **contém uma referência que aponta para uma instância daquele tipo específico**. Mas quando a variável recebe *null*, seu conteúdo passa a ser o quê? Nada?

Não exatamente. Ainda que `null` essencialmente signifique nada, esse "nada" precisa ser representado de alguma forma na memória do computador.

No C#, a palavra reservada `null` representa uma **referência nula**, que é uma referência que não aponta para nenhum objeto. Na prática, essa referência é representada como um número (de 32 ou 64 bits, dependendo do sistema operacional) com todos os bits zerados.

É claro, tudo isso são detalhes de implementação. Isso poderia ter sido implementado de maneiras diferentes, ou seja, não é tão relevante assim pra gente agora. O que você realmente precisa entender é que você **precisa de algo para representar nada**. É necessário algum tipo de valor especial que significa "esse valor está faltando" ou "esse valor é desconhecido".

Quando você entende isso, fica mais fácil enxergar qual é o problema com tipos de valor.

## Como você representaria null para um tipo de valor?

Para entender qual é a dificuldade em fazer um tipo de valor ser nulo, você precisa considerar que tipos de valor geralmente têm um intervalo de valores possíveis que eles são capazes de representar.

É mais fácil de entender isso com um exemplo. Então, considere o tipo de valor [byte](https://msdn.microsoft.com/pt-br/library/system.byte(v=vs.110).aspx).

Esse tipo representa um número inteiro sem sinal de 8 bits. Como 2 elevado a 8 é 256, é possível representar 256 valores. Como é um tipo "sem sinal", ele só pode representar valores maiores ou igual a zero. Portanto, o range de valores possíveis para esse tipo é **de 0 a 255**.

    00000000 => 0
    00000001 => 1
    00000010 => 2
        .        .
        .        .
        .        .
    11111111 => 255

Agora vem a parte complicada. Se os projetistas do C# quisessem que o tipo byte fosse nulável, eles teriam que escolher um dos valores desse intervalo para elegê-lo como o valor nulo. Imagine que eles tivessem escolhido o zero. Nesse caso, **nós nunca poderíamos usar o zero como um valor válido novamente!**

Esse é todo o problema: para que um tipo de valor seja nulável, seria necessário sacrificar um dos possíveis valores do intervalo para representar o valor nulo.

Jon Skeet, autor do livro C# In Depth, é capaz de explicar bem melhor do que eu:

 > You've got to be able to store the values 0-255 in that variable; otherwise it's useless for reading arbitrary binary data. With the 256 normal values
and one null value, you'd have to cope with a total of 257 values, and there's no way of squeezing that many values into a single byte. 
>
The designers could've decided that every value type would have an extra flag bit somewhere determining whether a value was null or contained real data, but the memory usage implications 
are horrible, not to mention the fact that you'd have to check the flag every time you wanted the use the value.

Em tradução livre:

> Você precisa ser capaz de armazenar os valores de 0 a 255 naquela variável; do contrário esse tipo seria inútil para ler dados binários arbitrários. Com os 256 valores normais e um valor nulo, você teria que lidar com um total de 257 valores, e não tem jeito de espremer tudo isso em um único byte.

> Os projetistas poderiam ter decidido que todo tipo de valor teria um bit extra em algum lugar determinando se um valor é nulo ou contém dados reais, mas as implicações de uso de memória são horríveis, sem falar que você teria que checar esse bit toda vez que quisesse usar o valor.

Então, não há nada **em princípio** que impede que tipos de valor recebem nulo. É que seria tão complicado que os projetistas da linguagem decidiram que os benefícios de fazer isso não superam os custos.

## Mas eu realmente preciso de um tipo de valor nulável. E agora?

Agora você entende as complicações envolvidas em representar `null` para um tipo de valor, e porque os projetistas do C# decidiram contra permitir isso. Mas, e se você realmente precisa fazer isso? Um cenário comum é quando você busca dados de um banco de dados relacional. O que é possível ser feito?

Felizmente há uma solução fácil. Ainda que tipos de valor "normais" não são nuláveis, a versão 2 do C# introduziu a estrutura `Nullable<T>`, que permite atribuir `null` a praticamente qualquer coisa. 

Falarei sobre isso no próximo artigo da série. Como bônus, você vai aprender um pouco sobre outra feature interessante chamada **generics**.

Até lá!
