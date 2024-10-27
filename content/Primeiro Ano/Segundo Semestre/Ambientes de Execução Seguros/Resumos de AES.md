## Modelo de segurança do sistema operativo

O modelo de segurança do sistema operativo é composto por o seguinte conjunto de entidades (objetos) geridos pelo Kernel:

- *Processos*: Entidade que executa um programa;
- *Identificadores do Utilizador (UID)*: Identifica o utilizador;
- *Ficheiros*: Entidade que armazena informação;
- *Canais de comunicação*: Entidade que permite a comunicação entre processos (sockets, pipes, etc.);

### User ID (UID)

O UID é um identificador numérico único que identifica um utilizador no sistema atribuído durante o processo de autenticação.

Existem dois tipos de UID:
- *Real UID*: Identifica o utilizador que executou o processo;
- *Effective UID*: Identifica o utilizador que tem permissões para executar o processo.

### Group ID (GID)

O GID é um identificador numérico único que identifica um grupo de utilizadores no sistema.

**Nota:** Um utilizador pode pertencer a vários grupos.

## Controlo de acesso

É composto por:
- *Sujeitos*: Entidades que executam operações sobre objetos;
- *Monitor de acesso*: Entidade que verifica se o sujeito tem permissão para aceder ao objeto;
- *Objetos*: Entidades que são acedidas pelos sujeitos.

Obs.: O Kernel é um monitor de acesso.

### ACL (*Access Control List*)

É uma lista que define as permissões de acesso a um objeto.

Pode ser:
- *Discretionary*: O dono do objeto pode definir as permissões de acesso;
- *Mandatory*: As permissões de acesso são definidas pelo sistema.

Em Unix, as permissões de acesso são definidas por:
- *Read* (R): Permite a leitura/listagem do ficheiro;
- *Write* (W): Permite a escrita/remoção no ficheiro;
- *Execute* (X): Permite a execução do ficheiro.

Em Unix, também pode ser feita proteção usando *special protection bits*:
- *Set-UID*: Permite que o programa seja executado com os privilégios do dono do ficheiro;
- *Set-GID*: Permite que o programa seja executado com os privilégios do grupo do ficheiro;
- *Sticky bit*: Permite que apenas o dono do ficheiro possa remover o ficheiro.

### Capabilities

É um conjunto de permissões que um sujeito tem sobre um objeto.

## Windows NFTS file protection

O Windows NFTS (*New Technology File System*) é um sistema de ficheiros que permite a proteção de ficheiros e diretórios.

## Elevação de privilégios

### Mecanismo usando *Set-UID*/ *Set-GID*

Caso o *Set-UID*/ *Set-GID* esteja ativado, o programa será executado num processo com o mesmo ID do dono/grupo do ficheiro. 

É usado para mudar o UID de um processo durante a execução de um programa armazenado no ficheiro Set-UID.

Isto permite a utilizadores que não têm permissões de administrador executar programas com privilégios de administrador num ambiente controlado.

Nota: O *Real UID* não é alterado, apenas o *Effective UID*.

### Mecanismo usando *sudo*

O comando `sudo` permite que um utilizador execute um comando com privilégios de administrador, mesmo que o utilizador não seja *root*. Para o executar o utilizador pode ser sujeito a autenticação.

## Redução de privilégios

Permite reduzir a visibilidade de um determinado processo.

### *Chroot*

O comando `chroot` significa *change root* e permite que **um processo seja executado numa diretoria diferente da diretoria raiz**, limitando o acesso/visibilidade a outras partes do sistema.

Nota: Embora este mecanismo permita uma forma de isolamento, **não é seguro** pois existem formas de *bypass*.

### *Chroot Jail*

É um ambiente de execução limitado que permite a execução de um processo numa diretoria diferente da diretoria raiz.

## Login no Linux

Não é uma operação do Kernel.

O processo de login é composto por:
 - pcb;
 - UID;
 - GID;
 - *Home directory*;

### Ficheiros de configuração

O caminho `/etc/passwd` contém a informação dos **utilizadores do sistema**, como:
- Nome de utilizador;
- UID;
- GID;
- *Home directory*;
- *Shell*.

O caminho `/etc/group` contém a informação dos **grupos do sistema**, como:
- Nome do grupo;
- GID;
- Lista de utilizadores.

O caminho `/etc/shadow` contém a informação das **passwords dos utilizadores do sistema** (em formato *hash*).

### PCB (Process Control Block)

