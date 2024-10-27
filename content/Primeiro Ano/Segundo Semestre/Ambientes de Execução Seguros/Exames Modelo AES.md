## Questões que podem aparecer na frequência 1 (p/ temática)

### Conceitos de ambiente de execução seguro

**1. Qual o mecanismo fundamental de uma TCB (*Trusted Computing Base*)?**

R: É a existência de um *hardware* e *software* que permitem concretizar um monitor de controlos de acesso, o qual é responsável por garantir a segurança do sistema.

**2. Explique como é que os sistemas operativos (software) exploram funcionalidades do hardware, nomeadamente CPU, para concretizar o monitor de controlos de acesso.**

R: Os sistemas operativos exploram funcionalidades do hardware, nomeadamente CPU, para concretizar o monitor de controlos de acesso através de mecanismos de segurança do CPU, como anéis de proteção, virtualização, interrupts e exceções, e *Trusted Execution Environment* (TEE).

**3. Considere o conceito de atestação (certificação) remota realizada através de um TPM (*Trusted Platform Module*). Indique o que se consegue provar com este mecanismo.**

R: Permite provar a integridade e confiança do sistema para terceiros, fazendo isto logo no processo de boot do sistema.

**4. Explique por que razão um arranque seguro (*secure bootstrap*) é vital para evitar potenciais corrupções da TCB concretizada num sistema operativo.**

R: Porque garante que é carregado (boot) de forma segura, pois a integridade do hardware do sistema e a autenticidade do sistema operativo é verificada, evitando assim ataques como *bootkits*, *rootkits*, *malware*, etc.

### Segurança em sistemas operativos

**1. Os processos em Linux possuem um effective UID e um real UID, mesmo para o GID. Explique por que razão os processos têm estes dois UID's.**

R: Esta rotulagem é feita para controlo de acesso a recursos. O real UID representa o ID do utilizador que iniciou o processo, enquanto o effective UID representa o ID do utilizador ao qual o processo está a correr. 

Isto permite ao processo aceder a determinados recursos para efetuar uma operação, mesmo que o utilizador que iniciou o processo não tenha permissões para tal (e.g. comando `passwd`).

**2. Os sistemas Unix permitem a proteção de informação através de ACL's (*Access Control Lists*) e através de *capabilities*. Explique a diferença entre estes dois mecanismos e indique uma situação em que um é mais adequado que o outro.**

R: As ACL's são uma lista de permissões associada a um objeto, enquanto as *capabilities* são tokens individuais que representam permissões específicas que um processo possa ter. 

As ACL's podem ser mais adequadas em sistemas de arquivos compartilhados onde multiplos utilizadores podem aceder a um mesmo objeto mas com diferentes permissões, enquanto as *capabilities* são mais adequadas para sistemas onde os processos têm permissões específicas e não necessitam de permissões adicionais.

**3. Uma ACL (*Access Control List*) é uma lista de permissões associada a um objeto, e pode ser de dois tipos. Indique quais são esses tipos e explique a diferença entre eles.**

R: Os dois tipos de ACL são *discretionary* e *mandatory*. A *mandatory* é definida pelo sistema e não pode ser alterada pelo utilizador, enquanto a *discretionary* é definida pelo dono do objeto e pode ser alterada pelo mesmo.

**4. Considere o mecanismo Set-UID em sistemas Unix. Explique como é o seu funcionamento.**

R: O Set-UID é um mecanismo que permite a um utilizador executar um programa com as permissões do dono do programa. Isto é feito através da definição do bit Set-UID no ficheiro executável. Quando o programa é executado, o effective UID do processo é alterado para o UID do dono do programa.

(Bonus: Qual é a sua utilidade?)

O Set-UID é útil para permitir que um utilizador execute um programa que necessita de permissões elevadas, sem ter de dar permissões elevadas ao utilizador.

**5. O mecanismo de chroot permite a execução de um processo numa diretoria diferente da diretoria raiz. Explique como é que este mecanismo pode ser usado para reduzir a visibilidade de um processo.**

R: O mecanismo de chroot pode ser usado para reduzir a visibilidade de um processo, pois limita o acesso/visibilidade a outras partes do sistema, permitindo que um processo seja executado numa diretoria diferente da diretoria raiz.

## Virtualização

