## Objetivos de criptanálise
- Descobrir o texto original;
- Descobrir a chave;
- Descobrir o algoritmo.

>[!note]
>Normalmente os algoritmos não são secretos, mas há exceções.

## Conceitos base
Objetivo inicial da criptografia: Garantir que a mensagem da pessoa A chegue a pessoa B sem que a pessoa C consiga ler.

1. **Texto-limpo**: mensagem original.
2. **Cifra ou Esquema Criptográfico**: algoritmo que transforma o texto-limpo em texto-cifrado e vice-versa (por norma são dois algoritmos diferentes).
3. **Criptograma**: texto-cifrado.
4. **Chave de cifra**: conjunto de dados que permite a cifrar e/ou decifrar do texto-limpo.
5. **Sistema criptográfico**: conjunto de cifra, chave de cifra, conjunto de decifra e chave de decifra.
6. **Modelo de ataque**: classificação para um possível ataque ao sistema criptográfico.
7. **Ataque**: Tentativa de quebra dos objetivos da técnica criptográfica.
8. **Criptanálise**: Conjunto de técnicas que visam a quebra de sistemas criptográficos. Consistem em decifrar sem saber a chave ou tendo a chave.

## Cifras clássicas

### Cifra de substituição Mono alfabética
Tipo de cifra que utiliza **apenas uma** chave para cifrar e decifrar a mensagem.

#### Cifra de César
É uma cifra de substituição, em que cada letra do texto original é substituída por outra letra que se encontra um número fixo de posições à sua frente no alfabeto.

Ou seja: `C(K, M) = Mi + K mod 26`, onde 'K' é a chave, 'Mi' é uma letra da mensagem no índice 'i' e 26 é o número de letras do alfabeto.

### Cifra de substituição Poli alfabética
Tipo de cifra que utiliza **duas ou mais** chaves para cifrar e decifrar a mensagem.

#### Cifra de Vigenère
É uma cifra de substituição polialfabética, em que cada letra do texto original é substituída por outra letra que se encontra um número fixo de posições à sua frente no alfabeto, mas a chave é uma palavra. 

Esta cifra é mais difusa que a de César, pois ao utilizar uma palavra como chave, a mesma letra da mensagem original pode ser cifrada de várias formas diferentes, alterando assim a estatística das letras.

Ou seja: `V(K,M) = Mi + Ki mod 26`, onde 'K' é a chave, 'Mi' é uma letra da mensagem no índice 'i' e 26 é o número de letras do alfabeto.

#### Máquinas de Rotores
São máquinas que utilizam rotores para cifrar e decifrar mensagens. Estes rotores são discos com 26 posições, onde cada posição corresponde a uma letra do alfabeto. Cada rotor tem uma posição inicial, que é a chave de cifragem.

A cada letra que é cifrada, o rotor avança uma posição, alterando a cifra. Quando o rotor dá uma volta completa, o rotor à sua direita avança uma posição. Quando o rotor do meio dá uma volta completa, o rotor à sua esquerda avança uma posição. Assim que o rotor da direita dá uma volta completa, o rotor do meio avança uma posição.

#### Máquinas de Rotores vs Cifra de Vigenère
Em comparação com a cifra de Vigenère, a máquina de rotores oferece vários aprimoramentos:

**Complexidade Superior**: A cifra de rotores é mais complexa e difícil de quebrar do que a cifra de Vigenère devido à substituição polialfabética, ao movimento dos rotores e aos refletores.

**Segurança Dinâmica**: A cifra de Vigenère usa uma única chave repetida, o que torna a quebra da cifra mais fácil se o tamanho da chave for descoberto. As máquinas de rotores usam uma chave inicial que muda constantemente, tornando a quebra mais desafiadora.

**Resistência à Análise de Frequência**: A cifra de Vigenère ainda é suscetível à análise de frequência, enquanto a cifra de rotores torna essa técnica de quebra menos eficaz devido à constante mudança nas substituições.

## Cifra segura a nível teórico vs Cifra segura a nível computacional

- **Segurança da Teoria da Informação** (Information-Theoretic Security):
  - O espaço de todas as mensagens possíveis
  - O espaço de todos os textos cifrados possíveis
  - O espaço de todas as chaves possíveis
  - A cifra não pode ser quebrada, mesmo que o adversário tenha poder computacional infinito
  - Segurança perfeita, um conceito onde a criptografia é absolutamente invulnerável. As suas características são a indistinguibilidade, onde a mensagem cifrada é indistinguível de uma mensagem aleatória, a chave aleatória e única para cada mensagem e a chave é tão longa (ou mais) quanto a mensagem.
- **Segurança ao nível Computacional** (Computational Security):
  - O adversário tem poder computacional limitado
  - A cifra pode ser quebrada, mas o custo computacional é muito elevado
  - Segurança prática, onde a criptografia é invulnerável a ataques com recursos limitados. As suas características são a indistinguibilidade, onde a mensagem cifrada é indistinguível de uma mensagem aleatória, a chave aleatória e única para cada mensagem e a chave é tão longa (ou mais) quanto a mensagem.

### Cifra de Vernam (ou cifra de chave única)
Foi o primeiro exemplo de uma cifra segura (contra Cipher-only Attacks ou COA). 

