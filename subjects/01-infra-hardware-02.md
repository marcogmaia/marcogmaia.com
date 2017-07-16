---
layout: single
permalink: /subjects/hardware/ch2
title: "Instruções: Linguagem do Computador."
modified: 2017-07-15T16:46:49
math: true
sidebar:
    title: Disciplinas
    nav: subjects
---

{% include toc %}

## Sobre os aspectos do MIPS.

1. Tamanho do dado a ser processador: **32 bits.**
2. Espaço de endereçamento de memória: **$$ 2^{32} $$**
3. Número de registradores: **32 registradores de 32 bits.**
4. Formato e tamanho das instruções:
    Existem **3 tipos de formato de instruções**:
    - **Tipo R**:

        |---
        | OPCODE | RS | RT | RD | SHAMT | FUNC
        |:-:|:-:|:-:|:-:|:-:|:-:
        |---
        | 6 | 5 | 5 | 5 | 5 | 6 
        |---

    - **Tipo I**


        |---
        | OPCODE | RS | RT | IMMEDIATE
        |:-:|:-:|:-:|:-:
        |---
        | 6 | 5 | 5 | 16
        |---

    - **Tipo J**


        |---
        | OPCODE | OFFSET
        |:-:|:-:
        |---
        | 6 | 26
        |---

## Técnicas de implementação de processadores
    
### Mono-Ciclo

- Vantagens:
    - Simplicidade.
- Desvantagens:
    - Maior custe de hardware.
    - Implementação não eficiente, devido à instruções pequenas que podem ocupar tempo da cpu mesmo tendo sido realizadas, pois o clock é baseado de acordo com a instrução que demora mais.

### Multi-Ciclo

- Vantagens:
    - Implementação eficiente se comparada ao mono-ciclo.
    - Menos custo de hardware

### Do formato de instruções.

Tanto na arquitetura projetada em sala de aula como na descrita no livre, todas as instruções aritméticas envolvem **3 operandos** (registradores) e possuem o mesmo formato. Vantagens e desvantagens disso:

- Vantagens:
    - Não se perde o valor dos registradores.
    - Operações mais rápidas, pois já se encontra em registradores.
    - Diminui o acesso à memória.
- Desvantagens:
    - Necessita de uma quantidade maior de registradores.
    - Aumenta o código, pois sempre tem que carregar os registradores e depois fazer a operação.

## Arquitetura LOAD/STORE.

O MIPS se caracteriza como uma arquitetura LOAD/STORE pois seus acessos à memória são feitos exclusivamente pelas instruções load e store.

- Vantagens:
    - Mais eficiência
    - Menos complexidade
- Desvantagens:
    - Aumento do código, pois sempre tem que carregar nos registradores antes de executar uma instrução.

## Da eficiência.

Considere três processadores P1, P2 e P3 executando o mesmo conjunto de instruções com as frequências de clock descritas na tabela:

|---
| Processador | Clock | CPI
|:-:|:-:|:-:
|---
| P1 | 2 GHz | 1.5
| P2 | 1.5 GHz | 1
| P3 | 3 GHz | 2.5
|---

- Qual o precessador tem o melhor desempenho?

    $$
    T_1 = I * \frac{CPI}{Clock} = I*\frac{1.5}{2*10^9} = I * 0.75 * 10^{-9} \\

    T_2 = I * \frac{CPI}{Clock} = I*\frac{1}{1.5*10^9} = I * 0.66 * 10^{-9} \\

    T_3 = I * \frac{CPI}{Clock} = I*\frac{2.5}{3*10^9} = I * 0.8 * 10^{-9}
    $$
    
    Portanto:
        $$ T_2 < T_1 < T_3 $$

- Se os processadores executam um programa em 10 segundos, qual o número de ciclos e de instruções para cada um?
    
    $$
    I = \frac{T * Clock}{CPI} \\
    Ciclos = T*Clock
    $$
    
    - P1:

    $$
    I = \frac{10*2*10^9}{1.5} \\
    Ciclos = 10*2*10^{9} = 2*10^{10}
    $$

    - P2:

    $$
    I = \frac{10*1.5*10^9}{1} \\
    Ciclos = 10*1.5*10^{9} = 1.5*10^{10}
    $$

    - P3:

    $$
    I = \frac{10*3*10^9}{2.5} \\
    Ciclos = 10*3*10^{9} = 3*10^{10}
    $$

- Se tentarmos reduzir o tempo em 30%, ocorreria um aumento de 20% no CPI. Qual seria o clock para essa redução?

$$
T = 10*0.7 = 7s \\
7 *x*Clock = I *1.2*CPI\\
10*Clock = I * CPI \\
x = \frac{1.2*CPI/7}{CPI/10} = 1.7143
$$    
o que nos daria um aumento de 71,43% no clock