É uma estrutura de dados que contém informação sobre o processo.
## TCB (*Trusted Computing Base*)

O TCB é composto por *hardware*, *software* e procedimentos que são necessários para garantir a segurança do sistema.

Incluí:
- Mecanismos de segurança do CPU:
  - Anéis de proteção
  - Virtualização
  - Interrupts e exceções
  - *Trusted Execution Environment* (TEE)
- Modelo de segurança do sistema operativo:
  - Modelo computacional;
  - Firmware;
  - Permissões de acesso e privilégios;

### Aneis de proteção

Os aneis de proteção são uma forma de implementar a separação entre o *user-mode* e o *supervisor-mode*.

Hoje em dias os processadores têm 4 aneis de proteção:
 - *Ring 0*: Kernel;
 - *Ring 1*: Drivers;
 - *Ring 2*: Sistemas de ficheiros;
 - *Ring 3*: Aplicações.

## TEE (*Trusted Execution Environment*)

É um ambiente de execução seguro que é isolado do sistema operativo normal. O TEE é geralmente implementado em hardware (e.g. ARM TrustZone) e é usado para executar código seguro.

## ARM TrustZone

TrustZone é uma extensão de segurança por *hardware* que o separa em duas zonas distintas, uma **zona segura** e uma **zona normal**. A zona segura é isolada da zona normal e é protegida por hardware, usada para armazenar dados sensíveis e executar código seguro.

## Soc e IP

### Soc (*System on Chip*)

O SoC é um chip que integra todos os componentes de um computador em um único chip. Ele contém um processador, memória, controladores de periféricos, interfaces de comunicação, etc.

Um SoC normalmente contém:
- Processadores;
- IP's;
- Memória (RAM, ROM, etc.);
- Bus de comunicação;

### IP (*Intellectual Property*)

IP é um termo usado para descrever um design de hardware que pode ser licenciado para ser usado num SoC.

## Worlds

O isolamento é atingido através do uso do mesmo CPU em mundos *worlds* (estados).
- *Secure World*: Onde o código seguro é executado (Secure OS).
- *Normal World*: Onde o código normal é executado (Rich OS).

O CPU flag bit NS (*Non-Secure*) é usado para alternar entre os mundos.
- **NS = 0**, *Secure State*
- **NS = 1**, *Non-Secure State*

O acesso ao mundo segundo é feito através de instruções específicas (SMC - *Secure Monitor Call*) feita a partir do Rich OS.

![[Primeiro Ano/Segundo Semestre/Ambientes de Execução Seguros/imgs/image-1.png]]

## Recursos de Hardware protegidos

Os recursos protegidos são apenas acedidos pelo *Secure OS*.

## *Exception Levels*

O `ARMv8-A` define **quatro níveis** de exceção:
- **EL0**: Nível de exceção mais baixo, onde o código de aplicação é executado.
- **EL1**: Onde o código do *kernel* é executado.
- **EL2**: Onde o código de *hypervisor* é executado.
- **EL3**: Onde o código de *secure monitor* é executado (componente de software que controla a transição entre mundos).

## Arquitetura TrustZone

![[Primeiro Ano/Segundo Semestre/Ambientes de Execução Seguros/imgs/image.png]]

### Detalhes da Arquitetura
- 2 MMU's (*Memory Management Units*): indexados por `SCR_EL3.NS` para selecionar o mundo.
- 1 TBL (*Translation Tables*): Mas as entradas contém o valor do bit `NS` para indicar o mundo.
- O *Secure Mode* pode aceder a ambos os mundos.
- 1 *Cache Controller*: mantém o NS bit p/ cada linha de cache.

#### MMU (*Memory Management Unit*)

A MMU é usada para traduzir endereços virtuais em endereços físicos. A MMU é configurada para permitir que o *Secure OS* e o *Normal OS* tenham diferentes espaços de endereçamento.

#### TBL (*Translation Tables*)

As tabelas de tradução são usadas para mapear endereços virtuais em endereços físicos. Cada mundo tem a sua própria tabela de tradução.

#### AXI (*Advanced eXtensible Interface*)

O AXI é um protocolo de comunicação usado para conectar periféricos ao SoC. O AXI é configurado para garantir que os periféricos de um mundo não são acessíveis a partir do outro mundo.

### *TrustZone Controllers*

Estes controladores são usados para configurar a segurança do SoC e o seu registo de controlo é acessível apenas no *Secure World*.

