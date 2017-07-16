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
    Existem 3 tipos de formato de instruções:
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