Funciona da seguinte forma:
 - É obtido o texto limpo e a chave, ambos em bits.
 - Para cifrar E(k,m) = k xOR m
 - Para decifrar D(k,c) = k xOR c

Nota: Cada chave deve ser usada apenas uma vez e escolhida aleatoriamente para cada texto-limpo a cifrar.

É de notar que esta cifra tem **limitação**, pois a chave tem de ser **tão grande** quanto o **texto a cifrar** e usadas **apenas uma vez**. Algo que as cifras continuas convencionais **superam**, pois as mesmas permitem **chaves mais curtas** e uma **reutilização segura das chaves**.

## Cifras simétricas
São cifras que usam a **mesma chave** para cifrar e decifrar. Têm como vantagem **performance** e como desvantagem a **troca de chaves** (para ter segurança N pessoas precisam de `N * (N - 1) / 2` chaves).

Existem dois tipos de cifras simétricas:
 - **Simétricas continuas**: a cifragem é feita byte a byte, ou seja, o texto cifrado é gerado à medida que o texto plano é lido.
 - **Simétricas por blocos**: a cifragem é feita por blocos de tamanho fixo, ou seja, o texto cifrado é gerado quando o bloco é lido.

## Cifra de DES
A cifra de DES é uma cifra simétrica por blocos. Usa na sua arquitetura **redes de feistel**. Tem outras variantes como o **3DES** que envolve 3x mais rondas na rede de feistel (DES tem 16 rondas, 3DES tem 48 rondas).

## Cifra de AES
A cifra de AES é uma cifra simétrica por blocos. Usa na sua arquitetura **substituição-permutação**.

Funciona da seguinte forma:
 1. Divide o texto-limpo em blocos de 128 bits (16 bytes);
 2. É fornecida uma chave de cifragem;
 3. É calculado o **número de rodadas** dependendo do tamanho da chave (128 bits = 10 rondas, 192 bits = 12 rondas, 256 bits = 14 rondas);
 4. A chave é expandida em várias sub-chaves, uma para cada rodada;
 5. Após todas as rodadas é obtido o texto cifrado.

Em cada **rodada**:
 1. **AddRoundKey**: o bloco é combinado com uma sub-chave exclusiva daquela rodada usando o XOR, o resultado é uma matriz 4x4 (16 bytes);
 2. **SubBytes**: cada byte no bloco é substituído por outro byte de acordo com uma tabela de substituição (S-box);
 3. **Shiftrows**: as linhas no bloco são permutadas (movidas) para a esquerda, essas permutação podem variar (0,1,2 e 3);
 4. **MixColumns**: as colunas no bloco são permutadas;

Existem **5 modos de cifra**, onde:
- Três são continuas: CTR, CFB e OFB;
- Duas são por blocos: ECB e CBC;
### *Eletronic Code Book* (ECB)
O **ECB** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma independente. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (caso os blocos não sejam iguais) para cada bloco de dados.

Nota: **Não é recomendado** o uso para mensagens acima de 12 bytes não pseudo-aleatórios.

Exemplo para **cifrar**:

| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |
| Algoritmo | AES-e(k,m[0]) | AES-e(k,m[1]) | AES-e(k,m[2]) |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |

Exemplo para **decifrar**:

| Texto     | Bloco 1       | Bloco 2       | Bloco 3       |
| --------- | ------------- | ------------- | ------------- |
| Cifrado   | 934fafa       | 9f9f9f9       | 934fafa       |
| Algoritmo | AES-d(k,c[0]) | AES-d(k,c[1]) | AES-d(k,c[2]) |
| Limpo     | aaaaaaa       | bbbbbbb       | aaaaaaa       |

**Vantagens** deste modo:
 - Permite o acesso aleatório a dados cifrados.
 - Permite processamento paralelo da informação.
 - Não tem problemas de propagação de erros entre blocos.

**Desvantagens** deste modo:
 - Não é seguro a ataques COA (*Cipher-Only attack*) e ataques por *code book* (compilação de pares texto limpo/criptograma).
 - Não permite pré-processamento.
 - O último bloco necessita sempre de preenchimento.
 - Erros de sincronização são irrecuperáveis.

### *Cipher Block Chaining* (CBC)
O **CBC** é um modo de operação de cifra que consiste em cifrar cada bloco de dados de forma dependente do bloco anterior. Ou seja, o bloco de dados é cifrado com a mesma chave, mas o resultado é diferente (mesmo os blocos sendo iguais) para cada bloco de dados. Este método evita **alguns** ataques por maninupulação de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Recebe um vetor de inicialização (IV) - gerado aleatóriamente, único para cada mensagem e partilhado entre as duas partes;
 - É feito o XOR entre o bloco de texto-limpo e o IV;
 - O resultado do XOR é cifrado com a chave;
 - O resultado cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte;
 - Processo repete-se até ao fim da mensagem;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Este bloco é decifrado com a chave;
 - É feito o XOR entre o bloco de decifrado e o IV;
 - Esse bloco cifrado é enviado para o bloco seguinte e irá ser feito o XOR com o bloco seguinte após ser decifrado;
 - Processo repete-se até ao fim da mensagem;

