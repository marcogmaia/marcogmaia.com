---
layout: post
title: "Revisão de infraestrutura de comunicação - Cap. 4"
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

- Virtual-circuits forwarding tables

    o pacote do VC carrega o número do VC (ao invés do endereço de destino), esse número será trocado a cada enlace, o novo número virá da forwarding table, e os roteadores mantém as informações sobre o estado das conexões.

- Datagram forwarding tables