#### *Cache Controllers*

Os controladores de cache são configurados para garantir que os dados de um mundo não são acessíveis a partir do outro mundo.

#### TZASC (*TrustZone Address Space Controller*)

Permite classificação dinâmica de regiões de memória como seguras ou não seguras. 

#### TZMA (*TrustZone Memory Adapter*)

Mantém a classificação de áreas de mesmo do SoC como seguras ou não seguras. 

#### TZPC (*TrustZone Protection Controller*)

Permite a configuração de permissões de acesso a periféricos. 

#### GIC (*Generic Interrupt Controller*)

O GIC é usado para gerir interrupções. O GIC é configurado para garantir que as interrupções de um mundo não são acessíveis a partir do outro mundo.

### TrustZone Bootstrap

O TrustZone Bootstrap é um pequeno pedaço de código que é executado quando o SoC é ligado,de modo a não arrancar o sistema num mundo inseguro e comprometer a segurança.

**Nota**: A configuração pode ser feita no ROM do SoC ou fornecido por periféricos externos.

### Enclaves

São uma forma de executar código de forma segura. O código é apenas decifrado dentro do processador e é mesmo seguro até por leituras diretamente na memória RAM.

Ciclo de vida:
1. Creation (`ECREAT`)
2. Loading (`EADD` ,`EEXTEND`)
3. Initialization (`EINIT`)
4. Enter/Exit the Enclave (`EENTER`/`EEXIT`)
5. Teardown (`EREMOVE`)

### Intel SGX (*Software Guard eXtensions*)

A Intel SGX é uma tecnologia que permite a criação de enclaves. 

Tudo **fora do processador** é considerado **inseguro**:
- Chave de cifra é escolhida aleatoriamente após cada reinício do processador.
- Valores lidos da memória são verificados de forma a corresponderem ao valor original (usando assinaturas digitais).
- Pode haver uma pequena perda de desempenho se a memória do enclave ficar em cache do processador.

Em particular, os seguintes componentes são considerados **inseguros**:
- BIOS (*Basic Input/Output System*);
- SMM (*System Management Mode*);
- ME (*Management Engine*, anel -3);
- Sistema operativo (*kernel*, anel 0);

Existem dois fluxos de execução:
- *ECALL*: Transferência de código/memória para **dentro** do enclave;
- *OCALL*: Transferência de código/memória para **fora** do enclave.

Exemplo de código de um enclave:

```c
#include "enclave_t.h"

void ecall_hello_world() {
    ocall_print_string("Hello, World!\n");
}

int main() {
    ecall_hello_world();
    return 0;
}
```

> [!Note] 
> O código enclave corre no anél 3 (*least privileged mode*).

### Memória Virtual

É técnica utilizada pelos sistemas operativos para fornecer aos programas a ilusão de que têm acesso a uma grande quantidade de memória principal (RAM) contígua, quando na verdade essa memória pode estar fragmentada e pode ser armazenada tanto na RAM quanto em dispositivos de armazenamento secundário, como discos rígidos.

É **útil para a virtualização**, pois:
1. **Permite o isolamento/gestão de recursos**: ajuda a garantir que um sistema operativo não interfere com outro;
2. **Evita conflitos de endereços**: cada sistema operativo pode ter o seu próprio espaço de endereçamento (através de *page tables*);
3. **Alocação dinâmica de memória**: permite que mesmo com limitações de memória física, as máquinas virtuais possam ter acesso a mais memória do que a memória física disponível.
## Sistema operativo

Um sistema operativo é um conjunto de programas que gerem os recursos de um sistema computacional e oferecem serviços aos utilizadores e aplicações.

Contém **dois modos**:
- *User-mode*: Executa as aplicações e serviços em modo normal da CPU, sem acesso a instruções privilegiadas.
- *Supervisor-mode*: Executa instruções em modo privilegiado da CPU (através do *kernel*), interagindo diretamente com o hardware.

O Kernel **tem como função**:
 - Virtualizar os recursos físicos;
 - Reforçar politicas de proteção contra acessos não autorizados/involuntários;

De modo a poder confiar no nosso sistema operativo no seu processo de boot:
- *Secure Bootstrapping*: Garantir que o sistema operativo é carregado (boot) de forma segura.
  - *Trusted Platform Module* (TPM): Verifica a integridade do sistema comparando os valores de hash dos componentes do arranque com os valores armazenados no TPM.
  - *Unified Extensible Firmware Interface* (UEFI) Secure Boot: Verifica a assinatura digital dos componentes do arranque, como o *bootloader*.