**Vantagens** deste modo:
 - É seguro contra ataques CPA (*Chosen-Plaintext Attack*).
 - Os padrões são mascarados pelo XOR e efeito cascata.
 - Textos limpos iguais resultam em criptogramas distintos, inviabilizando ataques por *code book*.
 - Permite o acesso aleatório a dados cifrados.
 - Permite processamento paralelo da informação cifrada.

**Desvantagens** deste modo:
 - Ataques por manipulação do IV podem não ser detetáveis.
 - Não permite processamento paralelo da informação na cifragem. 
 - Erros de perda de bits são irrecuperáveis e um erro num bit afeta o bloco de texto limpo correspondente e o seguinte (cascata).

#### *Padding* (Preenchimento)
O **padding** é uma técnica de preenchimento de dados que consiste em adicionar um número de bytes ao final de um bloco de dados, de forma a que o tamanho do bloco de dados seja múltiplo do tamanho do bloco de dados da cifra.

Nota: O último bloco tem sempre *padding*, mesmo que o bloco da mensagem seja múltiplo do tamanho do bloco da cifra é acrescentado um bloco de *padding*.

### *Output Feeback Mode* (OFM)
O **OFM**  é um modo de operação de cifra que consiste em cifrar o IV com a chave e fazer o XOR entre o resultado e o bloco de texto-limpo.

Exemplo a **cifrar**:
- Recebe um bloco de texto-limpo;
- Recebe um vetor de inicialização (IV) - gerado aleatóriamente, único para cada mensagem e partilhado entre as duas partes;
- É cifrado o IV **anterior** com a chave;
- É feito o XOR entre o bloco de texto-limpo e o resultado do IV cifrado;
- Processo repete-se, usando o IV do bloco anterior, até ao fim da mensagem;

**Vantagens** deste modo:
 - Permite pré-processamento.
 - Permite processamento paralelo da informação (caso, seja feito o pré-processamento).
 - Permite acesso aleatório a dados cifrados (caso, seja feito o pré-processamento).

**Desvantagens** deste modo:
 - Sendo ela uma cifra de chave simétrica contínua, ela fica **maneável**.
 - Erros de perda bits são irrecuperáveis.

### *Ciphertext Feedback Mode* (CFM)
O **CFM**  é um modo de operação de cifra que consiste em cifrar o IV com a chave e fazer o XOR entre o resultado e o bloco de texto-limpo. A diferença entre o CFM e o OFM é que o CFM usa o bloco de texto-cifrado anterior e não o IV cifrado.

Exemplo a **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Recebe um vetor de inicialização (IV);
 - É cifrado o IV **anterior** com a chave (neste caso o IV é obtido através da operação xOr entre o IV cifrado e o bloco de texto-limpo);
 - Processo repete-se, usando o IV do bloco anterior, até ao fim da mensagem;

Exemplo a **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Recebe um vetor de inicialização (IV);
 - É decifrado usando o IV cifrado na primeira iteração;
 - As restantes iterações usa como IV o bloco de texto-cifrado anterior e é feito o xOr com o bloco de texto-cifrado atual;
 - Processo repete-se, até ao fim da mensagem;

**Vantagens** deste modo:
 - Permite processamento em paralelo para a decifragem.
 - Existe a capacidade de recuperação de erros.

**Desvantagens** deste modo:
 - Sendo ela uma cifra de chave simétrica contínua, ela fica **maneável**.
 - Um erro pode propagar-se para os bits seguintes.

### *Randomized Couter Mode* (CTR)
O **CTR** é um modo de operação de cifra que consiste em cifrar através de uma chave de cifra de forma simétrica e continua a partir de uma cifra de blocos.

Exemplo para **cifrar**:
 - Recebe um bloco de texto-limpo;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-limpo e o contador;

Exemplo para **decifrar**:
 - Recebe um bloco de texto-cifrado;
 - Cria um contador (CTR) - do mesmo tamanho que o bloco, gerado aleatóriamente através da chave de cifra;
 - Faz o XOR entre o bloco de texto-cifrado e o contador;

**Vantagens** deste modo:
 - É seguro contra ataques CPA (*Chosen-Plaintext Attack*).
 - Os padrões do texto-limpo são mascarados por imitar o processo de uma cifra contínua.
 - Textos-limpos iguais resultam em criptogramas distintos, inviabilizando ataques por *code book*.
 - Permite o acesso aleatório a dados cifrados.
 - Permite o processamento paralelo da informação.

**Desvantagens** deste modo:
 - Sendo ela uma cifra de chave simétrica contínua, ela fica **maneável**.
 - Erros de perda bits são irrecuperáveis.

## Qual modo escolher?

![[modos_de_cifra.png|600]]

## Funções de *hash*

Funções que dado uma entrada de qualquer tamanho, produzem uma saída de um tamanho fixo.

Baseiam-se em **três propriedades**:
 - **Resistência à colisão**: é difícil encontrar dois inputs que produzam o mesmo output;
 - **Resistência à pré-imagem**: é difícil encontrar um input que produza um output específico;
 - **Resistência à segunda pré-imagem**: é difícil encontrar um input que produza o mesmo output que um input específico;

### Funções de Hash Criptográficas (Abordagens)

#### Construção Merkle-Damgard
  1. Divide o input em blocos de tamanho fixo e aplica uma função de compressão a cada bloco, sendo que o output da função de compressão é usado como input para a próxima iteração. 
  2. O output final é o output da última iteração (e.g. MD5, SHA-1, SHA-2, SHA-3);
