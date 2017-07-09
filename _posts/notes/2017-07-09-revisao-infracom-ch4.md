---
layout: post
title: "Infraestrutura de comunicação - Cap. 4"
categories: notes
author: "Marco Maia"
date:   2017-07-09 5:59:7
meta: "infraestrutura de comunicação"
---

## R3
### Diferença entre forwarind e routing.

Forwarding refere-se a direcionar o pacote de uma porta de entrada do roteador
à porta de saída apropriada.

Routing é o processo de determinar o roteamento fim-a-fim (da fonte até o destino).

## R4
### Roteadores em datagram networks e virtual-circuits networks usam forwarding tables? Se sim, descreva forwarding tables de ambas as classes de redes.

Sim, ambas usam forwarding tables.

- Virtual-Circuits forwarding tables

    O pacote do VC carrega o número do VC (ao invés do endereço de destino), esse número será trocado a cada enlace,
    o novo número virá da forwarding table, e os roteadores mantém as informações sobre o estado das conexões.

    Sempre que um novo VC é estabelecido, uma nova entrada na tabela de repasse é criada, similarmente,
    é removida quando a conexão é terminada.

- Datagram forwarding tables

    Os pacotes são repassados tipicamente usando endereços de destino.

    Cada roteador tem uma tabela de repasse que mapeia o endereço de destino a enlaces.


## R12
### Roteadores tem endereços IP? Se sim, quantos?

Sim, têm um endereço IP para cada interface.


## R13
### Qual é o 32-bit binário equivalente do endereço IP 223.1.3.27?

11011111.00000001.00000011.00011011


## R17
### Suponha que A envia para B um segmento TCP encapsulado em um datagrama IP. Quando B receber o datagrama, como a network layer em B saberá que deverá passar o segmento ao TCP ao invés do UDP ou a qualquer outra coisa?

O campo de 8-bits de protocolo no datagrama IP contém informação sobre qual protocolo de camada de transporte
o host de destino deverá passar o segmento.


## P1
### Consideremos os pros e os cons de VC e datagram networks.
#### a) Suponha que um roteador seja sujeito a condições que causem sua falha com frequência. Nesse caso, qual seria a melhor arquitetura? Por quê?

Com a rede VC, cada falha de roteador envolvera a rota inteira daquela conexão. No mínimo será preciso que o roteador "upstream" dessa conexão estabeleça um novo caminho até o destino, com todos os requisitos envolvendo a criação de um novo caminho.
Além disso, todos os roteadores downstream da conexão inicial deverão terminar a conexão, com todo o trabalho envolvido para isso.

#### b) Suponha que uma fonte e um destino precisem que uma determina capacidade sempre esteja a disposição em todos os roteadores em um caminho entre eles, para o uso exclusivo do tráfego. Isso seria melhor feito em VC ou datagram? Por quê?

Para que um roteador mantenha uma capacidade fixa no caminho entre a fonte e o destido, ele precisaria conhecer as caracteŕisticas do tráfego de todas as sessões passando por esse enlace.
Isso é apenas possível em uma rede connection-oriented. Portanto uma VC seria necessária.

#### c) Suponha que os enlaces e os roteadores nunca falhem na rede e que os caminhos se mantenham constantes. Nesse caso, qual das duas arquiteturas tem mais controle sobre o overhead do tráfego? Por quê?

Nesse caso, uma rede de datagramas tem mais controle do overhead. Isso se dá por conta dos vários packet headers necessários para rotear os datagramas envolvidos na rede.
Em uma arquiterura VC, uma vez que o circuito é estabelecido, eles não mudarão, portanto o overhead é negligenciado ao longo prazo.