**1. O suporte para a virtualização diretamente sobre o hardware (*bare-metal*) e não sobre um sistema operativo (*hosted*) obrigou a introdução de novos niveis de proteção no CPU. Indique quais e explique porquê.**

R: Os níveis de proteção no CPU são representados por os *protection rings*, estes são o modo do CPU implementar os níveis de privilégios e proteção do sistema, onde 0 é o nível mais privilegiado e 3 é o nível menos privilegiado. 

Com o suporte para a virtualização *bare-metal*, foi necessário introduzir um novo nível de proteção, o *Ring -1*, para permitir ao *hypervisor* a execução de código seguro em modo mais privilegiado que o OS hospedeiro. Este novo nível de proteção encontra-se dentro do *Ring 0*.

**2. A Virtualização pode ser feita através de diversos modos de operação. Enumere e explique sucintamente cada um deles.**

R: Existem os seguintes modos de virtualização:
- real mode: modo utilizado ao arrancar ou após um reset do processador, onde o processador opera em modo de 16 bits e sem proteção de memória.
- protected mode (aneis 0-3): modo utilizado pelos sistemas operativos modernos, onde o processador opera em modo de 32 bits e com proteção de memória.
- hypervisor mode (anel -1): modo utilizado pelos *hypervisors* para controlar a execução de máquinas virtuais.
- system management mode (anel -2): "god" mode do processador, onde o processador executa código de baixo nível para controlar o hardware.

**3. O mecanismo de memória virtual é vital para a virtualização. Explique porquê.**

R: O mecanismo de memória virtual permite ao sistema operativo fornecer a software a ilusão de acesso a uma grande quantidade de memória principal contígua, quando na verdade essa memória pode estar fragmentada e pode ser armazenada tanto na RAM quanto em dispositivos de armazenamento secundário, como discos rígidos. 

Isto é vital para a virtualização, pois permite o isolamento e gestão de recursos, evitando conflitos de endereços entre sistemas operativos e permite alocação dinâmica de memória.

## Intel SGX

**1. Explique o que é o Intel SGX e qual a sua utilidade.**

R: O Intel SGX é uma tecnologia que permite a criação de enclaves, que são regiões de memória protegidas que são isoladas do resto do sistema. A sua utilidade é garantir a confidencialidade e integridade do código e dados sensíveis, mesmo em ambientes não confiáveis.

**2. Explique a diferença entre `OCALL` e `ECALL` no contexto do Intel SGX.**

R: Durante o fluxo de execução de um enclave, o `OCALL` é usado para transferir código/memória para fora do enclave, enquanto o `ECALL` é usado para transferir código/memória para dentro do enclave.

**3. Ao longo do ciclo de vida de um enclave, é necessário realizar várias operações. Indique quais são essas operações e explique a sua utilidade.**

R: Durante o ciclo de vida de um enclave, são realizadas as seguintes operações:

1. **Creation:** Criação do enclave.
2. **Loading:** Carregamento do código do enclave.
3. **Initialization:** Inicialização do enclave.
4. **Enter/Exit the Enclave:** Fluxo de execução dentro e fora do enclave.
5. **Teardown:** Remoção do enclave.

**4. Um enclave SGX protege a execução de código da observação por outras tarefas que executem no mesmo processador, independentemente do seu nível de privilégio (*protection ring*). Explique como é que isto é possível.**

R: O enclave SGX tem a capacidade de proteger a execução de código da observação por outras tarefas que executem no mesmo processador, pois os conteúdos do enclave (armazenados na DRAM) são isolados do resto do sistema, sendo cifrados usando uma chave de cifra gerada aleatoriamente após cada reinício do processador. A sua integridade também é verificada através de uma assinatura digital feita ao código do enclave.

## ARM TrustZone

**1. O que é o ARM TrustZone e qual a sua utilidade?**

R: O ARM TrustZone é uma tecnologia que permite a execução de código seguro em *hardware* ARM. Permite a execução de dois sistemas em paralelo, um *Rich* OS (não seguro) e um *Secure* OS (seguro), isolados entre si.

**2. O TrustZone introduz um novo *exception level* no CPU ARM. Explique a sua utilidade.**

R: O TrustZone introduz na sua arquitetura o *exception level* 3 que contém o *Secure Monitor*. Este tem como função gerir a troca entre os mundos *Secure* e *Non-Secure*, permitindo a execução de código seguro e aceder a recursos restritos ao *Secure* OS.