#### Funções esponja (Sponge Functions)

  1. **Absorção**: Atualiza um estado interno (pool de entropia) com blocos de input de tamanho fixo (padding é adicionado se necessário).
  2. **Espremer (Squeezing)**: O output final é o output da última iteração.

## Message Authentication Code (MAC)

Tem como propósito garantir que uma determinada mensagem não foi alterada e que foi enviada por uma determinada entidade (autenticidade).

Há várias formas de construir um MAC, algumas delas são:
 - **HMAC** (Hash-based Message Authentication Code): este MAC tem dois algoritmos, um para construção e outro para verificação e recebe dois inputs, um é a chave e o outro é a mensagem;

As **três formas** possíveis de combinar os dois mecanismos são:
 - *MAC and Encrypt*: Processo onde é calculado o MAC **através da mensagem** e depois é cifrada a mensagem concatenando o com o MAC (e.g. SSH);
 - *MAC then Encrypt*: Processo onde é calculado o MAC **através da mensagem** e depois é cifrado MAC dessa mensagem (e.g. TLS);
 - *Encrypt then MAC*: Processo onde é calculado o MAC **através da mensagem cifrada** (e.g. IPsec).

## RSA
Um cifra de chave pública que precisa de:

- Gerador de chaves: 
	  1. Primeiramente geramos dois números primos extremamente grandes, p e q.
	  2. Calcula-mos `N = p * q`.
	  3. Calcula-mos `phi(N) = (p - 1) * (q - 1)`.
	  4. Escolhe-se um expoente de encriptação `e` tal que `1 < e < phi(N)` e `mdc(e, phi(N)) = 1`.
	  5. Calcula-se o expoente de desencriptação `d` tal que seja o inverso multiplicativo de `e` módulo `phi(N)`, ou seja, `d * e = 1 mod phi(N)`.
	  6. A chave pública é `(N, e)` e a chave privada é `(N, d)`.
- Para cifrar fazemos a seguinte operação: `C = M^e mod N`, sendo o M a mensagem a cifrar e C a mensagem cifrada;
- Para decifrar fazemos a seguinte operação: `M = C^d mod N`, sendo o C a mensagem cifrada e M a mensagem decifrada.

>[!note]
>A segurança desta cifra basea-se no problema do logaritmo discreto e no problema da fatorização de números primos.

>[!important]
>Normalmente não se utiliza o **Text Book RSA** (apenas cifrar o conteúdo pretendido). Invés disso é acrescentado um padding aleatório para aumentar a segurança (OAEP ou Optimal Assimetric Encription Padding).

### Aritmética Modular

A aritmética modular é essencial para manter os cálculos dentro de um intervalo específico, preservando a segurança e a integridade do esquema de partilha de segredo.
### Teorema do  Chinês

O Teorema do Resto Chinês é um resultado matemático que facilita a **resolução de sistemas de congruências lineares**. Este teorema é utilizado para acelerar o **processo de decifragem do RSA**. Ele diz que se tivermos um sistema de congruências lineares, podemos resolver o sistema de forma mais rápida se resolvermos cada congruência individualmente.

Por exemplo, se o expoente usado para cifrar uma mensagem é sempre 3 e em que não se usa padding aleatório, enviar a mesma mensagem m para três destinatários diferentes, com chaves públicas (n1, 3), (n2, 3) e (n3, 3), é altamente desaconselhado, já que se as três mensagens cifradas, `m3 mod n1`, `m3 mod n2` e `m3 mod n3`, forem intercetadas é possível recuperar a mensagem original, da seguinte forma:
  - Seja m a mensagem original;
  - Seja n1, n2 e n3 os módulos das chaves públicas;
  - Seja c1 = `m^3 mod n1`, c2 = `m^3 mod n2` e c3 = `m^3 mod n3`, isto é os residuos da divisão de m^3 por n1, n2 e n3, respectivamente;
  - Seja N = `n1*n2*n3`, N é o produto dos módulos das chaves públicas;
  - Seja N1 = N/n1, N2 = N/n2 e N3 = N/n3;
  - Seja y1, y2 e y3 os inversos multiplicativos de N1, N2 e N3, respetivamente;
  - Seja x = `c1*y1*N1 + c2*y2*N2 + c3*y3*N3`;
  - A mensagem original é `m = x^(1/3) mod N`;

## Criptografia de chave pública

A criptografia de chave pública moderna é baseada na teoria dos números e em problemas difíceis de resolver. Alguns exemplos são os protocolos de acordos de chaves, assinaturas digitais e cifras de chave pública.

Exemplos de problemas intratáveis com mais relevância:
- O problema do logaritmo discreto;
- O problema da fatorização de números compostos em números primos;
### Problema do logaritmo discreto

Consiste em encontrar o valor de um número inteiro (exponencial) que é utilizado para cifrar uma mensagem, conhecido o valor da base e o resultado da exponenciação, num grupo finito. Esse problema é considerado difícil de resolver computacionalmente quando se trabalha com números grandes, tornando-o fundamental para garantir a segurança da criptografia de chave pública.

