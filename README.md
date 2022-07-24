<h1 align="center">Guide Assembly x86 👽</h1>

<p align="center">
 <a href="#Introdução">Introdução</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
 <a href="#Porque Assembly">Porque Assembly</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#O que é assembly">O que é assembly</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#O que é assembler">O que é assembler</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Noção de arquitetura">Noção de arquitetura</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Endianness">Endianness</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Instruções">Instruções</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Modo de processamento">Modo de processamento</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
</p>

<a id="Introdução"></a>

# Introdução 🥱

Esse e um guia para quem quer aprender Assembly x86 e x86-64.

<a id="Porque Assembly"></a>

#### Por que aprender Assembly ?

1. Engenharia Reversa (de software)
2. Exploração de binários
3. Otimização de código
4. Tarefas de "baixo nível"
5. C & Assembly

<a id="O que é assembly"></a>

# O que é Assembly ? 🧐

De forma resumida Assembly é uma notação em formato de texto das instruções do código de máquina de uma determinada arquitetura. A "arquitetura" ao qual me refiro aqui é a ISA (Instruction Set Architecture) onde ela cria um modelo abstrato de um computador e tem diversas instruções que são computadas pelo processador, essas instruções são o que é conhecido como código de máquina.
Falando de um ponto de vista humano, entender instruções em código de máquina é uma tarefa árdua. Por isso os manuais da ISA costumam simplificar o entendimento da instrução se referindo a ela com uma notação em texto, onde essa notação é conhecida como mnemônico e tem o fim de facilitar o entendimento e a memorização da instrução do processador.
E é justamente dessa notação em texto dos manuais que surgiu o que a gente conhece hoje como "linguagem Assembly". Onde na verdade não existe uma linguagem Assembly (ou ASM para abreviar) mas sim cada ISA tem uma linguagem ASM diferente.
Os programadores antigamente escreviam o código usando a notação em texto (Assembly) e depois, a partir dela, convertiam para código de máquina manualmente. Mas felizmente hoje em dia existem softwares que fazem essa conversão de maneira automática e eles são chamados de assemblers.

<a id="O que é assembler"></a>

# O que é Assembler ? 😄

O assembler é um compilador que converte código em Assembly para o código de máquina.

<a id="Noção de arquitetura"></a>

# Noção de arquitetura 🐵

Antes de ver a linguagem e importante que sabamos sobre a arquitetura do assembly. É claro que não dá para explicar todas as características da arquitetura x86 aqui, só para te dar uma noção o manual para desenvolvedores da Intel tem mais de 5 mil páginas. Mas por enquanto vamos ter apenas uma noção sobre a arquitetura x86 para entender melhor à respeito da mesma.

# O que é arquitetura x86 ? 🏴‍☠️

Essa arquitetura nasceu no 8086, que foi um microprocessador da Intel que fez grande sucesso.
Daí em diante a Intel lançou outros processadores baseados na arquitetura do 8086 ganhando nomes como: 80186, 80286, 80386 etc. Daí surgiu a nomenclatura 80x86 onde o x representaria um número qualquer, e depois a nomenclatura foi abreviada para apenas x86.
A arquitetura evoluiu com o tempo e foi ganhando adições de tecnologias, porém sempre mantendo compatibilidade com os processadores anteriores. O processador que você tem aí pode rodar código programado para o 8086 sem problema algum.
Mais para frente a AMD criou a arquitetura x86-64, que é um superconjunto da arquitetura x86 da Intel e adiciona o modo de 64 bit. Nos dias atuais a Intel e a AMD fazem um trabalho em conjunto para a evolução da arquitetura, por isso os processadores das duas fabricantes são compatíveis.
Ou seja, x86 é um nome genérico para se referir a uma família de arquiteturas de processadores. Por motivos de simplicidade eu vou me referir as arquiteturas apenas como x86, mas na prática estamos abordando três arquiteturas neste README.

<p align="center">
  <img src="./.github/arquitetura.jpeg">
</p>

<a id="Endianness"></a>

# Endianness 🤖

A arquitetura x86 é little-endian, o que significa que a ordem dos bytes de valores numéricos segue do menos significativo ao mais significativo. Por exemplo o seguinte valor numérico em hexadecimal 0x1a2b3c4d ficaria disposto na memória RAM na seguinte ordem:

```
  1 4d 3c 2b 1a
```

<a id="Instruções"></a>

# Instruções 🤖

A arquitetura x86 é uma arquitetura <a href="https://pt.wikipedia.org/wiki/CISC">CISC</a> que, resumindo, é uma arquitetura com um conjunto complexo de instruções. Falando de maneira leviana isso significa que há várias instruções e cada uma delas tem um nível de complexidade completamente variada. Boa parte das instruções são complexas na arquitetura x86. Uma instrução "complexa" é uma instrução que faz várias operações.
Cada instrução do código de máquina tem um tamanho que pode variar de 1 até 15 bytes. E cada instrução consome um número de ciclos diferente (devido a sua complexidade variada).

## Modulo

A arquitetura x86 segue o modelo da arquitetura de Von Neumann onde esse, mais uma vez resumindo, trabalha principalmente usando uma unidade central de processamento (CPU) e uma memória principal.

<p align="center">
  <img src="./.github/CPU.png">
</p>

<p>As instruções podem trabalhar manipulando/lendo dados em registradores que são pequenas áreas de memória internas à CPU. E também pode manipular dados na memória principal que no caso é a memória RAM. Bem como também usar o sistema de entrada e saída de dados, feito pelas portas físicas.
O registrador Program Counter no diagrama acima armazena o endereço da próxima instrução que será executada na memória principal. Na arquitetura x86 esse registrador é chamado de Instruction Pointer.</p>