**3. A arquitetura ARM TrustZone permite executar sobre o mesmo CPU (ARM) dois sistemas isolados: *Rich* OS (não seguro) e *Secure* OS (seguro). Explique de que forma os dois interagem.**

R: Os dois sistemas interagem entre si via chamadas ao sistema, onde o *Rich* OS pode chamar o *Secure* OS para executar código seguro e aceder a recursos que estão restritos ao mesmo, através de SMCs (*Secure Monitor Calls*) implementadas nos *drivers* do *Rich* OS. Esta troca entre mundos é feita através da manipulação do bit NS (*Non-Secure*) no registo do controlador SCR (*Secure Configuration Register*).

# Exame 29 de junho 2022

4. Considere os espaços de nomes do Linux (Linux namespaces), nomeadamente o de processos. Explique de que forma o mesmo pode ser usado como mecanismo de segurança.

R: O recurso namespaces, permite isolar e separar recursos do sistema para diferentes processos, de modo que cada conjunto de processos possa operar como se estivesse num ambiente isolado.

5. Explique, de uma forma sucinta mas objetiva, o que distingue uma contentor LXC de uma máquina virtual executada sobre um determinado sistema operativo.

R: Ao contrário da máquina virtual, o LXC não necessita de emular hardware, o que o torna mais leve e mais rápido. O container LXC partilha o mesmo kernel do host, enquanto a máquina virtual tem o seu próprio kernel.

6. Explique que tipo de controlo se consegue realizar com o mecanismo AppArmor.

R: Através do AppArmor é possível definir políticas de segurança para aplicações, limitando o acesso a determinados recursos do sistema, como ficheiros, diretórios, sockets, etc.

7. Certas aplicações podem ter interesse em descobrir se estão a executar num ambiente suportado por uma máquina virtual. Explique de que forma podem fazer essa descoberta.

R: Uma aplicação pode verificar se está a executar num ambiente suportado por uma máquina virtual, procurando por hardware virtualizado, como por exemplo, a presença de dispositivos virtuais, ou através de chamadas ao sistema que retornam informações sobre o ambiente de execução.

11. Explique como funcionava o modelo de secure boot proposto no âmbito do AEGIS (não precisa de referir o processo de recuperação).

R: O AEGIS consiste na verificação de integridade do sistema, no momento do arranque. Isto é feito, construindo uma cadeia de verificação de integridade, desde o momento de ligar o sistema até à transferência final de controlo para o sistema operativo. Verificações são feitas através da correspondência de hashes criptográficos calculados com assinaturas digitais armazenadas.

12. Explique os princípios fundamentais para a atestação do arranque de um sistema computacional.

R:

- **Chain-of-Trust**
  - SRT1: Inicialização de uma cadeia de confiança desde o primeiro código executado na UEFI/BIOS até carregar o OS. É feito o hash de cada componente antes de sua execução,garantindo que o código executado é de confiança .
  - DRT1: chain of trust que pode ser inicializada a qualquer momento após o arranque inicial
- **PCR**: utilizados durante medições a componentes durante o processo de arranque
  - Não podem ser apagados/definidos e os seus valores são usados para guardar hashes
  - Podem verificar o estado do sistema depois do arranque Atestação Remota + permite verificar de forma remota se um PC arrancou de forma segura e o estado atual é continua. UEFI Secure Boot-processo de validação do firmware que define como a plataforma firmware valida os certificados
- **Recuperação**: Se a verificação de integridade falhar, o processo consegue recuperar um modulo de substituição.

13. Segundo a TCPA (Trusted Computing Platform Alliance), há dois modos de arranque (boot): autenticado/confiável (authenticated/trusted) e seguro (secure). Explique as diferenças entre ambos.  

R: No caso do **secure boot**, ele aplica políticas durante o processo de inicialização, garantido que apenas software confiável seja executado. O arranque é interrompido se um valor de PCR não corresponder ao esperado. No caso do **authenticated boot**, ele verifica cada componente do processo de inicialização em relação a valores conhecidos, mas não aplica políticas, apenas registando os valores de PCR. Os valores de PCR são armazenados para posterior verificação.

14. Explique em que consiste um arranque sob avaliação (measured boot) dos sistemas operativos Windows.

R: Este processo de measured boot permite que as entidades consultem o TPM após a conclusão do processo e verifiquem se os valores na stack do PCR correspondem aos valores esperados, pré-calculados com versões "conhecidas" das várias camadas.