>[!note]
>A definição mais geral do problema recorre apenas a grupos cíclicos, aplicando-se, por isso a outros grupos diferentes de números primos. O melhor algoritmo conhecido para resolver o problema do logaritmo discreto é conhecido por *general number field sieve*, determinando o tamanho que o número tem de ter para o problema ser considerado seguro.

### Problema da fatorização de números compostos

Consiste no facto de ser é computacionalmente inviável fatorizar um número composto pelo produto de dois números primos grandes. Por exemplo, se tivermos o número 15, ele pode ser decomposto em 3 e 5, que são números primos. O problema da fatorização torna-se difícil à medida que os números tornam-se maiores, e isso é utilizado em esquemas de criptografia de chave pública baseados em algoritmos como o RSA. 
## Assinatura Digital

Os esquemas de assinatura digital atuais são normalmente construídos usando criptografia de chave pública. Estas são algumas das propriedades:

- Autenticidade da Informação
- Integridade dos Dados
- Garantia de Não Repúdio
- Autenticação da Origem da Informação
- Dificuldade de Falsificação 

Repare-se que, na verdade, enquanto que a assinatura digital pode garantir todas as propriedades anteriores, o mesmo não costuma acontecer para as assinaturas manuscritas.
## Protocolos de acordos de chaves

Neste capítulo é apresentado formas de trocar ou estabelecer um segredo entre duas entidades sem haver nada secreto acordado à partida. Essa troca é realizada por uma comunicação segura, aonde as partes enviam mensagens encriptadas uma para a outra e usam técnicas de criptografia e matemática para garantir que apenas elas possam obter a chave secreta compartilhada. O objetivo é garantir a segurança e a privacidade das comunicações entre as partes envolvidas.

Nota: Este tipo de protocolo deve ser utilizado em situações de ataque ao homem no meio passivo, onde o atacante não consegue modificar as mensagens que são enviadas entre as partes.

## Protocolo de Diffie-Hellman

Este é um exemplo de um protocolo de acordo de chaves, onde duas partes podem concordar sobre uma chave secreta, mesmo que nunca tenham trocado qualquer informação secreta anteriormente. A sua segurança basea-se no problema do logaritmo discreto.

Funciona da seguinte forma:
 1. Alice e Bob escolhem um número primo P e um número G que seja raiz primitiva de P;
 2. Alice escolhe um número secreto A e Bob escolhe um número secreto B;
 3. Alice calcula G^A mod P e envia para Bob;
 4. Bob calcula G^B mod P e envia para Alice;
 5. Alice calcula (G^B mod P)^A mod P;
 6. Bob calcula (G^A mod P)^B mod P;
 7. Ambos obtêm o mesmo resultado, que é a chave secreta partilhada.

Para estabelecer um segredo entre 3 partes (ao invés de 2), é feito do seguinte modo:
 1. Alice, Bob e Carol escolhem um número primo P e um número G que seja raiz primitiva de P;
 2. Alice escolhe um número secreto A, Bob escolhe um número secreto B e Carol escolhe um número secreto C;
 3. Alice calcula G^A mod P (y_a) e envia para Bob;
 4. Bob calcula G^B mod P (y_b) e envia para Carol;
 5. Carol calcula G^C mod P (y_c) e envia para Alice;
 6. Bob calcula (y_c)^B mod P (K_ab);
 7. Carol calcula (y_a)^C mod P (K_bc);
 8. Alice calcula (y_b)^A mod P (K_ca);
 9. Cada participante combina as chaves partilhadas para obter a chave secreta partilhada (K = K_ab + K_bc + K_ca).

## Curvas Elípticas
A segurança deste método basea-se no problema do logaritmo discreto.

Numa curva eliptica, a adicao de 3 pontos dá origem a um terceiro ponto nessa mesma curva eliptica, sendo P1+P2=P3. 

O que acontece é que é tracada uma reta que passa por P1 e P2 que interceta P3 na curva noutro local. Se os dois pontos P1 e P2 coincidirem, isto e, forem o mesmo, a reta vai ser tangente à curva eliptica e irá econtrar o segundo ponto na curva eliptica, fazendo P1+P2=P3 <=> P1+P1=P3 <=> 2*P1=P3. Desta forma obtem-se uma multiplicacao por 2. 

Para explorar esta propriedade são feitas várias somas consecutivas da seguinte forma:
```
11P = 8P + 2P + P
8P = 4P + 4P
4P = 2P + 2P
2P = P + P
```

Para multiplicar um ponto de um curva eliptica, usando um número inteiro negativos adiciona-se um passo, que é a multiplicação do ponto por -1, e depois faz-se a soma dos pontos. Por exemplo:
```
11P = -8P - 2P - P
-8P = -4P - 4P
-4P = -2P - 2P
-2P = (-P) + -(P) = -P - P
```

>[!note] 
>O protocolo Diffie-Helman pode ser implementado usando curvas elípticas, pois a operação de multiplicação de um ponto por um escalar é computacionalmente difícil de ser invertida;

Este protocolo é implementado por curvas elípticas da seguinte forma:
  - Alice e Bob concordam em usar uma curva elíptica sobre um corpo finito e um ponto gerador G;
  - Alice escolhe um ponto `y_a` e Bob escolhe um ponto `y_b`;
  - Alice calcula `k_a = y_a * G` e Bob calcula `k_b = y_b * G`;
  - A chave será o ponto `k_a * y_b = k_b * y_a`;