- *Remote Attestation*: Permite provar a integridade e confiança do sistema para terceiros, fazendo isto logo no processo de boot do sistema.

Protege contra ameaças como:
- Bootkits;
- Rootkits;
- Malware;
- Etc.

Podemos também proteger o conteúdo do sistema operativo usando:
- Intel SGX (*Software Guard Extensions*): Permite a execução de código seguro em *user-mode*.
- Sandbox: Permite a execução de código não confiável em ambientes controlados.

## Sandbox

O Sandbox é um mecanismo de segurança que permite a execução de código de forma isolada. É utilizado para executar código não confiável.

## Virtualização

Permite emular parte do hardware (virtual) dentro de um sistema operativo (real).

Existem dois **tipos de virtualização**:

*Hosted*: O sistema operativo hospedeiro é executado diretamente no hardware e o sistema operativo convidado é executado sobre o sistema operativo hospedeiro.

| Guest OS           |
| ------------------ |
| Hypervisor Process |
| Host OS            |
| Hardware           |

*Bare-metal*: O sistema operativo convidado é executado diretamente no hardware. É mais seguro pois permite o isolamento entre os sistemas operativos (sem necessitar de *on-the-fly translation*).

| Guest OS   |
| ---------- |
| Hypervisor |
| Hardware   |

### Máquinas Virtuais

É um ambiente de execução que simula um sistema computacional.
### *Hypervisors*

É um programa que permite a execução de várias máquinas virtuais num único sistema físico.

### Namespaces

Permite isolar e separar recursos do sistema para diferentes processos, de modo que cada conjunto de processos possa operar como se estivesse em um ambiente isolado. Esse conceito é fundamental para a criação de containers, como os usados em tecnologias de virtualização leve, por exemplo, Docker.

### Tipos de Namespaces

1. **PID (Process ID) Namespace**: Isola os identificadores de processos. Cada namespace PID pode ter seu próprio conjunto de IDs de processos, o que permite que processos dentro de um container tenham IDs de processos que parecem começar do zero.

2. **NET (Network) Namespace**: Isola a pilha de rede, incluindo interfaces de rede, roteamento, regras de iptables, etc. Cada namespace de rede pode ter suas próprias interfaces de rede e configuração de roteamento, permitindo a criação de ambientes de rede isolados.

3. **MNT (Mount) Namespace**: Isola o sistema de arquivos montado. Permite que diferentes namespaces vejam diferentes conjuntos de sistemas de arquivos montados, permitindo, por exemplo, que um container tenha seu próprio sistema de arquivos independente do sistema de arquivos do host.

4. **UTS (UNIX Time-Sharing) Namespace**: Isola o hostname e o domain name do sistema. Cada namespace UTS pode ter seu próprio nome de host e domínio, o que é útil para renomear containers de maneira independente.

5. **IPC (Interprocess Communication) Namespace**: Isola recursos de comunicação entre processos, como filas de mensagens, semáforos e segmentos de memória compartilhada. Isso permite que containers tenham seus próprios recursos IPC sem interferência mútua.

6. **USER Namespace**: Isola IDs de usuários e grupos. Permite que processos dentro de um namespace vejam um conjunto diferente de IDs de usuários e grupos, o que é útil para rodar processos como root dentro de um container sem ter privilégios de root no host.

7. **CGROUP Namespace**: Isola a visão de control groups (`cgroups`), permitindo que processos dentro de um namespace vejam e manipulem apenas os cgroups atribuídos a eles.

A criação e manipulação de namespaces em Linux pode ser feita através de chamadas de sistema como `clone()`, `unshare()` e `setns()`, bem como utilizando ferramentas como `ip netns` para namespaces de rede ou `docker` para criar e gerir containers que utilizam várias dessas namespaces de forma transparente.

### LXC (Linux Containers)

Tecnologia de virtualização a nível de sistema operacional que permite criar e gerir containers no Linux. Diferente das máquinas virtuais, que emulam hardware e executam um sistema operacional completo, os containers LXC compartilham o mesmo kernel do host, proporcionando uma virtualização mais leve e eficiente.

### Tipos de Containers

