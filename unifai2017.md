---
layout: page
title: Informações sobre o minicurso "Introdução aos testes unitários automatizados com NUnit e C#"
permalink: /unifai2017/
ref: unifai2017
lang: pt
---

Esta página vai servir para agregar todo o conteúdo relevante relativo ao minicurso ministrado por mim na XXI Semana de Informática da UNIFAI, em Adamantina - SP, nos dias 17 e 18 de agosto de 2017.

## Downloads

- [Slides](https://speakerdeck.com/carlosschults/introducao-aos-testes-unitarios-automatizados-com-nunit-e-c-number)
- Projetos de exemplo no Github:
	- [Primeiro Teste](https://github.com/carlosschults/PrimeiroTeste)
	- [Testando a Classe Funcionário](https://github.com/carlosschults/testando-a-classe-funcionario)
	- [TDD com String Calculator Kata](https://github.com/carlosschults/tdd-com-string-calculator-kata)

## Série *Testes Unitários Para Iniciantes*

"Testes Unitários Para Iniciantes" é uma série de posts em progresso no meu blog, no qual tento apresentar, de maneira bem didática, o assunto de teste unitários
para pessoas sem experiência com este tema.

O minicurso foi parcialmente baseado nesta série, que conta com dois artigos publicados até o momento.

- Em Português:
	- [Testes Unitários Para Iniciantes - Parte 1](http://carlosschults.net/pt/testes-unitarios-iniciantes-parte1)
	- [Testes Unitários Para Iniciantes - Parte 2](http://carlosschults.net/pt/testes-unitarios-iniciantes-parte-2)
- Em Inglês:
	- [Unit Testing For Beginners - Part 1](http://carlosschults.net/en/unit-testing-for-beginners-part1/)
	- [Unit Testing For Beginners - Part 2](http://carlosschults.net/en/unit-testing-for-beginners-part2/)


## Instalação do NUnit

Para criar os testes unitários, você precisa de um **Framework de Testes**. No meu dia-a-dia utilizo o [NUnit](http://nunit.org/), desta forma nada mais natural que escolher este framework para o minicurso e também minha série de artigos sobre testes.

Além do Nunit em si, precisamos de mais um componente chamado **NUnit Test Adapter**, que faz com que o Visual Studio consiga enxergar a e executar os testes do NUnit.

Tanto o NUnit quanto o NUnit Test Adapter são disponibilizados como pacotes do Nuget, e podem ser instalados com os seguintes comandos no console do Nuget:

> Install-Package NUnit

e 

> Install-Package NUnit3TestAdapter

Caso precise de mais ajuda, meu segundo artigo sobre teste unitários possui [uma seção detalhada ensinando passo-a-passo a instalação destes componentes](http://carlosschults.net/pt/testes-unitarios-iniciantes-parte-2#instalando-o-nunit).

