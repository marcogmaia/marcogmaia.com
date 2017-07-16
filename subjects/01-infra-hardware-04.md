---
layout: single
permalink: /subjects/hardware/ch4
title: "Processador: Pipeline e Superscalar."
modified: 2017-07-16T19:11:9
math: true
sidebar:
    title: Disciplinas
    nav: subjects
---

{% include toc %}

## Pipeline.

Considere um sistema de computação que possuia uma CPU com palavras de 32 bits, o repertório é o do processador **MIPS**.

Inicialmente a CPU foi implementada com a técnica **multi-ciclo** e que a quantidade de ciclos de cada instrução é dada na tabela abaixo.

|---
| Instrução | N° de ciclos
|---
|Aritméticas e deslocamente | 4
|Load word - lw | 5
|Store word - sw | 4
|Jump | 3
|Beq | 4
|Lui | 3
|Jal e Jr | 4
|---

Qual o **tempo de execução** e o **CPI** para uma implementação **multiciclo** executar o programa

~~~
lw $t1, 4($t4)
lw $t3, 8($t4)
lw $t2, 12($t4)
lw $t0, 0($t4)
beq $t0, $t1, endX
sub $t0, $t0, $t1
sub $t3, $t3, $t2
addi $t0, $t0, 1
addi $t2, $t2, 1
sub $t2, $t2, $1
sub $t1, $t1, $3
j endY
endX:
    sub $t3, $t3, $t2
    add $t0, $t0, $t1
    addi $t3, $t3, -1
    addi $t2, $t2, -1
    add $t2, $t2, $t1
    add $t1, $t1, $t3
endY:
    sw $t0, 0($t4)
    sw $t1, 4($t4)
    sw $t2, 12($t4)
~~~

Em multiciclo temos:
    - 4 load
    - 3 store
    - 1 beq
    - 6 aritméticas