## Assinaturas digitais

As assinaturas digitais permitem, **autenticar conteúdos de um documento** (integridade), **autenticar a origem do documento** (autenticidade) e garantir a **não repúdio** (não negação da autoria).

As assinaturas digitais são compostas por **dois algoritmos**:
- **Geração de assinaturas**: produção de um valor usando a **chave privada**;
- **Verificação de assinaturas**: validação do valor usando a **chave pública**.

Existem dois **esquemas de assinatura digital**:
- **Esquema de assinatura com apêndice**: a assinatura é separada do mensagem. A mensagem pode ser visualizada sem a assinatura validada;
- **Esquema de assinatura com recuperação de mensagem**: a assinatura é incluída na mensagem. A mensagem não pode ser visualizada sem a assinatura validada.

### Algoritmo de geração de assinaturas

Para **esquemas de assinatura com recuperação de mensagem**:
- É assinado o documento, Assinatura(Mensagem) = informação + E(Priv, documento)
- Para verificar a assinatura, extraimos a chave pública das informações e, D(Pub, Assinatura) e verificamos a integridade do documento.

Para **esquemas de assinatura com apêndice**:
- É assinado o documento, Assinatura(Mensagem) = E(Priv, Hash(Mensagem))
- Para verificar a assinatura, extraimos a chave pública das informações e, D(Pub, Assinatura) = hash'(Mensagem) e verificamos se o hash' é igual ao hash da mensagem.

**Elementos principais** de uma assinatura digital:
- A mensagem a assinar;
- Data da assinatura;
- Identificação do assinante;

A **data da assinatura** pode ser:
- Dada pela máquina que assina;
- Dada por uma **entidade de confiança** (TSA ou Time Stamp Authority).

### TSA (Time Stamp Authority)

A **Time Stamp Authority** é uma entidade de confiança que fornece **carimbos de tempo**. 

Estes carimbos de tempo são usados para **provar a existência de uma mensagem** num determinado momento e proteje contra **ataques de falsificação**. 

É feito o hash da mensagem, o mesmo é contatenado com a data e é assinado o hash dessa contatenação com a chave privada da TSA.

A **identificação do assinante** pode ser:
- Fornecida por um **certificado de chave pública**;

### Certificado de chave pública

Este certificado fornece:
- Diversos atributos de identificação do assinante;
- A chave pública do assinante, para verificação da assinatura;
- Prazo de validade do certificado;
- **CRL** (Certificate Revocation List) ou **OCSP** (Online Certificate Status Protocol) para verificar a validade do certificado.

A assinatura digital pode também ter **elementos opcionais**:
- **Localização de onde foi assinado**;
- **Motivo da assinatura**;
- etc.

### Assinaturas digitais com RSA

- Criação de assinaturas com a chave privada, validação com a chave pública;
- Padding especial para esquemas de assinatura com apêndice (i.e. RSASSA-PSS e RSASSA-PKCS1-v1_5);
- Prefixação com o algoritmo de hash usado (i.e. ASN.1);

### ASN.1 prefixação

É composto por um **OID** (Object Identifier) que contém o algoritmo de hash usado. Este OID é seguido pelo **hash** da mensagem.

### Standards de assinatura digital (DSS)

Existem dois standards de assinatura digital:
- Com a variante do **ElGamal** (DSA);
- Com curvas elípticas (ECDSA);
### Blind signatures

É um esquema de assinatura digital que permite que uma entidade assine uma mensagem sem saber o conteúdo da mesma. É usado para garantir a anonimidade de uma mensagem.

Implementação, usando RSA:

**Escolha do Fator do Blinding Factor - k:**
Gere um número aleatório K.

**Propriedade do Fator de Ofuscação:**
Garanta que K × K^(-1) ≡ 1 (mod N), onde N é o módulo da chave RSA.