## Portas físicas

Uma porta física é um barramento do processador usado para se comunicar com o restante do hardware. Por exemplo para poder usar a memória secundária, o HD, usamos uma porta física para enviar e receber dados do dispositivo. O gerenciamento desta comunicação é feito pelo chipset da placa-mãe.
Do ponto de vista do programador uma porta física é só um número especificado na instrução, muito parecido com uma porta lógica usada para comunicação em rede.

## FPU

Na época do 8086 a Intel também lançou o chamado 8087, que é um co-processador de ponto flutuante que trabalhava em conjunto com o 8086. Os processadores seguintes também ganharam co-processadores que receberam o nome genérico de x87. A partir do 80486 a FPU é interna a CPU e não mais um co-processador, porém por motivos históricos ainda chamamos a unidade de ponto flutuante da arquitetura x86 de x87.
FPU nada mais é que a unidade de processamento responsável por fazer cálculos de ponto flutuante, os famosos números float.

## Outras tecnologias

Quem dera um processador fosse tão simples assim, já mencionei que o manual da Intel tem mais de 5 mil páginas? Deixei de abordar muita coisa aqui mas que fique claro que os processadores da arquitetura x86 tem várias outras tecnologias, como o 3DNow! da AMD e o SSE da Intel.

<a id="Modo de processamento"></a>

# Modo de processamento 🤖

Como já explicado a arquitetura x86 foi uma evolução ao longo dos anos e sempre mantendo compatibilidade com os processadores anteriores. Mas código de 16, 32 e 64 bit são demasiadamente diferentes e boa parte das instruções não são equivalentes o que teoricamente faria com que, por exemplo, código de 32 bit fosse impossível de rodar em um processador x86-64. Mas é aí que entra os modos de processamento.
Um processador x86-64 consegue executar código de versões anteriores simplesmente trocando o modo de processamento. Cada modo faz com que o processador funcione de maneira um tanto quanto diferente, fazendo com que as instruções executadas também tenham resultados diferentes.
Ou seja, lá no 8086 seria como se só existisse o modo de 16 bit. Com a chegada dos processadores de 32 bit na verdade simplesmente foi adicionado um novo modo de processamento aos processadores que seria o modo de 32 bit. E o mesmo aconteceu com a chegada dos processadores x86-64 que basicamente adiciona um modo de processamento de 64 bit. É claro que além dos modos de processamento novos também surgem novas tecnologias e novas instruções, mas o modo de processamento anterior fica intacto e por isso se tem compatibilidade com os processadores anteriores.
Podemos dizer que existem três modos de processamento principais:

<p align="center">
  <img src="./.github/modoDePross.jpeg">
</p>

## Barramento interno

Os tais "bit" que são muito conhecidos mas pouco entendido, na verdade é simplesmente uma referência a largura do barramento interno do processador quando ele está em determinado modo de processamento. A largura do barramento interno do processador nada mais é que o tamanho padrão de dados que ele pode processar de uma única vez.
Imagine uma enorme via com 16 faixas e no final dela um pedágio, isso significa que 16 carros serão atendidos por vez no pedágio. Se é necessário atender 32 carros então será necessário duas vezes para atender todos os carros, já que apenas 16 podem ser atendidos de uma única vez. A largura de um barramento nada mais é que uma "via de bits", quanto mais largo mais informação pode ser enviada de uma única vez. O que teoricamente aumenta a eficiência.
No caso do barramento interno do processador seria a "via de bits" que o processador usa em todo o seu sistema interno, desconsiderando a comunicação com o hardware externo que é feita pelo barramento externo e não necessariamente tem o mesmo tamanho do barramento interno.

## Mais modos de processamento

Pelo que nós vimos acima então na verdade um "sistema operacional de 64 bit" nada mais é que um sistema operacional que executa em submodo de 64-bit. Ah, mas aí fica a pergunta:

    Se está rodando em 64 bit como é possivel execultar codigo de 32 bit ?

Isso é possível porque existem mais modos de processamento do que os que eu já mencionei. Reparou que eu disse "submodo" de 64-bit? É porque na verdade o 64-bit não é um modo principal mas sim um submodo. A hierarquia de modos de processamento de um processador Intel64 ficaria da seguinte forma:

  - Real mode (16 bit)
  - Protected mode (32 bit)
  - SMM (não vamos falar desse modo, mais ele existe)
  - IA-32e
    - 64-bit (64 bit)
    - Compatibility mode (32 bit)

O modo IA-32e é uma adição dos processadores x86-64. Repare que ele tem outro submodo chamado "compatibility mode", ou em português, "modo de compatibilidade".

    Não confundir com o modo de compatibilidade do Windows, ali é uma coisa diferente que leva o mesmo nome.

O modo de compatibilidade serve para obter compatibilidade com a arquitetura IA-32. Um sistema operacional pode setar para que código de apenas determinado segmento na memória rode nesse modo, permitindo assim que ele execute código de 32 e 64 bit paralelamente (supondo que o processador esteja em modo IA-32e). Por isso que seu Debian de 64 bit consegue rodar softwares de 32 bit, assim como o seu Windows 10 de 64 bit também consegue.

## Virtual-8086

Lembra que o antigo Windows XP de 32 bit era capaz de rodar programas de 16 bit do MS-DOS?
Isto era possível devido ao modo Virtual-8086 que, de maneira parecida com o compatibility mode, permite executar código de 16 bit enquanto o processador está em protected mode. Nos processadores atuais o Virtual-8086 não é um submodo de processamento do protected mode mas sim um atributo que pode ser setado enquanto o processador está executando nesse modo.