- **Privilegiados**: Os containers privilegiados (privileged) têm acesso total ao sistema host, permitindo que executem operações que normalmente seriam restritas, como montar sistemas de arquivos, criar dispositivos especiais, etc.
- **Não Privilegiados**: Os containers não privilegiados (non-privileged) executam com privilégios reduzidos, utilizando mapeamentos de UID (User ID) e GID (Group ID) para isolar os processos do container do sistema host.

### Vantagens dos Containers LXC

- **Desempenho Superior**: Devido à ausência da sobrecarga de emulação de hardware, os containers LXC são mais rápidos e consomem menos recursos.
- **Facilidade de Uso**: Ferramentas e comandos intuitivos facilitam a criação e gestão de containers.
- **Flexibilidade**: Pode ser usado para diversos fins, como desenvolvimento, testes, ambientes de produção, etc.

### Desvantagens dos Containers LXC

- **Segurança**: Embora o isolamento seja forte, ele não é tão completo quanto em máquinas virtuais. Vulnerabilidades no kernel podem afetar todos os containers.
- **Compatibilidade**: Todos os containers devem usar o mesmo kernel do host, limitando a diversidade de sistemas operacionais que podem ser executados simultaneamente.


### AppArmor

É uma ferramenta de controlo de acesso obrigatório (MAC - Mandatory Access Control) para aplicações específicas. Ele permite que um administrador do sistema imponha limites de acesso detalhados para aplicações individuais usando perfis específicos.

### Perfil de Segurança

Utiliza perfis para definir políticas de controlo de acesso granulares para recursos do sistema. Os perfis do AppArmor podem controlar o acesso a arquivos, direitos de execução, acesso à rede, etc.

### Aplicação

- **Kernel do Linux**: O AppArmor funciona no kernel do Linux como um Módulo de Segurança do Linux (LSM - Linux Security Module).
- **Framework do LSM**: Desde o kernel 2.6, o LSM fornece "hooks" para a inspeção de chamadas de sistema que estão prestes a fornecer acesso a objetos relevantes do sistema.

### Benefícios do AppArmor

- **controlo de Objetos**: Permite controlar os objetos que uma aplicação pode usar, oferecendo um controlo mais detalhado do que o modelo tradicional baseado em identidades de usuários e capacidades.
- **Redução da Superfície de Ataque**: Minimiza a superfície de ataque das aplicações, garantindo que elas operem com o mínimo de privilégios necessários, seguindo o princípio do menor privilégio. Isso é ideal para prevenir ataques de dia zero e comportamentos indesejados, como cavalos de Troia.
- **controlo de Exposição**: Permite que uma aplicação tenha múltiplas interfaces controladas, onde apenas as interfaces necessárias são exploradas por outras aplicações locais ou remotas.

### Políticas de Aplicação

- **Sem Perfil**: Se não houver um perfil para um binário em execução, não há controlo.
- **Com Perfil**: Se houver um perfil para um binário em execução, os controlos de acesso definidos pelo perfil são aplicados.

### Modos de Aplicação

- **Kill**: Violações de acesso terminam o processo.
- **Enforce**: Violações de acesso não são permitidas, e erros são retornados.
- **Complain**: Violações de acesso são apenas registadas, não impedindo a execução, permitindo ajuste iterativo dos perfis.

### Auditoria e Logging

- **Violações de Acesso**: Podem ser registadas para auditoria posterior.
- **Melhoria Interativa de Perfis**: Violações registadas podem ser usadas para melhorar perfis interativamente com a ferramenta `aa-logprof`.

### Perfis e controlo

- **Perfis Textuais**: São arquivos de texto que definem as políticas de segurança para aplicações.
- **Carregamento e Associação**: Perfis são carregados no kernel e associados a processos na execução de syscalls `exec`.
- **Modificações em Tempo de Execução**: Perfis podem ser modificados em tempo de execução, refletindo imediatamente nos processos associados.

### Sintaxe dos Perfis

- **Variáveis e Inclusões**: Permitem a definição de variáveis e a inclusão de outros arquivos, proporcionando flexibilidade na definição de perfis.
- **Curingas de Nomes de Arquivos**: Usados para especificar grupos de arquivos ou diretórios de forma concisa.
- **Permissões de Arquivos**: Definem permissões específicas como leitura, escrita, mapeamento de memória, entre outras.

### Controlo Abrangente

Os perfis do AppArmor podem controlar:

