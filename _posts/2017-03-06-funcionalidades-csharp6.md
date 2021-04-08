---
title: Já está na hora de começar a usar essas features do C# 6!
ref: csharp6
lang: pt
layout: post
author: Carlos Schults
permalink: /pt/funcionalidades-csharp-6/
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1487896790/csharp6features_y5czrf.jpg
tags:
- csharp
- iniciantes
---
  
![](https://res.cloudinary.com/dz5ppacuo/image/upload/v1487896790/csharp6features_y5czrf.jpg)

A sétima versão do C# está chegando, e vai provavelmente trazer várias funcionalidades novas e úteis para nossas  caixas de ferramentas. Mas deixa eu perguntar uma coisa: você já está usando as funcionalidades da versão anterior?
 <!--more-->

Alguns dias atrás eu estava pensando sobre qual seria o tema do próximo post. Nada mais natural que escrever sobre o C# 7, já que [seu lançamento, junto com o Visual Studio 2017, é amanhã.](https://blogs.msdn.microsoft.com/visualstudio/2017/02/09/visual-studio-2017-launch-event-and-20th-anniversary/)

Mas então eu percebi que, mesmo já fazendo cerca de dois anos desde o lançamento do C# 6, alguns desenvolvedores ainda não se sentem confortáveis o suficiente com as funcionalidades da versão, de maneira a não incorporá-las em seu código.

Assim, eu decidi voltar um pouco e escrever sobre as funcionalidades do C# 6 no lugar disso. Não todas, mas aquelas que podem tornar seu código mais limpo e expressivo, e que são simples o suficiente para você já sair usando!
 
## Interpolação de String
 
Suponha que nós temos uma classe chamada `Person`, com duas propriedades somente-leitura, `Name` e `Age`. Algo assim:
 
<script src="https://gist.github.com/carlosschults/84db03cd2a530530b72c4b9eeeb738d4.js"></script>
 
Então nós adicionamos um método chamado `Introduce`, para que nossas pessoas sejam capazes de se apresentar. Para uma pessoa de 22 anos chamada Maria, o método deve retornar "Hi! My name is Maria and I'm 22 years old."
 
Tem algumas maneiras diferentes de se fazer isso na versão 5 do C#, como você pode ver na seguinte listagem:

<script src="https://gist.github.com/carlosschults/9e30324951420356397c5cc8f50ea51b.js"></script>

Cada uma delas tem suas vantagens e desvantagens, claro, mas o C# 6 disponibiliza um novo jeito:
 
<script src="https://gist.github.com/carlosschults/17f501bd6d0ce6f5938edf17ef8e8704.js"></script>

Apenas coloque um cifrão no início da string, coloque suas variáveis dentro de chaves, e é isso!

Interpolação de strings não funciona para todas as ocasiões. Se você precisa de uma formatação especial nos valores, você ainda teria de usar `string.Format()`, por exemplo.

Mas no dia-a-dia, eu uso interpolação na maioria das vezes que preciso fazer concatenação de strings. Eu acho essa forma bem mais interessante e mais clara do que as outras opções.
 
## Initializers para propriedades automáticas
 
Continuando com o exemplo anterior. Vamos supor que nós precisamos de um construtor sem parâmetros em nossa classe. Junto com isso, vamos precisar disponibilizar valores padrão para `Name` e `Age`.

Do contrário, o método `Introduce()` retornaria "Hi! My name is  and I'm 0 years old." E não iríamos querer isso, né?
 
No C# 5, nós teríamos que inicializar as propriedades dentro do construtor:
 
<script src="https://gist.github.com/carlosschults/d95cade5d8d5f245a1d6bb49ef2feb1f.js"></script>
 Já a sexta versão da linguagem nos permite definir valores padrão para as propriedades no mesmo momento em que as declaramos:

<script src="https://gist.github.com/carlosschults/e7d56c032e723f7c5110a9e3bfa1c744.js"></script>
 
## Operador condicional nulo
 
Considere o código a seguir:
 
<script src="https://gist.github.com/carlosschults/7fb5caff2e73f4130f4db982825adbe6.js"></script>
 
Nada demais, não é? Mas tem um problema esperando para acontecer aqui. Se `customer` é `null`, esse código vai disparar uma `NullReferenceException`.
 
É nesse momento que o "Operador condicional nulo" vem a calhar: 
 
<script src="https://gist.github.com/carlosschults/65bc4372a0e4fc3e8f38c0ee57905beb.js"></script>
 
O que o código acima faz? Simples: se `customer` não é `nulo`, a propriedade `Address` é acessada normalmente, e seu valor é atribuído à nossa variável local. No entanto, se `customer` *é* `null`, a expressão toda é avaliada para nulo, e é isso que a variável recebe.

Outra coisa legal a respeito desse operador é que você pode usá-lo em conjunto com o [Operador Null Coalesce](https://msdn.microsoft.com/en-us/library/ms173224.aspx) para disponibilizar, de maneira fácil, um valor default diferente de `null`.

<script src="https://gist.github.com/carlosschults/e17d34ba939fb7c472e164010db56377.js"></script>
 
## Métodos e propriedades "Expression-bodied"

Essa é bem fácil. Trata-se de uma maneira mais curta de escrever métodos, utilizando a sintaxe das expressões lambda.

Por exemplo, os dois métodos a seguir fazem a mesma coisa:

<script src="https://gist.github.com/carlosschults/eeae77f3876f9b692ca667281b5401d0.js"></script>

Essa funcionalidade não é restrita a métodos. Ela também pode ser usada com propriedades (de apenas leitura) e indexadores.
 
## Conclusão

Parece claro que o objetivo da Microsoft  com a sexta versão do C# não era adicionar funcionalidades radicalmente novas à linguagem.

Ao invés disso, a intenção era permitir aos desenvolvedores escrever código de uma maneira mais clara e concisa. E em minha opinião, o objetivo foi alcançado.

Você pode pensar que algumas das funcionalidades não fazem tanta diferença, na prática. Eu discordo. C# é frequentemente acusado de ser muito verboso. Existem situações nas quais você precisa escrever uma quantidade razoável de código para fazer algo que em Ruby ou Python poderia ser feito em uma linha.

E isso é normal. Um pouco (a maioria) da já mencionada verbosidade vem do fato de C# ser uma linguagem estaticamente tipada, e eu digo: **sou feliz por isso**. Eu não consigo contar a quantidade de vezes que o compilador me salvou, pegando meus erros idiotas.

Se um pouco de verbosidade é o preço que tenho que pagar por isso, que seja.
 
Tudo isto dito, os detratores têm uma certa razão. É possível ser verboso *excessivamente*. Então, qualquer funcionalidade que me permite eliminar um pouco dessa verbosidade extra e escrever código mais conciso é muito bem vinda.
 
## Veja mais
 
- [https://geekswithblogs.net/WinAZ/archive/2015/06/30/whatrsquos-new-in-c-6.0-auto-property-initializers.aspx](https://geekswithblogs.net/WinAZ/archive/2015/06/30/whatrsquos-new-in-c-6.0-auto-property-initializers.aspx)
- [https://msdn.microsoft.com/en-us/magazine/dn802602.aspx](https://msdn.microsoft.com/en-us/magazine/dn802602.aspx)
- [https://blog.caelum.com.br/novidades-do-c-6-0/](https://blog.caelum.com.br/novidades-do-c-6-0/)
