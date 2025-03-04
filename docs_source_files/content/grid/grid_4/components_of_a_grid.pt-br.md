---
title: "Componentes"
weight: 1
---

{{% notice info %}}
<i class="fas fa-language"></i> There are certain paragaraphs needs translation from 
English to Portuguese. Do you speak Portuguese? Help us to translate
it by sending us pull requests!
{{% /notice %}}


![Grid](/images/grid_4.png)

## Roteador

O roteador se encarrega de encaminhar a solicitação para o componente correto.

É o ponto de entrada da Grid, todas as solicitações externas serão recebidas por ele.
O roteador se comporta de maneira diferente dependendo da solicitação. Se for uma nova sessão,
o roteador irá encaminhá-la para o enfileirador de sessão, que irá adicioná-la a nova fila de sessão.
O Enfileirador de Sessão irá disparar um evento através do Event Bus.
O Distribuidor (onde a criação da nova sessão será tratada)
irá receber o evento e pesquisar o Enfileirador de Sessão para obter a nova solicitação de sessão.
Se a solicitação pertencer a uma sessão existente, o
roteador irá enviar a ID da sessão para o Mapa da Sessão, e o Mapa da Sessão irá
retornar o Nó onde a sessão está rodando. Depois disso, o roteador irá
encaminhar a solicitação ao Nó.

O Roteador visa equilibrar a carga na Rede, enviando as solicitações para o
componente que é capaz de lidar melhor com eles, sem sobrecarregar nenhum componente
que não é necessário no processo.

## Distribuidor

O Distribuidor está ciente de todos os nós e suas capacidades. Seu papel principal é receber um novo pedido de sessão
e encontrar um Nó adequado onde a sessão pode ser
criada. Depois que a sessão é criada, o Distribuidor armazena no Mapa da Sessão
a relação entre o ID da sessão e o nó onde a sessão está sendo executada.

## Nó

Um Nó pode estar presente várias vezes em uma Grid. Cada nó cuida de gerenciar
os slots para os navegadores disponíveis da máquina onde está sendo executado.

O Nó se registra no Distribuidor através do Event Bus, e sua configuração é enviada como parte da mensagem de registro.

Por padrão, o Nó registra automaticamente todos os drivers de navegador disponíveis no PATH da máquina onde ele roda. Ele também cria um slot por CPU disponível para navegadores baseados em Chromium e Firefox. Para Safari e Internet Explorer, apenas um slot é criado.
Por meio de uma configuração específica, ele pode executar sessões em contêineres Docker. Você pode ver
mais detalhes de configuração na próxima [seção]({{<ref "/grid/grid_4/setting_up_your_own_grid.pt-br.md">}}).

Um Nó apenas executa os comandos recebidos, não avalia, não faz julgamentos,
ou controlar qualquer coisa. As máquinas onde o Nó está rodando não precisam ter
o mesmo sistema operacional que os outros componentes. Por exemplo, um nó do Windows
pode ter a capacidade de oferecer o Internet Explorer como uma opção de navegador,
considerando que isso não seria possível no Linux ou Mac.

## Session Map

The Session Map is a data store that keeps the information of the session id and the Node 
where the session is running. It serves as a support for the Router in the process of 
forwarding a request to the Node. The Router will ask the Session Map for the Node 
associated to a session id.

## New Session Queue

New Session Queue holds all the new session requests in a FIFO order. 
It has configurable parameters for setting the request timeout and request retry interval.

The Router adds the new session request to the New Session Queue and waits for the response.
The New Session Queue regularly checks if any request in the queue has timed out, 
if so the request is rejected and removed immediately.

The Distributor regularly checks if a slot is available. If so, the Distributor requests the
New Session Queue for the first matching request. The Distributor then attempts to create
a new session.

Once the requested capabilities match the capabilities of any of the free Node slots, the Distributor attempts to get the
available slot. If all the slots are busy, the Distributor will ask the queue to add the request to the front of the queue. 
If request times out while retrying or adding to the front of the queue it is rejected.

After a session is created successfully, the Distributor sends the session information to the New Session Queue.
The New Session Queue sends the response back to the client. 

## Enfileirador de Sessão, Fila de Sessão

O Enfileirador de Sessão é o único
componente que pode se comunicar com a nova fila de sessão. Ele lida com todas as operações de fila (como
*add*) para manipular a fila. Possui parâmetros configuráveis ​​para definir
o tempo limite da solicitação e o intervalo de repetição da solicitação.

A Fila de Sessão recebe a nova solicitação de sessão do Roteador e a adiciona à fila.
O enfileirador espera até receber a resposta para a solicitação.
Se a solicitação expirar, ela será rejeitada imediatamente e não adicionada à fila.

Ao adicionar com sucesso a solicitação à fila, o Event Bus aciona um evento.
O Distribuidor seleciona este evento e pesquisa a fila. Agora ele tenta criar uma sessão.

Se os recursos solicitados não existirem em nenhum dos nós registrados, a solicitação será rejeitada
imediatamente e o cliente recebe uma resposta.

Se os recursos solicitados corresponderem aos recursos de qualquer um dos slots de Nó, o Distribuidor tenta obter o
slot disponível. Se todos os slots estiverem ocupados, o Distribuidor pedirá ao enfileirador para adicionar o pedido
para o início da fila. O Distribuidor recebe a solicitação novamente após o intervalo de repetição da solicitação.
Ele tentará novas tentativas até que a solicitação seja bem-sucedida ou tenha expirado.
Se a solicitação atingir o tempo limite ao tentar novamente ou adicionar à frente da fila, ela será rejeitada.

Depois de obter um slot disponível e a criação de sessão, o Distribuidor passa a nova resposta de sessão
para a nova fila de espera de sessão por meio do Event Bus. Enfileirador de Sessão responderá ao cliente quando ele
recebe o evento.

## Event Bus

The Event Bus serves as a communication path between the Nodes, Distributor, New Session Queuer, and Session Map. 
The Grid does most of its internal communication through messages, avoiding expensive HTTP calls. 
When starting the Grid in its fully distributed mode, the Event Bus is the first component that should be started. 

## Funções na Grid

Na Grade 3, os componentes eram Hub e Nó, e era possível executá-los juntos iniciando a
Grid em modo autônomo. O mesmo conceito está disponível na Grid 4, é possível executar um hub
agrupando alguns dos componentes descritos acima, e também é possível executar todos os componentes
juntos em um modo autônomo. 

### Hub

Hub é a união dos seguintes componentes:

* Roteador
* Distribuidor
* Mapa da Sessão
* Enfileirador de Sessão
* Event Bus

Habilita a configuração clássica de hub e nó(s).

### Standalone

Como mencionado antes, Standalone é a união de todos os componentes e, aos olhos do usuário, eles são
executado como um. Isso inclui todos os componentes que fazem parte do hub, mais um nó. Totalmente
Uma Grid totalmente funcional está disponível após iniciá-la no modo Standalone.