- **Acesso a Arquivos**: Leitura, escrita, execução, etc.
- **Execução de Binários**: controlo sobre quais binários podem ser executados.
- **Capacidades**: controlo sobre capacidades específicas do sistema.
- **Rede e Sockets**: controlo sobre operações de rede e sockets UNIX.
- **Montagem de Sistemas de Arquivos**: controlo sobre operações de montagem.
- **Sinais**: controlo sobre o envio e recebimento de sinais.
- **Dbus e ptrace**: controlo sobre comunicações Dbus e rastreamento de processos.
- **Rlimits**: controlo sobre limites de recursos.

### TPM

O Trusted Platform Module (TPM) é um microchip projetado para fornecer funções relacionadas à segurança, principalmente envolvendo a criptografia. É um componente essencial para a implementação de medidas de segurança avançadas em sistemas informáticos, neste caso, garantir a integridade e a segurança de um sistema.

### Funcionalidades do TPM

- **Geração de Chaves Criptográficas**: O TPM pode gerar chaves criptográficas seguras, que são armazenadas no chip e não podem ser exportadas.
- **Armazenamento Seguro de Chaves**: As chaves geradas pelo TPM são armazenadas dentro do chip, protegidas contra acesso não autorizado.
- **Criptografia**: O TPM pode realizar operações criptográficas, como cifragem e decifragem de dados, assinaturas digitais, etc.
- **Autenticação de Plataforma**: O TPM pode ser usado para verificar se um dispositivo está autorizado a aceder a uma rede ou recurso. Isso é feito através de um processo chamado de *attestation* (certificação), onde o TPM fornece provas de que o hardware e o software não foram alterados.
- **Verificação de Integridade**: O TPM pode armazenar hashes de software e firmware críticos, permitindo a verificação da integridade desses componentes durante o arranque do sistema.
- **Timestamping**: O TPM pode associar data e hora a um conjunto de dados, fornecendo uma prova de que esses dados existiam em um determinado momento.

#### Evolução do TPM 1.2 para 2.0

- **Problemas com SHA-1**: O TPM 1.2 confiava fortemente no algoritmo SHA-1, que foi atacado com sucesso em 2005.
- **TPM 2.0**: Projetado para permitir algoritmos de digest alternativos e alternativas para todos os algoritmos criptográficos, além de introduzir criptografia simétrica para implementar cifras híbridas.

#### Conceitos Criptográficos

- **Hash Extends**: Usado para implementar PCRs (Platform Configuration Registers), criar logs de auditoria e políticas de autenticação.
- **Tickets**: Estruturas de dados contendo um HMAC calculado sobre alguns dados, permitindo que o TPM reconheça a informação posteriormente sem ter que armazená-la.
- **Cifras Simétricas**: Utilizadas para garantir a confidencialidade dos dados privados do TPM e das comunicações.

#### Modos de Cifra Simétrica

- **Modos de Bloco**: ECB, CBC (necessitam de preenchimento quando os dados não são múltiplos do tamanho do bloco).
- **Modos de Fluxo**: CFB, OFB, CTR (usados quando os dados não estão alinhados ao bloco).
- **controlo de Integridade Integrado**: HMAC-based Encrypt-then-MAC, com HMACs calculados com nonces para prevenção de replay.

#### Chaves de Endosso (EKs)

- **Chaves de Endosso**: Pares de chaves que identificam dispositivos TPM, certificadas pelo fabricante do TPM e utilizadas para certificar outras chaves TPM.

#### Casos de Uso do TPM

- **Identificação do Host**: Autorizar a participação em ambientes protegidos.
- **Criptografia de Dados do Host**: Proteção de arquivos e sistemas de arquivos.
- **Geração de Números Aleatórios**: Essencial para gerar suas próprias chaves e nonces.
- **NVRAM**: Armazenamento de dados críticos.
- **PCRs (Platform Configuration Registers)**: Registos do TPM, que armazenam hashes de componentes críticos do sistema. São usados para verificar a integridade do sistema.

#### Pilha de Software TPM (TSS)

- **TSS**: Padrão de software do TCG, onde as aplicações escritas para o TSS devem funcionar em qualquer sistema que implemente um TSS compatível.
- **Camadas do TSS**: Incluem Feature API (FAPI), Enhanced System API (ESAPI), System API (SAPI), TPM Command Transmission Interface (TCTI), TPM Access Broker (TAB) e Resource Manager (RM).

#### Entidades TPM

- **Permanentes**: Incluem índices não voláteis, objetos, e sessões de autorização por senha.
- **Não Persistentes**: Desaparecem no power-on e podem ser salvas fora do TPM, mas não recarregadas após um ciclo de energia.
- **Persistentes**: Objetos que o proprietário de uma hierarquia define para persistir entre ciclos de energia.

