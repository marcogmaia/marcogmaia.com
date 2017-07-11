---
layout: post
title: "Infraestrutura de hardware - Rev. 3ª prova"
categories: disciplinas infraestrutura_hardware
author: "Marco Maia"
date: 2017-07-11 1:41:8
meta: "infraestrutura de hardware"
math: true
---

---
### Algoritmos para cálculos
#### Hit time:

- Transformar tudo em ciclos de clock
>multiplicar o tempo pela frequência

- primary stall
    
    PS = hit_time + miss_rate

---
## Questão 1
### Considere que um computador possua uma cache de 64KB, que use endereços de 32 bits e que cada bloco tenha 4 palavras. Descreva o layout do endereço, indicando quais e **quantos bits** são utilizados para representar a **tag**, o **índice** (ou conjunto) e o **offset**, para as seguintes configurações de associatividade:

#### a) Mapeamento direto 

$$ 64KiB = 2^{16} bytes $$ então o meu índice deve ter 6 bits, como o meu bloco contém 4 palavras, eu preciso de 2 bits de offset, e o restante é de tag (não levando em consideração bit de validade), menos 2 bits de endereço, e menos o portanto:

$$ index = 16 bits \\
offset = 2 bits \\
tag = 32 - 16 - 2 - 2 = 12 bits $$


#### b) Associativa por conjunto grau 8 (8 - way set).

Nessa memória, eu procuro em paralelo no meu index, $$ 8 = 2^3 $$, então, eu terei $$64/8 = 2^{16}/2^3 = 2^{13}$$ entradas, portanto o tamanho do meu **index** será 13 bits, o block **offset** 3 bits, 2 bits de offset de endereço, portando a minha **tag** será 32 - 13 - 3 - 2 = 14 bits.

---
## Questão 2
### O tamanho do bloco (linha) da cache influencia o desempenho da cache, podendo aumentar o desempenho ou reduzí-lo.

#### a) Dê duas razões porque blocos grandes podem degradar o desempenho. Justifique a resposta

- Blocos grandes demoram mais para ser carregado da memória.
- Dependendo do tamanho da cache pode gerar mais misses que hits, pois.

#### b) Descreva técnicas que podem ser utilizadas para reduzir os problemas gerados pelo uso de blocos grandes, considerando que o tamanho da cache é fixo.



























