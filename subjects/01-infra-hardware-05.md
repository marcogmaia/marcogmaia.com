---
layout: single
permalink: /subjects/hardware/ch5
title: "5. Cache, hierarquia de memória."
modified: 2017-07-16T22:56:29
math: true
sidebar:
    title: Disciplinas
    nav: subjects
---

{% include base_path %}

{% include toc %}

## De caches.

Uma cache está sendo projetada para um computador com $$2^{32}$$ bytes de memória, a qual terá 2k slots e usará blocos de 16 bytes.

O número de bytes que a cache terá:
- Mapeamento direto:
    1. $$2^{32}$$ bytes de memória $$\rightarrow$$ endereço de 32 bits.
    2. 2k slots $$\rightarrow 2^{11} $$ slots $$\rightarrow$$ index de 11 bits.
    3. Blocos de 16 bytes $$\rightarrow$$ 4 bits para offse (16 bytes são 4 palavras, 2 bits para offset de bloco e 2 bits para offset de byte).
    4. Tag = endereço - (index + offset) = 32 - (11 + 4) = 17 bits.

    Endereço de memória:
    
    |---
    |Tag|index|offset bloco | offset byte
    |---
    | 17 bits | 11 bits | 2 bits | 2 bits
    |---

## Memória virtual.

Um sistema de memória virtual implementado com as seguintes características:
- Espaço de endereçamento 4GB
- memória principal de 32MB com páginas de 4KB

Portanto:
- Endereçamento = 4GB = 2^32
- Tamanho do endereço virtual = 32 bits
- Tamanho da página = 4KB = 2^12
- Offset de página = 12 bits
- Tamanho da memória principal = 32 MB = 2^5 * 2^20 = 2^25
- Número de página físico = 25 - 12 = 13 bits

**Layout do endereço virtual:**

O número da página virtual é o endereçamento menos o offset de página.

|---
|Número da página virtual | Offset da página 
|---
| 20 bits | 12 bits
|---

Layout da tabela de tradução:

|---
|bit de presença = 1 bit | dirty bit = 1 bit | Número de página físico = 13 bits|
|---
|... |... |...
|... |... |...
|---

A tabela possui 2^20 entradas, sendo assim, a tabela de tradução tem um tamanho de $$ 2^{20} * 15 bits = 15*2^{17} bytes $$

**Tradução do endereço virtual em endereço físico:**
A cada endereço virtual está associada uma posição na tabela com o endereço físico correspondente. É analisado se o endereço está na memória através do bit de presença, se a página foi modificada o drity bit vai pra 1. Quando a página precisa ser substituída na memória física é realizada a atualização dos dados na memória secundária e só depois a substituição.

---

### Análise comparativa dos diferentes modos de tradução de endereços.

- **Paginação:** consistem em dividir a memória em blocos chamados páginas, onde toda transferência é feita em unidade de página entre disco e memória.
    - **Prós:** Simples de alocar, fácil de compartilhar
    - **Cons:** Exige grande tabela, pode ocorrer fragmentação interna.

- **Segmentação:** Divide os dados por conteúdos, onde cada conteúdo de um processo é chamado de segmento e este é alocado na memória de acordo com o tamanho necessário.
    - **Prós:** Eficiente, fácil de compartilhar, proteção
    - **Cons:** Complexo, pode ocorrer a fragmentação externa, precisa guardar os limites do segmento.

<!-- Um sistema possui uma TLB two-way set associativa com 512 entradas. Como se dá a tradução de endereços via TLB.

Quando a memória virtual é acessada, a MMU busca na TLB pelo número da página virtual que será acessada, caso encontre (hit) será usada na entrada da tabela de páginas armazenada na TLB, casa não encontre (miss) o tratador de interrupção buscará uma maneira de contornar a falta do endereço na TLB.

Resumindo, a TLB opera similarmente à cache, reduzindo acessos à memória principal.

1. (Bits virtual - offset) $$\rightarrow 2^{32}, 2^{12}  $$ $$\rightarrow 32 - 12 = 20 $$  -->