#### Hierarquias TPM

- **Hierarquia de Plataforma**: Controlada pelo fabricante da plataforma.
- **Hierarquia de Armazenamento**: Controlada pelo proprietário da plataforma.
- **Hierarquia de Endosso**: Controlada pelo utilizador da plataforma.

#### Gestão de Chaves

- **Geração e Exportação de Chaves**: Chaves podem ser geradas internamente, exportadas e importadas.
- **Árvores de Chaves (Hierarquias de Chaves)**: Sequência de chaves começando por uma chave primária.

#### Sessões TPM

Mantêm o estado entre sequências de comandos, permitindo a continuação de operações criptográficas e de controlo de acesso.

- **Variações de Sessões**:
  - **Bound/Unbound**: Sessões encontra-se ligada a um valor de autorização e computa a chave de sessão com base nesse valor.  
  - **Salted/Unsalted**: Usam um valor aleatório para computar a chave de sessão (adiciona entropia).
- **Modificadores de Uso de Sessão**: Instruções por comando como continuar, cifrar, auditar.

#### Tipos de Sessões

- **Sessão de Senha**: Sessão de comando único dependente de uma senha fornecida em texto claro.
- **Sessão HMAC**: Sessão com HMAC computado com um valor authValue compartilhado.
- **Sessão de Política (Extended Authorization)**: Construída sobre a sessão HMAC e usa políticas para calcular um segredo compartilhado.

### Vantagens do TPM

- **Segurança Avançada**: Protege contra roubo e manipulação de chaves criptográficas.
- **Confiança e Integridade**: Assegura que o hardware e o software do sistema não foram alterados.
- **Gestão de Chaves**: Simplifica a gestão e armazenamento de chaves criptográficas de forma segura.

### Limitações do TPM

- **Dependência de Hardware**: Requer um chip TPM dedicado no hardware, o que pode limitar a sua disponibilidade.
- **Compatibilidade**: Nem todos os sistemas suportam ou são compativeis com o TPM, o que pode dificultar a sua implementação em alguns ambientes.

### Bootstrap Seguro

Um processo de bootstrap seguro é crucial para proteger a Base de Computação Confiável (TCB). Garante que o código inicial executado pelo sistema é confiável e não foi adulterado. Isto estabelece a base para um ambiente operacional seguro.

### AEGIS

- **Objetivo**: Garantir a integridade do bootstrap do sistema, assegurando que o kernel do sistema operativo é lançado por um processo de confiança.
- **Abordagem**: Construção de uma cadeia de verificações de integridade desde o momento de ligar o sistema até à transferência final de controlo para o sistema operativo. Verificações são feitas através da correspondência de hashes criptográficos calculados com assinaturas digitais armazenadas.

### Cadeias de Confiança

- **Princípio**: A confiança é construída sobre medições. Se um código é medido e validado antes da execução, uma cadeia de confiança pode ser estabelecida. Cada componente mede e verifica o próximo antes de transferir o controlo.

### Medições de Raiz de Confiança

- **SRTM (Static Root of Trust for Measurement)**: Parte do BIOS/UEFI e inicia a cadeia de confiança no momento da ligação do sistema.
- **DRTM (Dynamic Root of Trust for Measurement)**: Utiliza um Módulo de Código Autenticado (ACM) e requer um modo seguro especial da CPU (Intel TXT ou AMD SVM).

### Trusted Computing Platform Alliance (TCPA)

- **Definição de Confiança**: Um componente ou processo é considerado confiável se o seu comportamento for previsível sob quase todas as condições operacionais e altamente resistente à subversão.
- **Atestado Remoto**: Permite que uma plataforma comprove a sua configuração atual a outra plataforma de uma maneira confiável.Esse processo envolve o TPM assinando os valores dos PCRs com uma Chave de Identidade de Atestação (AIK). Os valores dos PCRs assinados, juntamente com um nonce fornecido pelo verificador, são enviados de volta ao verificador. O verificador pode então verificar a assinatura e os valores dos PCRs para garantir que correspondam aos valores esperados, assegurando que o sistema está em um estado confiável.

### TPM (Trusted Platform Module)

