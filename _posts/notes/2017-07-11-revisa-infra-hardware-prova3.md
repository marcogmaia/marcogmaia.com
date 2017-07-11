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
## Questão 1
### Considere que um computador possua uma cache de 64KB, que use endereços de 32 bits e que cada bloco tenha 4 palavras. Descreva o layout do endereço, indicando quais e **quantos bits** são utilizados para representar a **tag**, o **índice** (ou conjunto) e o **offset**, para as seguintes configurações de associatividade:

#### a) Mapeamento direto 

$$ 64KiB = 2^{16} bytes $$ então o meu índice deve ter 6 bits, como o meu bloco contém 4 palavras, eu preciso de 2 bits de offset, e o restante é de tag (não levando em consideração bit de validade), portanto:

$$ index = 16 bits \\
offset = 2 bits \\
tag = 32 - 16 - 2 = 14 bits $$


#### b) Associativa por conjunto grau 8 (8 - way set).

Nessa memória, eu procuro em paralelo no meu index, $$ 8 = 2^3 $$, então, eu terei $$64/8 = 2^{16}/2^3 = 2^13$$ entradas 
