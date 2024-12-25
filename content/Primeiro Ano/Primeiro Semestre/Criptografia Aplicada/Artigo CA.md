# Resumo do artigo

O objetivo da cifragem é assegurar a confidencialidade da informação durante a comunicação e processo de armazenamento. 

Os esquemas de cifragem homomórfica, surgiu como uma solução para a delegação de computação, que permite que sejam feitas operações sobre os textos cifrados, sem que seja necessário decifrar o texto.

Desde o aparecimento do primeiro esquema de cifragem homomórfica, em 1978, muitos esquemas foram propostos, mas nenhum deles foi implementado na prática, devido a problemas de segurança e performance, utilizando aplicações como, a partilha de segredos, zero-knowledge proofs, multiparty computation, mix-nets, threshold, entre muitos outros.

## Notação
**l(x):** o número de bits que constitui a expansão binária de x.
**Zn:** Os inteiros de modulo n.
**Z∗n:** Os inteiros de modulo n que são coprimos com n.

## Básicos de Criptografia
De acordo com o principio de Kerckhoffs, a segurança de um sistema de criptografia não deve depender do segredo do algoritmo, mas sim da chave.

### Tipos de cifras
Existem dois tipos de cifras: cifras simétricas e cifras assimétricas.

| Esquema de cifra    | Chave(s) | Performance | Tipo(s) de cifra  |
| ------------------- | -------- | ----------- | ----------------- |
| Cifras simétricas   | 1        | Ótima       | Blocos e Continua |
| Cifras assimétricas | 2        | Ruim        | Blocos            |

#### Cifras simétricas
- Este tipo de cifra não pode ser usado para a comunicação entre duas partes que não partilham uma chave secreta;
- Normalmente, são usadas para cifrar informação de grandes dimensões;

#### Cifras assimétricas
- Estas baseiam-se em problemas matemáticos difíceis, como a fatorização de inteiros e o logaritmo discreto, para garantir a segurança, tornando-as mais lentas que as cifras simétricas;
- Duas das mais conehecidas são a RSA e a ElGamal;
- Normalmente, são usadas para cifrar informação de pequenas dimensões.

Por exemplo, a cifra por blocos AES é, por norma, 100x mais rápida que a RSA na cifragem e 2000x mais rápida na decifragem.

### Performance

Por isso, na prática, é normal usar-se uma cifra simétrica para cifrar a mensagem e uma cifra assimétrica para cifrar a chave da cifra simétrica, combinando assim a eficiência de cifras simétricas com as funcionalidades de cifras assimétricas.

### Problemas de segurança

No artigo publicado por Shannon, ele introduziu a noção de **segredo perfeito/segurança incondicional**, que caracteriza os esquemas de cifragem para os quais o conhecimento de um texto cifrado **não dá nenhuma informação** sobre o texto limpo correspondente ou sobre a chave. 

Ele provou que o **One-time pad** é (perfeitamente) seguro sob algumas condições, sendo estas:
- A chave é gerada aleatoriamente e é tão longa (ou maior) quanto a mensagem.
- A chave é usada apenas uma vez.

Nota: **Excluindo** o One-time pad, **nenhum outro esquema de cifragem** (simétrica ou assimétrica) é seguro, e toda a segurança de um esquema de cifragem depende do **poder computacional** do adversário (no caso das cifras assimétricas, depende na solução de problemas matemáticos difíceis).

Muitas das provas de segurança são realizadas no modelo de segurança de **oráculo aleatório**, que é um modelo de segurança que diz que um esquema de cifragem é seguro se o adversário não consegue distinguir entre dois textos cifrados, mesmo que ele conheça a função de cifragem.

Uma avaliação empirica é realizada em qualquer caso, e novas cifras simetricas  e assimetricas são avaliadas de acordo com os ataques publicados.


### Como escolher o esquema de cifra correto?
O esquema correto é aquele que se adapta da melhor forma às suas restrições. Por restrições, pode-se dizer restrições de tempo, memória, segurança, etc.
Os dois primeiros critérios são muito importantes para arquiteturas bastante restritas(PDAs, cartão de cidadão, etc).
Um outro ponto a ter é uso frequente da mesma cifra, pois em caso de falha, o hacker terá acesso total ao sistema.

