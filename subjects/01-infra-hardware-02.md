---
layout: single
permalink: /subjects/hardware/ch2
title: "Instruções: Linguagem do Computador"
modified: 2017-07-15T16:46:49
math: true
sidebar:
    title: Disciplinas
    nav: subjects
---

{% include toc %}

## Sobre os apectos do mips.

1. Tamanho do dado a ser processador: **32 bits.**
2. Espaço de endereçamento de memória: **$$ 2^{32} $$**
3. Número de registradores: **32 registradores de 32 bits.**
4. Formato e tamanho das intruções:
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
    - Implementação não eficiente, devido à intruções pequenas que podem ocupar tempo da cpu mesmo tendo sido realizadas, pois o clock é baseado de acordo com a instrução que demora mais.

### Multi-Ciclo

- Vantagens:
    - Implementação eficiente se comparada ao mono-ciclo.
    - Menos custo de hardware

### Do formato de instruções

Tanto na arquitetura projetada em sala de aula como na descrita no livre, todas as instruções aritméticas envolvem **3 operandos** (registradores) e possuem o mesmo formato. Vanteges e desvantages disso:

- Vantagens:
    - Não se perde o valor dos registradores.
    - Operações mais rápidas, pois já se encontra em registradores.
    - Diminui o acesso à memória.
- Desvantagens:
    - Necessita de uma quantidade maior de registradores.
    - Aumenta o código, pois sempre tem que carregar os registradores e depois fazer a operação.

