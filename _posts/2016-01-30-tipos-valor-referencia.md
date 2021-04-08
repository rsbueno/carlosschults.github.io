---
title: Tipos de valor e referência em C#
ref: types
lang: pt
layout: post
permalink: /pt/tipos-valor-referencia-em-csharp/
author: Carlos Schults
img: https://res.cloudinary.com/dz5ppacuo/image/upload/v1466341001/csharp-min_buiizq.png
tags:
- csharp
- iniciantes
- orientacao-a-objetos
- tipagem
---

![](https://res.cloudinary.com/dz5ppacuo/image/upload/v1466341001/csharp-min_buiizq.png)

Este é o meu primeiro post pra valer aqui no meu blog, e eu decidi escrever sobre tipos de valor e tipos de referência em C#. Isso é um assunto relativamente básico, no sentido de que é algo que você já deveria entender caso você programe em C# profissionalmente. Mas ao mesmo tempo, é algo que pode ser um pouco contra-intuitivo caso você não seja um desenvolvedor experiente.
<!--more-->

Eu vou tentar deixar o post o mais simples e curto possível, então não vou falar hoje sobre imutabilidade de string, *boxing*, *unboxing*, e outras coisas com nomes chiques.
Vou escrever sobre essas coisas no futuro, mas por hoje vamos focar no básico.

Então, dê uma olhada no código a seguir:

{% highlight c# %}
int x = 10;
int y = x;
y++;
Console.WriteLine($"O valor de x é {x}"); //Imprime "O valor de x é 10"
Console.WriteLine($"O valor de y é {y}"); //Imprime "O valor de y é 11"
{% endhighlight %}

Nenhuma surpresa até aqui, esse é exatamente o comportamento que você esperaria. Agora, imagine que nós temos uma classe assim:

{% highlight c# %}
public class Pessoa
{
    public string Nome { get; set; }
    public string Profissao {get; set; }

    public Pessoa(string nome, string profissao)
    {
        Nome = nome;
        Profissao = profissao;
    }

    public void DizerOi()
    {
        Console.WriteLine($"Oi! Meu nome é {Nome} e eu sou {Profissao}");
    }
}
{% endhighlight %}

Agora, faça o seguinte:

{% highlight c# %}
var pessoa = new Pessoa("Maria", "programadora");    
pessoa.DizerOi(); // imprime "Oi! Meu nome é Maria e eu sou programadora"
var pessoa2 = pessoa;
pessoa2.Nome = "João";
pessoa.Profissao = "músico";    
pessoa.DizerOi(); // imprime "Oi! Meu nome é João e eu sou músico"  
pessoa.DizerOi(); // imprime "Oi! Meu nome é João e eu sou músico"  
{% endhighlight %}

Esse é o momento no qual iniciantes costumam ficar confusos. "Isso não faz sentido", eles dizem. "Eu mudei o valor de uma das variáveis, e a outra também mudou." Bem, essa é a maneira errada de enxergar o que aconteceu. Na verdade, você <strong>não</strong> mudou o valor da varíavel, e esse é o ponto.

Lembra do primeiro exemplo? Vamos dar uma olhada nele novamente, dessa vez passo-a-passo:

<img alt="A figura mostra um trecho de código C# no qual a variável é criada e lhe é atribuído o valor 10" src="https://res.cloudinary.com/dz5ppacuo/image/upload/v1454161625/fig1_czxki5.png" />

Nós declaramos a primeira variável e atribuímos o valor 10 a ela. Agora, em algum lugar dentro da memória do computador, existe uma "caixa" com o nome de x, e dentro dessa caixa tem o valor 10.

<img alt="A figura mostra um trecho de código C# no qual a variável y é criada e recebe o valor da variável x" src="https://res.cloudinary.com/dz5ppacuo/image/upload/v1454165139/fig2_de8azi.png" />

Nós declaramos a segunda variável e atribuímos a ela o valor da primeira variável. Note que o valor é copiado de x para y. Agora nós temos duas caixas, uma chamada x e a outra y, e ambas guardam o valor 10.

<img alt="A figura mostra um trecho de código em C# no qual o valor da variável y é incrementado em 1" src="https://res.cloudinary.com/dz5ppacuo/image/upload/v1454165134/fig3_sdjbze.png" />

Finalmente, nós incrementamos o valor da variável y em 1. Note que o valor de x permanece inalterado. Claro, por que eles realmente não tem nada a ver um com outro! Por outro lado, algo bem diferente acontece quando você está lidando com tipos de referência. Para entender isso, vamos repassar o segundo exemplo, também passo-a-passo:

<img alt="A figura mostra um trecho de código C# no qual a variável pessoa é criada e recebe uma nova instância da classe Pessoa" src="https://res.cloudinary.com/dz5ppacuo/image/upload/v1454165141/fig4_xivrng.png" />

Primeiramente, nós criamos uma variável chamada pessoa e atribuímos a ela uma nova instância da classe Pessoa. Agora, em algum lugar na memória do computador vive uma caixa chamada "pessoa". Note, porém que nossa variável pessoa guarda <strong>uma referência que aponta para a instância da classe Pessoa, ao invés de guardar a própria instância!</strong>

<img alt="A figura mostra a criação da variável pessoa2, que logo em seguida recebe o valor da variável pessoa" src="https://res.cloudinary.com/dz5ppacuo/image/upload/v1454165138/fig5_i21mgj.png" />

No segundo passo, criamos a variável "pessoa2" e atribuímos a ela o valor da variável "pessoa." Assim como no exemplo anterior, o valor de uma variável é copiado para a outra. Nesse caso, **o valor que é copiado é a referência que aponta para a instância de pessoa**. Então agora nós temos duas variáveis cujos valores são referências que apontam para a mesma instância da classe Pessoa.

Agora, é claro que quando você mudar os dados do objeto (por exemplo, mudar o nome e/ou profissão da pessoa) parece que as duas variáveis foram alteradas. Na verdade, os valores das variáveis continuam exatamente o mesmo: o que foi realmente alterado é o objeto para o qual elas apontam.

Então, podemos resumir da seguinte forma: tipos de valor armazenam dados. Quando você atribuir o valor de uma variável a outra, o que é copiado são os próprios dados (como um número inteiro, por exemplo). Isso é parecido com quando você copia um arquivo de uma pasta em seu computador e cola em outro lugar. Você fez uma cópia, mas de agora em diante eles são arquivos independentes e não têm nada a ver um com o outro.

Tipos de referência armazenam uma referência, que apontam para os dados, que vivem em algum outro lugar na memória do computador. Quando você atribui o valor de uma variável de referência para outra, o que é copiado é a referência. Pode ser útil pensar nas referências como atalhos para arquivos. Se você tem um ou mais atalhos que apontam para um arquivo em particular no seu HD, quando você fizer alterações no arquivo, tais alterações serão vis&iacute;veis quando você acessar o arquivo pelo atalho. Pois eles não passam disso, atalhos.

## Quais tipos são tipos de valor? ##

De acordo com o MSDN, os tipos de valor são:

- Todos os tipos númericos
- Boolean, Char, e Date
- Todas as estruturas
- Enumerações

## Quais tipos são tipos de referência? ##

Novamente, de acordo com o MSDN:

- String
- Todos os arrays
- Classes
- Delegates

## Espera um pouco! String é um tipo de referência?! ##

Talvez você tenha se surpreendido em ver String listada como um tipo de referência. Afinal de contas, ela parece se comportar como um tipo de valor. Bom, a razão para isso é que a string é um tipo **imutável**. Como eu disse antes, não vou falar sobre isso hoje, mas em breve teremos um post inteiro sobre System.String.

Bom, por hoje é só. Espero que tenham gostado do post, e eu adoraria ter o feedback de vocês. Eu me expressei claramente? Eu disse algo um pouco impreciso - ou mesmo totalmente errado? Deixe um comentário aqui embaixo ou [me chame no twitter](https://twitter.com/carlosschults).

## Referências (em inglês): ##

- [https://jonskeet.uk/csharp/references.html](https://jonskeet.uk/csharp/references.html)
- [https://msdn.microsoft.com/en-us/library/t63sy5hs.aspx](https://msdn.microsoft.com/en-us/library/t63sy5hs.aspx)