### Cifragem probabilística
Os sistemas de cifragem mais conhecidos são determinísticos, ou seja, a mesma mensagem com a mesma chave produz sempre o mesmo texto cifrado(RSA).

Este facto pode levar a alguns inconvenientes, por exemplo:
- Quando usado um esquema de cifragem determinístico, o adversário pode saber se duas mensagens são iguais, mesmo que não saiba o conteúdo das mensagens.
- Pode ser fácil o calculo de informações parciais sobre o texto limpo.
- Quando se usa um esquema de cifragem determinístico, o adversário pode saber se duas mensagens são iguais, mesmo que não saiba o conteúdo das mensagens.

Então, na prática, é preferivel usar um **esquema de cifragem probabilístico**, seja através de geradores pseudo-aleatórios ou outro processo que produza algum tipo de aleatoriedade.

Deste modo, novos esquemas de cifragem, baseados em aleatoriedade. Um efeito direto dessa necessidade de serem probabilísticos é a **expansão'**: devido à possibilidade de múltiplos textos cifrados para um texto simples, o número de textos cifrados é maior que o número de textos simples possíveis. Isso resulta em textos cifrados que devem ser mais longos que os textos simples, estabelecendo a relação chamada de **expansão**, que é a proporção entre o comprimento dos textos cifrados e dos textos simples, medido em bits.

## Cifragem Homomórfica

Este tipo de cifragem permite que sejam feitas operações sobre os textos cifrados, sem que seja necessário decifrar o texto.

A definição formal de cifragem homomórfica é a seguinte:

> Seja M um espaço de mensagens, C um espaço de textos cifrados e E um algoritmo de cifragem. 
> Diz-se que E é homomórfico se existir uma função f tal que para todo m1 e m2 em M, E(m1) (0) E(m2) = E(m1 (0) m2), sem nenhuma decifragem intermediária.

> Nota: (0) é uma operação aplicada sobre o espaço de mensagens, e o = simboliza 'pode ser computado através de'

Caso (M, (0)M) e (C, (0)C) sejam grupos, então nós temos um *grupo homomórfico*. Nós dizemos que o esquema é *aditivamente homomórfico* se considerarmos a operação de grupo como a adição, e *multiplicativamente homomórfico* se considerarmos a operação de grupo como a multiplicação.

