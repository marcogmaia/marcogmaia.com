---
layout: post
title: "Infraestrutura de comunicação - Cap. 4"
categories: disciplinas infraestrutura_comunicação
author: "Marco Maia"
date: 2017-07-09 5:59:7
meta: "infraestrutura de comunicação"
math: true
---

---
## R3
### Diferença entre forwarind e routing.

Forwarding refere-se a direcionar o pacote de uma porta de entrada do roteador
à porta de saída apropriada.

Routing é o processo de determinar o roteamento fim-a-fim (da fonte até o destino).

---
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

---
## R12
### Roteadores tem endereços IP? Se sim, quantos?

Sim, têm um endereço IP para cada interface.

---
## R13
### Qual é o 32-bit binário equivalente do endereço IP 223.1.3.27?

11011111.00000001.00000011.00011011

---
## R17
### Suponha que A envia para B um segmento TCP encapsulado em um datagrama IP. Quando B receber o datagrama, como a network layer em B saberá que deverá passar o segmento ao TCP ao invés do UDP ou a qualquer outra coisa?

O campo de 8-bits de protocolo no datagrama IP contém informação sobre qual protocolo de camada de transporte
o host de destino deverá passar o segmento.

---
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

---
## P3
### O bare-bone da tabela de repasse numa rede VC tem 4 campos, o que cada um desses campos quer dizer? E o bare-bone de uma rede tem datagramas tem dois campos, o que eles significam?

Numa rede VC, as colunas na tabela de repasse são: interface de entrada, número VC de entrada, interface de saída e número VC de saída.

Na tabela de repasse da rede de datagrama, as colunas são: endereço de destino e interface de saída.

---
## P10
### Considere uma rede de datagramas usando um endereço de host de 32 bits. Suponha que um roteador tenha 4 enlaces, numerados de 0 a 3, e que os pacotes tem que ser encaminhados ao enlace

tem uma tabela chata de codar/fazer aqui no html/markdown, to com preguiça...

---
## P13
### Considere um roteador que interconecta 3 subnets: Subnet1..3. Suponha que todas as interfaces precisam ter o prefixo 223.1.17/24. Também suponha que a Subnet1 precise ter pelo menos 60 interfaces, Subnet2 pelo menos 90 interfaces, e Subnet3 pelo menos 12 interfaces. Dê 3 endereços de rede (na forma a.b.c.d/x) que satisfaça essas condições.


1. 223.1.17.0/26
2. 223.1.17.128/25
3. 223.1.17.192/28

---
## P17
### Considere a topologia abaixo:

{: .center}
![fig. 4.17]({{site.url}}/imgs/fig-4.17.png)

### Denote as 3 subnets com os host (começando sentido horário em 12:00) como Networks A, B e C. Denote as subnets sem hosts como Networks D, E e F.

#### a) Atribua endereços de rede a cada uma das seis subnets, com as seguintes restrições: todos os endereços tem que ser alocados a partir de 214.97.254/23; Subnet A, B e C tem que suportar 250, 120 e 120 interfaces respectivamente (pelo menos). E claro, as Subnets D, E e F tem que suportar duas interfaces cada, a atribuição tem que ter a forma a.b.c.d/x ou a.b.c.d/x - e.f.g.h/y.

De 214.97.254/23, possíveis atribuições são:

- Subnet A: 214.97.255/24 (256 addresses)
- Subnet B: 214.97.254.0/25 - 214.97.254.0/29 (128-8 = 120 addresses)
- Subnet C: 214.97.254.128/25 (128 addresses)
- Subnet D: 214.97.254.0/31 (2 addresses)
- Subnet E: 214.97.254.2/31 (2 addresses)
- Subnet F: 214.97.254.4/30 (4 addresses)

#### b) Utilizando a resposta da letra a), dê uma forwarding table (usando longest prefix matching) para cada roteador.

|---
| Router 1
|Longest Prefix Match | Outgoing Interface
|:-|:-:|-
|11010110 01100001 11111111 | Subnet A
|11010110 01100001 11111110 0000000 | Subnet D
|11010110 01100001 11111110 000001 | Subnet F
|---

----

|---
| Router 2
|Longest Prefix Match | Outgoing Interface
|:-|:-:|-
|11010110 01100001 11111111 0000000 | Subnet D
|11010110 01100001 11111110 0 | Subnet B
|11010110 01100001 11111110 0000001 | Subnet E
|---

----

|---
| Router 3
|Longest Prefix Match | Outgoing Interface
|:-|:-:|-
|11010110 01100001 11111111 000001 | Subnet F
|11010110 01100001 11111110 0000001 | Subnet E
|11010110 01100001 11111110 1 | Subnet C
|---

---
## P19
### Considere enviar um datagrama de 2400 bytes em um enlace que tem um MTU de 700 bytes. Suponha que o datagrama original é marcado com identificação número 422. Quantos fragmentos serão gerados? Quais são os valores nos vários campos do(s) datagrama(s) IP gerados relacionado à fragmentação?

O tamanho máximo do campo de dados em cada fragmento é de 680 (porque 20 bytes são do IP header). Portanto o número de gramentos necessários é $$ = \lceil{\frac{2400 - 20}{680}}\rceil = 4 $$.

Cada framento terá identificação 422 (incluindo o IP header). 
O último datagrama terá tamanho de 360 bytes (incluindo o header).

Os offsets dos 4 fragmentos serão 0, 85, 170, 255. Cada um dos 3 primeiros terão flag de fragmentação = 1; o último terá flag = 0.