**Ofuscação da Mensagem (m'):**
Calcule m' = K^e × m mod N, onde e é a chave pública de RSA.

**Assinatura Usando a Chave Privada (Ax(m')):**
Compute Ax(m') = (m')^d mod N, onde d é a chave privada de RSA.

**Unblinding da Assinatura (Ax(m)):**
Calcule Ax(m) = K^(-1) × Ax(m') mod N.
### Assinatura eletrónica qualificada

Para uma assinatura eletrónica ser qualificada, é necessário:
- Ser compatível com a regulamentação da UE eIDAS;
- Permite a verificação de autoria por longos períodos de tempo;
- Pode ser considerado o equivalente eletrónico de uma assinatura manuscrita;

Contém **três requisitos**:
- A pessoa que assina deve ser vinculada e identificada de forma inequívoca à assinatura;
- Os dados usados para criar uma assinatura devem estar sob o controle exclusivo do signatário;
- Deve ser possível detectar alterações nos dados assinados;

Estas assinaturas pode ser produzidas por **dispositivos criptográficos qualificados**, como:
- Cartão do cidadão;
- Smart card;
- Chave Móvel Digital;

Estes dispositivos dão uma nova camada de segurança, pois:
- A chave privada não sai do dispositivo (não pode ser copiada nem exportada);
- Além da portação física, é necessário um segundo fator de autenticação (PIN);
- São certificadas por uma entidade de confiança;
### PKCS #11

É uma API que permite a utilização de dispositivos criptográficos (i.e. cartão do cidadão) e que permite a utilização de chaves privadas e a realização de operações criptográficas.

### Long-Term Validation (LTV)

É um mecanismo que permite a validação de assinaturas digitais de um modo intemporal, mesmo que o algoritmo de assinatura tenha ficado inválido ou o certificado esteja revogado. Isto é feito através de **camadas de assinatura**.

#### Proof of Existence

É um mecanismo que permite provar que um determinado documento existia numa determinada data.

Caso um documento possa ser validado agora e o timestamp esteja vinculado a valores que eram válidos quando foi assinado, então esses valores são válidos agora.

Tipos de assinaturas:
  - PAdES (PDF Advanced Electronic Signatures);
  - CAdES (CMS Advanced Electronic Signatures);
  - XAdES (XML Advanced Electronic Signatures);

## Gestão de chaves assimétricas

A gestão de chaves assimétricas **permite**:
  - Saber quando e como as chaves foram geradas;
  - Como as chaves privadas são protegidas;
  - Como as chaves públicas são distribuídas;
  - Prazo de validade do par de chaves;

A geração de chaves assimétricas **deve ser feita**:
  - **Usando bons PRNGs** (Pseudo Random Number Generator);
  - **Facilitar a geração sem comprometer a segurança**;
  - **Auto geração da chave privada**;

### Exploração da chave privada

A chave privada deve:
  - Ter a sua comprometidão minimizada;
  - Confinada (isolada) a um dispositivo seguro;

### Distribuição do certificado de chave pública

A chave pública deve ser distribuída entre:
  - **Remetentes** de dados confidenciais;
  - **Recepetores** de dados assinados;

Esta distribuição pode ser feita por:
  - **Cadeia de certificados**;
  - **Transitivade de confiança** (se A confia em B e B confia em C, então A confia em C);

Pode ser feita através de:
  - **Modo explícito**: pedido de modo voluntário pelo utilizador;
  - **Modo implícito**: pedido do utilizador a um serviço para obter um certificado necessário (i.e. acesso a um website).

Os certificados de chave pública são emitidos por **entidades de confiança** (CA ou Certificate Authority).

### Utilização do par de chaves

Um par de chaves está ligado a um perfil de utilização pelo certificado de chave pública.

Utilizações:
  - **Autenticação**;
  - **Assinatura de documentos**;
  - **Emissão de certificados**;

Para classificar a sua utilização, existem **extensões**, identificadas por um **OID**:
  - Uma **extensão crítica**: se não for reconhecida, o certificado não é válido;
  - Uma **extensão não crítica**: mesmo se não for reconhecida, o certificado é válido;

### Cadeia de certificados

A cadeia de certificados é uma **lista de certificados** que permite validar um certificado de chave pública.

É composta por:
  - **Certificado de chave pública**;
  - **Certificado de chave pública da(s) CA(s)**;
  - **Certificado de chave pública do CA raiz (root)**;

### Autoridade de certificação (CA)

É uma entidade de confiança que emite certificados de chave pública.

Define **politicas de certificação**:
  - Emissão de certificados;
  - Revogação de certificados;
  - Distribuição de certificados;
  - Emissão e distribuição da chave privada correspondente;

Tipos de CA:
  - **CA raiz (root)**: emite certificados de chave pública para outras CA;
  - **CA intermédia**: emite certificados de chave pública para utilizadores finais;

Existem **modelos de hierarquia de certificados**:
  - **PGP**: rede de confiança, onde não existe uma autoridade central e cada utilizador é uma CA. Existem dois tipos de confiança:
    - **Marginal**: o utilizador confia no certificado, mas não confia na capacidade do utilizador de verificar outros certificados;
    - **Completamente**: o utilizador confia no certificado e na capacidade do utilizador de verificar outros certificados;
  - **PEM**: hierarquia de certificados, onde existe uma CA raiz e CA intermédias (nunca implementado: floresta de hierarquias, onde cada CA raiz negoceia a distribuição de chaves públicas com outras CA raiz);

### Atualização de chaves assimétricas
Estes pares de chaves devem ter um **prazo de validade**, pois a sua segurança pode ser comprometida.

Os certificados de chave pública podem ser distribuidos livremente, por isso existe:
  - Certificados com **prazo de validade**;
  - Lista de certificados **revogados** (CRL ou Certificate Revocation List);

### CRL (Certificate Revocation List)

É uma lista de certificados revogados, emitida por uma CA.
Pode ser do tipo: 
  - Base: lista de certificados revogados;
  - delta: lista de certificados revogados desde a última lista base;

Validações de Certificados Individuais:
  - **OCSP (Online Certificate Status Protocol)**: protocolo que permite verificar o estado de um certificado;
  - OCSP Stapling: permite que o servidor web verifique o estado do certificado;

Distruibuição de CRLs é feita por:
  - Cada CA publica a sua CRL;
  - As CAs trocam entre si as suas CRLs;

Ao ser revogada:
  - A chave privada pode ser usada para assinar, porém é inválida;
  - A chave pública pode ser usada a qualquer momento;

### Infraestrutura de chaves públicas (PKI)

É um conjunto de hardware, software, pessoas, políticas e procedimentos necessários para criar, gerir, armazenar, distribuir e revogar certificados de chave pública.

É composta por:
  - A criação dos pares de chave assimétricas para cada entidade;
  - A criação e distribuição dos certificados de chave pública;
  - Definição e uso de cadeias de certificados;
  - Atualização, publição e distribuição de CRLs;
  - Uso de estruturas de dados e protocolos que permitem o funcionamento de serviços;

Tem as seguintes **entidades**:
- **Autoridade de Certificação** (CA): Esta entidade é responsável por emitir, revogar, renovar e gerenciar certificados de chave pública. A CA é crucial para estabelecer a confiança na identidade associada a uma chave pública.

- **Autoridade de Registro** (AR): A AR é encarregada de verificar a identidade dos solicitantes antes que eles possam obter um certificado da CA. A AR age como intermediária entre o usuário e a CA, garantindo que a CA emita certificados apenas para entidades legítimas.

- **Autoridade de Validação** (VA): Em alguns contextos, o termo Autoridade de Validação (VA) pode ser usado para se referir à Autoridade de Certificação (CA). No entanto, em certos sistemas, a VA pode ser uma entidade separada que valida informações específicas sobre os certificados emitidos pela CA.

A PKI define relações de confiança de duas formas diferentes:
- **Emitindo certificados de chave pública de outras CAs**: Hierarquicamente abaixo delas;
- **Requisitando a certificação de chave pública de outras CAs**: Hierarquicamente acima delas;

Estas relações de confiança podem ser:
- **Hierárquicas**: CA raiz e CA intermédias;
- **Cruzadas (cross-certification)**: CA raiz e CA raiz;
- **Em malha (mesh)**: grafos de certificação;

## Partilha de segredos

### Oblivious Transfer (OT)
O Oblivious Transfer (OT) é um protocolo criptográfico que permite a transferência de informações entre duas partes, de tal forma que uma das partes (o destinatário) obtenha uma das opções de informação, enquanto a outra parte (o remetente) permanece ignorante sobre qual informação específica foi escolhida.

#### One-of-Two OT
O remetenente tem duas mensagens, M0 e M1, e o destinatário tem um bit b. O destinatário recebe M_b, mas não sabe qual das duas mensagens recebeu.

Funcionamento:
- O remetente tem duas mensagens, M0 e M1. Ele gera um par de chaves RSA ((N,e), (N,d)) e envia a chave pública para o destinatário (N, e);
- O remetente gera dois valores aleatórios, x0 e x1 e envia para o destinatário;
- O destinatário gera um valor aleatório k e escolhe um bit b;
- O destinatário calcula `v = (x_b + k^e) mod N` e envia para o remetente;
- O remetente calcula `v0 = (v - x0)^d mod N` e `v1 = (v - x1)^d mod N`;
- O remetente calcula `M'0 = (M0 + v0) mod N` e `M'1 = (M1 + v1) mod N` e envia para o destinatário;
- O destinatário então calcula `M_b = (M'b - k) mod N`, obtendo a mensagem desejada;

Isto resulta, pois a Alice não consegue computar o valor de v pois não conhece o valor de k nem o b escolhido. E o Bob não consegue computar o valor da outra mensagem pois não conhece o valor de d.

## Provas com conhecimento nulo (Zero-Knowledge Proofs)

São um método criptográfico utilizado para provar o conhecimento sobre um dado, sem revelar o próprio dado à entidade a autenticar.

## Cifras homomórficas

Uma **cifra homomórfica** é uma cifra que permite que operações matemáticas sejam realizadas sobre os textos cifrados, sem que seja necessário decifrados o texto. Isso permite que os dados sejam processados sem revelar o seu conteúdo, o que é útil em muitos cenários, como a computação em cloud.

A definição formal de cifragem homomórfica é a seguinte:

> [!important]
> Seja M um espaço de mensagens, C um espaço de textos cifrados e E um algoritmo de cifragem. 
> Diz-se que E é homomórfico se existir uma função f tal que para todo m1 e m2 em M, E(m1) (0) E(m2) = E(m1 (0) m2), sem nenhuma decifragem intermediária.

> [!note]
> (0) é uma operação aplicada sobre o espaço de mensagens, e o = simboliza 'pode ser computado através de'

Caso (M, (0)M) e (C, (0)C) sejam grupos, então nós temos um *grupo homomórfico*. Nós dizemos que o esquema é *aditivamente homomórfico* se considerarmos a operação de grupo como a adição, e *multiplicativamente homomórfico* se considerarmos a operação de grupo como a multiplicação.

É de grande interesse a implementação desta propriedade não só para um operador, mas para dois ao mesmo tempo, também denominado de *[homoforismo de anéis](https://pt.wikipedia.org/wiki/Homomorfismo_de_an%C3%A9is)*.

> [!important]
> Tal que para todo o m1 e m2 em M:
> 
> E(m1) + E(m2) = E(m1 + m2),
> 
> E(m1) * E(m2) = E(m1 * m2).

Estas definições significam que para uma chave fixa, k, é equivalente realizar operações no plaintext antes de cifrar ou no ciphertext depois de cifrar, desta forma é necessário comutatividade entre a cifragem e algumas operações de de precissamento de dados. 