É de grande interesse a implementação desta propriedade não só para um operador, mas para dois ao mesmo tempo, também denominado de *[homoforismo de anéis](https://pt.wikipedia.org/wiki/Homomorfismo_de_an%C3%A9is)*.

> Tal que para todo o m1 e m2 em M:
> 
> E(m1) + E(m2) = E(m1 + m2),
> 
> E(m1) * E(m2) = E(m1 * m2).

Estas definições significam que para uma chave fixa, k, é equivalente realizar operações no plaintext antes de cifrar ou no ciphertext depois de cifrar, desta forma é necessário comutatividade entre a cifragem e algumas operações de de precissamento de dados. 

### Novas considerações a nível de segurança
A cifragem probabilistica foi introduzida sobre a promessa de melhorar a **segurança**. 

A **segurança de semântica**, conceito normalmente relacionado a sistemas de criptografia de chave pública acontece caso o conhecimento de um texto cifrado não dê nenhuma informação sobre o texto limpo correspondente, para um adversário com poder computacionado restrito.

Junto deste requisito, **segurança polinomial** foi também introduzida, que diz se um adversário escolher dois textos limpos, e nós escolhemos secretamente de forma aleatória um dos dois textos para cifrar, o adversário não consegue adivinhar qual dos dois textos foi cifrado, obtendo na sua escolha uma probabilidade de 0,5 + ε de acertar.

Com esta equivalência, é fácil afirmar que um esquema de cifragem assimétrica determinística **não pode ser** semanticamente seguro, uma vez que não pode ser **indistinguível**: o adversário conhece a função de cifragem, e assim pode calcular o único texto cifrado correspondente a cada texto limpo.

Mas com uma cifra assimétrica, o adversário sabe todo o processo de cifragem, E, envolvendo tanto a função de cifragem como a chave de cifra, podendo então computar qualquer par (m, E(m)).

IND-CPA (indistinguibilidade de texto cifrado sob ataque de texto cifrado) é um modelo de segurança que diz que um esquema de cifragem é seguro se o adversário não consegue distinguir entre dois textos cifrados, mesmo que ele conheça a função de cifragem.

IND-CCA1 (indistinguibilidade de texto cifrado sob ataque de texto cifrado e escolhido) é um modelo de segurança que diz que um esquema de cifragem é seguro se o adversário não consegue distinguir entre dois textos cifrados, mesmo que ele conheça a função de cifragem e possa escolher o texto limpo que quer cifrar.

IND-CCA2 (indistinguibilidade de texto cifrado sob ataque de texto cifrado e adaptativo) é um modelo de segurança que diz que um esquema de cifragem é seguro se o adversário não consegue distinguir entre dois textos cifrados, mesmo que ele conheça a função de cifragem e possa escolher o texto limpo que quer cifrar, e pode também escolher o texto cifrado que quer decifrar. Este é considerado o requisito de segurança mais forte, tornando-o não maniável.

Um outro requisito de segurança, é a não maneabilidade, isto é a impossibilidade de um adversário alterar um texto cifrado de forma a que o texto limpo decifrado seja alterado de uma forma previsível.

Enfantizado que na cifra homómorfico, esta não pode ter a propriedade de não maneabilidade, uma vez que o adversário pode alterar o texto cifrado, e depois decifrar o texto alterado, obtendo assim o texto limpo alterado.

Por ultimo, foi provado que esquemas de cifra homomórfica deterministica que se basea apenas na operação soma, não é seguro.


## Homomorphic Encryption: State os the Art

Tanto o esquema de cifragem RSA como o ElGamal são homomórficos multiplicativos. Contudo, o problema com o RSA original, por ser determinístico, é que não consegue alcançar um nível de segurança de IND-CPA (que é o nível mais alto de segurança para esquemas homomórficos). Em contrapartida, o ElGamal oferece um melhor nível de segurança para um esquema de cifragem homomórfica, sendo comprovado como IND-CPA. Também é interessante notar que uma variante aditiva homomórfica do ElGamal foi proposta R. Cramer, R. Gennaro, and B. Schoenmakers, “A secure and optimally efficient multiauthority election scheme,”.

1. **Cifragem**:
   - Bob quer enviar a mensagem \( m \) para Alice de forma segura.
   - Ele seleciona aleatoriamente um número \( k \) do conjunto \( Z_q \), onde \( q \) é um número primo grande.
   - Utilizando a fórmula de cifragem \( (c_1, c_2) = (g^k, G^m \cdot Y_A^k) \):
     - \( c_1 \) é calculado como \( g^k \), representando uma parte aleatória da cifra.
     - \( c_2 \) é obtido através de \( G^m \cdot Y_A^k \):
       - \( G^m \) representa a mensagem \( m \) elevada ao poder de \( G \), onde \( G \) é um elemento do grupo.
       - \( Y_A^k \) é o elemento \( Y_A \) (parte da chave pública de Alice) elevado ao poder de \( k \).
       - \( G^m \cdot Y_A^k \) é a combinação desses dois valores multiplicados no grupo.

2. **Decifragem**:
   - Para decifrar a mensagem e obter \( m \), Alice utiliza sua chave privada \( a \).
   - Ela calcula \( G^m \) usando \( c_1 \) e sua chave privada \( a \): 
   \( G^m = c_2 \. (c_1^a)^{-1} \).
   - Este passo é desafiador, pois envolve calcular a raiz discreta em um grupo, que é um problema difícil de resolver sem a chave privada correspondente.

3. **Dificuldade na Decifragem**:
   - O último passo de decifragem envolvendo o cálculo de \( m \) a partir de \( G^m \) é computacionalmente difícil e não possui um método direto.
   - Este processo requer encontrar a raiz discreta de \( G^m \) em relação a \( G \) no grupo, o que é difícil sem a chave privada correspondente.
   - Resolver esse problema geralmente requer métodos como a busca exaustiva, o que torna o processo de recuperação de \( m \) extremamente demorado.

Portanto, enquanto a cifragem no esquema ElGamal aditivo homomórfico é computacionalmente eficiente, a decifragem sem a chave privada adequada é um desafio, exigindo métodos computacionalmente intensivos como a busca exaustiva para recuperar a mensagem original.

É amplamente conhecido que a construção do ElGamal funciona para qualquer família de grupos onde se considera o problema do logaritmo discreto como intratável, tal como, por exemplo, na configuração que utiliza curvas elípticas.

Assim sendo, o ElGamal e as suas variantes são considerados candidatos muito interessantes para esquemas de cifragem homomórfica realistas. Um outro é o esquema de Paillier e as suas variantes são conhecidos pela sua eficiência, mas também porque, tal como o ElGamal, alcançam o mais alto nível de segurança para esquemas de cifragem homomórfica.

### História da familia dos esquemas de cifragem Homomórficos

A primeira publicação de um esquema probabilístico de criptografia de chave pública, proposto por Goldwasser e Micali, foi o primeiro esquema de criptografia probabilístico que alcançou o nível de segurança de IND-CPA. Este esquema é baseado no problema do logaritmo discreto, e é considerado um dos esquemas de criptografia mais eficientes.(Mostrar figura 4)

Vantagens do esquema de Goldwasser-Micali:
- É um esquema de criptografia probabilístico que alcança o nível de segurança de IND-CPA.
- É baseado no problema do logaritmo discreto.
- É considerado um dos esquemas de criptografia mais eficientes.
- A sua cifragem é pode ser realizada em ϑ(〖l(p)〗^2).

Desvantagens do esquema de Goldwasser-Micali:
- Não é homomórfico.
- Não é eficiente para criptografar mensagens de tamanho grande, pois o tamanho da mensagem é limitado pelo tamanho do grupo, isto é a sua expansão irá se tornar muito grande, um unico bit do plaintext é cifrado num inteiro de modulo n, que é l(n) bits.

Apresentado de um outro ponto de vista GM:

O esquema Goldwasser-Micali (GM) de criptografia de chave pública é baseado na ideia de dividir um subconjunto bem escolhido de inteiros módulo \( n \) em duas partes secretas: \( M_0 \) e \( M_1 \). Durante a criptografia, um elemento aleatório é selecionado de \( M_b \) para criptografar o bit \( b \), e durante a decifragem, é possível determinar em qual parte o elemento aleatório está contido. O ponto crucial está na seleção e partição desse subconjunto.

O esquema GM utiliza a teoria dos grupos da seguinte maneira: o subconjunto consiste no grupo \( G \) de inteiros invertíveis módulo \( n \) com um símbolo de Jacobi igual a 1 em relação a \( n \). A partição é gerada por outro grupo \( H \subset G \), composto pelos elementos invertíveis módulo \( n \) com um símbolo de Jacobi igual a 1 em relação a um fator fixo de \( n \); com essas configurações, é possível dividir \( G \) em duas partes: \( H \) e \( G \backslash H \).

As generalizações do Goldwasser-Micali exploram esses dois grupos; procuram encontrar dois grupos \( G \) e \( H \) de tal forma que \( G \) possa ser dividido em mais do que \( k = 2 \) partes.

O cerne da ideia reside na manipulação desses grupos para permitir uma divisão mais ampla dos elementos, e essas generalizações têm como objetivo encontrar configurações onde a divisão do grupo \( G \) seja em mais de duas partes.

(i) **Benaloh**:
O esquema de Benaloh é projetado para lidar com inputs de \(k\) bits. Durante a cifragem, um número aleatório \(r\) é escolhido e é realizada a operação \(c = g^{mrk} \mod n\), onde \(g\) é um gerador de um grupo \(G\) e \(n\) é um número inteiro. No entanto, a decifragem apresenta um custo computacional considerável, estimado em \(O(\sqrt{k} \cdot \log{k})\). Isso limita a sua eficiência para valores pequenos de \(k\).

(ii) **Naccache-Stern**:
Uma evolução do esquema Benaloh, o Naccache-Stern permite um \(k\) maior e reduz o custo de decifragem para \(O(n^5 \cdot \log{n})\), mas ainda mantém restrições específicas para certos parâmetros. Ele oferece melhorias significativas em termos de eficiência computacional em comparação com o seu antecessor.

(iii) **Okamoto-Uchiyama**:
Este esquema altera o grupo base \(G\) para \(Z^*_{p^2}\), onde \(p\) é um número primo. Procura reduzir a expansão para 3, mas as suas limitações estão associadas a condições específicas de escolha dos números \(p\) e \(q\). Isso restringe a sua aplicabilidade em certos cenários.

(iv) **Esquema de Paillier**:
O esquema de Paillier reduz a expansão para 2 usando \(Z^*_{n^2}\) como grupo base, o que é uma melhoria significativa em relação a esquemas anteriores. No entanto, o custo de decifragem ainda é um desafio, com complexidade \(O(\log^2{n})\). Isso pode limitar a sua eficácia em sistemas com altas demandas computacionais.

(v) **Damgård-Jurik**:
Esta variante generaliza para \(Z^*_{ns+1}\), permitindo uma redução na expansão conforme \(s\) aumenta. No entanto, o custo computacional desta abordagem pode ser consideravelmente maior do que o do esquema de Paillier, especialmente em cenários onde a segurança e a eficiência são fatores críticos.

(vi) **Galbraith**:
Adaptado para curvas elípticas, o esquema de Galbraith apresenta um custo computacional variável. Dependendo dos parâmetros escolhidos, pode ter custos computacionais superiores ou inferiores a outros esquemas, oferecendo um equilíbrio entre eficiência e segurança.

(vii) **Castagnos**:
Explorando campos quadráticos, o esquema de Castagnos mantém uma expansão de 3, mas com custos computacionais razoáveis. Ele mantém uma relação equilibrada entre eficiência e segurança, embora a sua expansão possa ser considerada maior que a de alguns outros esquemas.

(viii) **Amálgama ElGamal-Paillier**:
Funde aspectos do ElGamal e do Paillier, contendo as vantagens de ambos os esquemas e minimizando as suas desvantagens. 

É importante ter diferentes tipos de esquemas, devido às aplicações e propósitos de segurança. Uma vertente a explorar é projetar esquemas homomórficos que não estão diretamente relacionados aos mesmos problemas matemáticos que ElGamal ou Paillier (e suas variantes), deste modo, pode se considerar artigos recentes que lidam com o emparelhamento de Weil.

- Emparelhamento de Weil: Sugere-se explorar os avanços recentes nesse campo como uma direção promissora para criar esquemas homomórficos diferentes dos tradicionais, como ElGamal ou Paillier. Há interesse especial na adaptação de esquemas baseados em emparelhamento para criptografia homomórfica, incluindo a proposta de Boneh e Franklin para um esquema de criptografia ID homomórfico.

Outra vertente a explorar seria:
- Criptografia Simétrica e Homomorfia: Destaca-se a dificuldade de alcançar a homomorfia em criptografia simétrica, que geralmente não envolve operadores matemáticos convencionais. Embora poucos esquemas homomórficos simétricos tenham sido propostos, muitos foram quebrados. Uma sugestão mencionada é uma adaptação simplificada do one-time pad usando inteiros modulo n, com considerações sobre sua segurança.

E por fim, uma ultima vertente a explorar seria:
- Criptografia Homomórfica Algébrica: Aponta-se o desafio na concepção de esquemas de criptografia homomórfica algébrica. Existem poucas propostas até o momento, mas todas levantaram preocupações de segurança e eficiência. A conjectura de Boneh e Lipton sugere incertezas sobre a segurança desses tipos de esquemas.