- **Funções Criptográficas**: Geração de números aleatórios, hashing, cifragem simétrica e assimétrica, geração e armazenamento seguro de chaves.
- **Tipos de TPM**:
  - **Discrete**: Implementado como um chip separado, altamente seguro e resistente a manipulações físicas.
  - **Integrated**: Integrado em um chip que fornece outras funções, ainda seguro, mas menos resistente a manipulações físicas.
  - **Firmware**: Implementado em software protegido, geralmente dentro de um TEE (Trusted Execution Environment).
  - **Software**: Implementado puramente em software, útil para protótipos, mas não recomendado para produção devido à falta de segurança.
  - **Virtual**: Fornecido por um hypervisor em ambientes de nuvem.

### Registos de Configuração da Plataforma (PCR)

- **PCRs**: Registos que mantêm uma cadeia de hashes para verificar a integridade do sistema ao longo do tempo.
- **Tipos de PCR**: Divididos por função, como SRTM e DRTM, e usados para garantir que somente software autorizado seja executado.

### Modos de Arranque da TCPA

- **Secure Boot**: O secure boot aplica políticas durante o processo de inicialização, garantindo que apenas software confiável seja executado. O arranque é interrompido se um valor de PCR não corresponder a um valor esperado.
- **Authenticated Boot (Trusted Boot)**: O authenticated boot verifica cada componente do processo de inicialização em relação a valores conhecidos (hashes), mas não aplica políticas. Regista as medições (hashes) nos PCRs. Os valores são armazenados nos registos PCR durante o arranque, permitindo verificações posteriores.

### UEFI (Unified Extensible Firmware Interface)

- **Secure Boot**: Processo de validação do firmware, que define como o firmware da plataforma gere os certificados de segurança e valida o firmware e o bootloader do sistema operativo.
- **Chaves do Secure Boot**:
  - **Platform Key (PK)**: Controlada pelo proprietário da plataforma.
  - **Key Exchange Key (KEK)**: Conjunto de chaves assimétricas controladas pelo fabricante e fornecedores de sistemas operativos.
- **Bases de Dados de Assinaturas**:
  - **db (whitelist)**: Contém chaves ou certificados que validam firmware autorizado.
  - **dbx (blacklist)**: Contém hashes de firmware não autorizado.

### Recomendações de Segurança de Arranque da NSA

- **Modos de Arranque**:
  - **Legacy Boot**: Compatível com hardware antigo, menos restritivo em termos de segurança.
  - **UEFI Native Boot**: Oferece mais flexibilidade e modularidade, mas requer suporte de hardware e software modernos.
  - **Secure Boot**: Valida todas as partes do software durante o arranque, impedindo a execução de software não autorizado.
  - **TPM Auditing**: Regista hashes de componentes do firmware no TPM para verificações de integridade, mas não impede a execução de malware.

### Definição e Componentes

- **Smartcard**: Cartão com capacidades de processamento computacional. Pode ter interfaces com contacto ou sem contacto.
- **Componentes Principais**:
  - **CPU**: Processador de 8/16 bits, com opção de co-processador criptográfico.
  - **ROM**: Armazena o sistema operativo, comunicação e algoritmos criptográficos.
  - **EEPROM**: Armazena o sistema de arquivos para programas/aplicações, chaves e senhas.
  - **RAM**: Armazena dados transitórios que são apagados quando o cartão é desligado.
  - **Segurança Física**: Inclui uma caixa à prova de violação e resistência a ataques de canal lateral.

### Protocolos

- **APDU (Application Protocol Data Unit)**: Usado para comunicação entre aplicações fora e dentro do cartão.
  - **T=0**: Cada byte é transmitido separadamente, sendo mais lento.
  - **T=1**: Transmissão em blocos de bytes, sendo mais rápido.
  - **ATR (Answer to Reset)**: Resposta do cartão a uma operação de reset, reportando o protocolo esperado pelo cartão.
- **Java Cards**: Smartcards que executam applets Java utilizando o Java Card Runtime Environment (JCRE), que roda sobre um sistema operacional nativo.

### Sistemas de Arquivos

- **Estrutura**: Composta por Master Files (MF), Dedicated Files (DF) e Elementary Files (EF).
- **Tipos de Arquivos**: Transparentes, de registos fixos, de registos variáveis e cíclicos.
- **Controlo de Acesso**: Podem ser configurados para exigir autenticação externa e proteção com MACs para acessar dados.

### Criptografia

Incluí geração de chaves, cifragem/decifragem, assinaturas digitais e armazenamento seguro de chaves. Esses serviços são cruciais para transações seguras e proteção de dados