15. Um arranque seguro via UEFI (UEFI secure boot) garante a correção dos módulos de firmware carregados durante o arranque de um sistema através de registos colocados em bases de dados locais, sendo uma delas a dbx (blacklist). Explique para que serve e como é usada esta base de dados. Como funcionam?

R: Esta base de dados contém hashes de módulos de firmware que foram considerados inseguros ou comprometidos. Durante o arranque, o UEFI verifica se os módulos de firmware carregados correspondem a algum dos hashes na base de dados. Se corresponderem, o arranque é interrompido.

16. O mecanismo de hash extends (dispersões extendidas) é usado pelo TPM como base para atestação. Explique:
a. Como funcionam?
b. Por que razão são uteis para atestação?

R:

a. No mecanismo de hash extends, o TPM pega o valor atual do PCR, concatena com o valor do novo o valor de hash e aplica uma função hash ao resultado concatenado, da seguinte forma: `PCR[n] = hash(PCR[n] || hash(novo))`.

b. Este mecanismo é útil para atestação, pois permite que entidades externas verifiquem se o sistema foi inicializado de forma segura, verificando se os valores de PCR correspondem aos valores esperados. Além disso, permite uma melhor auditabilidade do processo de arranque.

17. Cada uma das 4 hierarquias do TPM possui uma árvore de chaves, as quais começam em chaves primárias. Explique o processo de criação destas chaves.

R:  As chaves primárias são geradas através de *hierarchy seeds* e uma *public template* (conjunto de parâmetros que define as características da chave a ser criada). Estas chaves são usadas para criar chaves secundárias (*storage keys*) que são usadas para criar chaves de utilizador. As chaves de utilizador são criadas a partir de uma *public template* e uma *storage key*.

1. Um TPM tem a capacidade de exportar dados gerados dentro de si de tal forma que, mais tarde, consegue verificar que foram por si gerados aquando de uma futura importação. Explique como.

R: O processo é feito da seguinte maneira:

1. **Criação de chaves e assinaturas**: o TPM gera chaves internamente que podem ser usadas para assinar dados internos. Estas assinaturas provam que os dados foram gerados dentro do TPh e não foram alterados.
2. **Exportação de chaves públicas**: chaves geradas pelo TPR podem ser exportadas de forma desprotegida. Isto permite que entidades externas possam verificar assinaturas feitas pelo TPR.
3. **Importação e Verificação**: Os dados previamente exportados podem voltar a ser importados pelo TPM. Quando são reimportados , o TPM usa as chaves internas para verificar a assinatura dos dados

19. O TPM permite assinar (com uma chave privada conhecida apenas por si) dados calculados internamente por si ou dados fornecidos a partir do exterior. Como é que o TPM consegue evitar que os dados fornecidos a partir do exterior simulem dados calculados internamente?

R: O TPM consegue evitar que os dados fornecidos a partir do exterior simulem dados calculados internamente, através da utilização de chaves internas que são usadas para assinar os dados. Estas chaves são geradas internamente e não podem ser exportadas. Assim, apenas o TPM pode assinar os dados com estas chaves, garantindo que os dados foram gerados internamente. Além disso, o TPM pode verificar a integridade dos dados fornecidos a partir do exterior, através do PCR.

20.  Os smartcards possuem uma interface de comunicação mestre-escravo, baseada em mensagens designadas por APDU (Application Protocol Data Unit). Estes APDU permite manipular entidades do smartcard, como é o caso do seu sistema de ficheiros. Porém, tem de haver uma sincronização no acesso concorrente de várias aplicações a um dado smartcard. Explique:

a. Por que razão tal é necessário?
b. Como é que tal é feito?

R: 

a. A sincronização no acesso concorrente de várias aplicações a um dado smartcard é necessária para garantir a integridade dos dados e evitar *race conditions* que possam corromper o sistema de ficheiros do smartcard.

b. Isto é feito através de um mecanismo de *locks* que garantem que apenas uma aplicação pode aceder ao smartcard de cada vez. Quando uma aplicação acede ao smartcard, ela adquire um *lock* que impede que outras aplicações acedam ao smartcard. Quando a aplicação termina de aceder ao smartcard, o *lock* é libertado e outras aplicações podem aceder ao smartcard, isto normalmente é implementado em conjunto com o middleware do smartcard.