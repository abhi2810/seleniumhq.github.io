---
title: "Grid"
linkTitle: "Grid"
weight: 9
description: >
  Want to run tests in parallel across multiple machines? Then, Grid is for you.
aliases: 
        [
          "/documentation/pt-br/selenium_installation/installing_standalone_server/",
          "/documentation/pt-br/grid/",
          "/documentation/pt-br/grid/grid_4/",
          "/documentation/pt-br/grid/purposes_and_main_functionalities/"
        ]
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to German. Do you speak German? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

Selenium Grid permite a execução de scripts WebDriver em máquinas remotas (virtuais
ou reais) por meio de comandos de roteamento enviados pelo cliente para instâncias remotas do navegador.
Seu objetivo é fornecer uma maneira fácil de executar testes em paralelo em várias máquinas.

Selenium Grid nos permite executar testes em paralelo em várias máquinas
e gerenciar diferentes versões e configurações do navegador centralmente
(em vez de em cada teste individual).

A Selenium Grid não é uma bala de prata.
Ela resolve um subconjunto de problemas comuns de delegação e distribuição,
mas não irá, por exemplo, gerenciar sua infraestrutura,
e pode não atender às suas necessidades específicas.

## Objetivos e funcionalidades principais

* Ponto de entrada central para todos os testes
* Gerenciamento e controle dos nós / ambiente onde os navegadores rodam
* Escalonamento
* Executar testes em paralelo
* Teste de plataforma cruzada
* Balanceamento de carga


_Selenium Grid 4_ é uma implementação nova e não compartilha a base de código
da versão anterior.

Grid 4 tem uma abordagem para tirar proveito de uma série de novas tecnologias para facilitar o escalonamento, permitindo ainda a execução local.

Para obter todos os detalhes dos componentes do Grid 4, entenda como funciona e como definir
o seu próprio. Navegue pelas seguintes seções.