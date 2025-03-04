---
title: "Componentes"
linkTitle: "Componentes"
weight: 1
aliases: ["/documentation/pt-br/grid/grid_4/components_of_a_grid/"]
---

{{% pageinfo color="warning" %}}
<p class="lead">
   <i class="fas fa-language display-4"></i> 
   Page being translated from 
   English to Portuguese. Do you speak Portuguese? Help us to translate
   it by sending us pull requests!
</p>
{{% /pageinfo %}}

{{< figure src="/images/documentation/grid/components.png" class="img-responsive text-center" alt="Grid">}}

## Roteador

The Router takes care of forwarding the request to the correct component.

It is the entry point of the Grid, all external requests will be received by it.
The Router behaves differently depending on the request.
If it is a new session request, the Router will add it to the New Session Queue. 
The Distributor regularly checks if there is a free slot. 
If so, the first matching request is removed from the New Session Queue.
If the request belongs to an existing session, the
Router will send the session id to the Session Map, and the Session Map will 
return the Node where the session is running. After this, the Router will
forward the request to the Node.

The Router aims to balance the load in the Grid by sending the requests to the
component that is able to handle them better, without overloading any component
that is not needed in the process.

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
mais detalhes de configuração na próxima [seção]({{< ref "setting_up_your_own_grid.md" >}}).

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
