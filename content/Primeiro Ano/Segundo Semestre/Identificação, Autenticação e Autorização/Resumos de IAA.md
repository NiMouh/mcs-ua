## Aula 1

### Controlo de acesso

Consiste no conjunto de políticas e mecanismos que regulam o acesso a recursos (objetos).

Tem como requisitos:
- **Autenticação**: Prova que uma entidade tem um atributo de identificação.
- **Autorização**: Determina se uma entidade tem permissão para aceder a um recurso.
- **Auditoria**: Registo de eventos de acesso.

No controlo de acesso existem duas entidades:
- **Sujeito**: Entidade que tenta aceder a um recurso.
- **Objeto**: Recurso a que o sujeito tenta aceder.

### *Least Privilege Principle*

Princípio que defende que um sujeito deve ter apenas as permissões necessárias para realizar as suas tarefas.

Permissões **a mais** permitem a **criação de vulnerabilidades**.

Permissões **a menos** podem **impedir a realização de tarefas**.


### Modelos de controlo de acesso

Existem dois tipos de modelos de controlo de acesso:
- **Discretionary Access Control (DAC)**: Permissões são definidas pelo dono do objeto. Podem ser alteradas pelo dono do objeto ou por um administrador (e.g. *superuser*).
- **Mandatory Access Control (MAC)**: Permissões são definidas por o monitor de controlo de acesso (e.g. kernel). As permissões são **fixas** e não podem ser alteradas.

#### ACL (*Access Control List*)

Lista de controlo de acesso que associa sujeitos a objetos e define as permissões especificas de acesso (e.g. leitura, escrita). Estas listas são **armazenadas nos objetos**.

Este modelo é bastante utilizado em **sistemas de ficheiros**, pois permite uma gestão **mais granular** das permissões (ou seja, é possível definir permissões específicas para cada objeto).

#### *Capabilities*

*Token* que representa a autorização de um sujeito para aceder a um objeto. Estes *tokens* são **armazenados nos sujeitos** (e.g. OAuth *access tokens*).

Este modelo é bastante utilizado em **aplicações web**.

#### *Role-Based Access Control (RBAC)*

Modelo de controlo de acesso que associa sujeitos a **funções**. Cada função tem associadas **permissões** que definem o acesso a objetos.

**Não é um DAC nem um MAC**, pois as permissões são definidas pelas funções e não pelos donos dos objetos.

Todas as atividades de um sujeito são realizadas através de **transações autorizadas**, permitidas pelas permissões associadas às funções.

Tem as seguintes variantes:
- **RBAC 0**: Sem hierarquia de funções, sem restrições.
- **RBAC 1**: Com hierarquia de funções (*privilege inheritance*).
- **RBAC 2**: Com restrições de acesso (separação de direitos).
- **RBAC 3**: RBAC 1 + RBAC 2.

#### NIST RBAC

- **Flat RBAC (RBAC 0)**: Modelo simples com review de funções. Uma função fornece uma permissão específica para o sujeito.
- **Hierarchical RBAC (RBAC 1)**: Modelo com hierarquia de funções. Uma função pode herdar permissões de outra função.
- **Constraint RBAC (RBAC 2)**: Modelo com restrições de acesso. Uma função pode ter restrições de acesso a objetos. Pode ser:
  - *Static*: Funções em conflito não podem ser atribuídas.
  - *Dynamic*: Funções em conflito não podem ser ativadas na mesma sessão.
- **Symmetric RBAC (RBAC 3)**: Modelo com restrições de acesso simétricas. Uma função pode ter restrições de acesso a outras funções.

##### *Roles vs Groups*

- **Roles**: Coleção de permissões que definem o acesso a objetos. Um sujeito pode ter apenas um *role* a cada momento.
- **Groups**: Coleção de sujeitos. Um sujeito pode pertencer a vários grupos.

#### *Context-Based Access Control (CBAC)*

Modelo de controlo de acesso que associa sujeitos a objetos com base em **contexto** histórico. O acesso não pode ser concedido sem um motivo associado a eventos passados.

##### *Chinese Wall Policy*

Política de controlo de acesso que aborda o problema de **conflitos de interesse**. Impede que um sujeito aceda a objetos que possam criar um conflito de interesse com objetos a que o sujeito já acedeu.

#### *Attribute-Based Access Control (ABAC)*

Modelo de controlo de acesso que associa sujeitos a objetos com base em **atributos**. O acesso é concedido com base em regras que comparam os atributos do sujeito com os atributos do objeto.

##### Arquitetura *XACML*

Arquitetura que define um conjunto de regras para a definição de políticas de controlo de acesso.

Na arquitetura *XACML* existem os seguintes componentes:
- **PAP (*Policy Administration Point*)**: Componente que define as políticas de controlo de acesso.
- **PEP (*Policy Enforcement Point*)**: Componente que aplica as políticas de controlo de acesso.
- **PDP (*Policy Decision Point*)**: Componente que toma decisões com base nas políticas de controlo de acesso.
- **PIP (*Policy Information Point*)**: Componente que fornece informação sobre os sujeitos e objetos ao PDP.

<p align="center">
  <img src="image.png" alt="Arquitetura XACML">
</p>
<p align="center">
  <i>Fig. 1 - Arquitetura XACML</i>
</p>

#### *Break Glass Procedure*

Procedimento de emergência que permite o acesso a recursos críticos em situações de emergência. Este procedimento deve ser **monitorizado** e **auditado**.

#### *Separation of Duties*

Requisito de segurança usado para fraude e prevenção de erros. Consiste na disseminação de tarefas e responsabilidades entre várias pessoas.

**Nota**: Muitas vezes implementado com *RBAC*.

### Segurança *Multilevel*

Sujeitos (ou funções) agem consoante o seu nível de segurança. Os níveis não se sobrepõem e normalmente são representados numa ordem parcial (e.g. hierarquia de níveis).

O fluxo de informação funciona do seguinte modo:
- **Mesmo nível**: Informação autorizada.
- **Nível diferente**: Informação controlada (podendo variar consoante a política de controlo de acesso).

Níveis de acesso Militares:
- **Top Secret**: Informação que pode causar danos graves à segurança nacional.
- **Secret**: Informação que pode causar danos sérios à segurança nacional.
- **Confidential**: Informação que pode causar danos à segurança nacional.
- **Restricted**: Informação que não é pública.
- **Unclassified**: Informação que não é sensível.

Níveis de acesso Civis:
- **Restricted**: Informação que não é pública.
- **Proprietary**: Informação que é propriedade de uma organização.
- **Sensitive**: Informação que é sensível.
- **Public**: Informação que é pública.

**Nota**: **Um objeto pode pertencer a um ou mais níveis de segurança** e ter associadas permissões específicas para cada nível.

Existem **dois tipos** de modelos de segurança *multilevel*:
- **Bell-LaPadula**: Modelo que define regras para a **confidencialidade** (controlo de informação).
- **Biba**: Modelo que define regras para a **integridade** (controlo de alterações).

#### *Labels* de Segurança

*Label* que é associado a um objeto e a um sujeito. Este *label* contém informação sobre o nível de segurança do objeto e do sujeito.

Label = {Nível de Segurança, Categoria}

#### Bell-La Padula

É um *state-transition model*, ou seja, em cada estado existem sujeitos, objetos, uma matriz de acesso e um conjunto de regras.

Regras:
- *no read up*: Um sujeito de um nível de segurança inferior não pode ler um objeto de um nível de segurança superior (N(S) < N(O)).
- *no write down*: Um sujeito de um nível de segurança superior não pode escrever num objeto de um nível de segurança inferior (N(S) > N(O)).
- *strong star property*: Um sujeito de um nível de segurança igual ao do objeto pode ler o objeto (N(S) = N(O)).

**Nota**: Este modelo é DAC.

Este modelo segue o princípio da tranquilidade (*tranquility principle*), ou seja:
- **Tranquilidade forte**: Os níveis são fixos e não são alterados.
- **Tranquilidade fraca**: Os níveis podem ser alterados, caso a segurança do sistema não seja comprometida.

#### Biba Integrity

Semelhante ao Bell-La Padula, mas com as **regras invertidas**:
- *no read down*: Um sujeito de um nível de segurança superior não pode ler um objeto de um nível de segurança inferior (N(S) > N(O)).
- *no write up*: Um sujeito de um nível de segurança inferior não pode escrever num objeto de um nível de segurança superior (N(S) < N(O)).

Nota: O sujeito não pode neste modelo pedir um acesso maior do que o seu nível de segurança.

### Windows Mandatory Integrity Control

Modelo de controlo de acesso que define regras para a integridade de objetos no sistema operativo Windows. Permite o reforço de controlos de acesso mandatórios em objetos.

Ou seja:
- Caso o acesso seja negado, o objeto não é acedido e as DACLs não são verificadas.
- Caso o acesso seja permitido, as DACLs são verificadas.

A integridade é representada por *labels* de integridade:
- Untrusted
- Low (or AppContainer)
- Medium (default)
- Medium Plus
- High
- System
- Protected Process

Nível de integridade do processo:
- O minimo associado ao dono do processo e ao ficheiro executável.
- Processos de utilizador são normalmente *medium*/*high*.
- Processo de serviços são normalmente *high*.

### Clark-Wilson Integrity Model

Modelo de integridade que define regras para a integridade de objetos no sistema.

Foca-se em garantir a integridade através de:
- Certificação: Garantir que os objetos são criados de forma correta.
- Reforço: Garantir que os objetos são acedidos de forma correta.

## Questões Aula 1

**1. O modelo de controlo de acesso baseado em papéis (Role-Based Access Control, RBAC) é normalmente preferível para sistemas de informação em vez dos sistemas baseados em ACL (Access Control List) típicos dos sistemas de ficheiros. Explique porquê.**

R: No modelo RBAC, as permissões são definidas pelas funções e não pelos donos dos objetos, o que permite uma gestão mais eficiente e segura das permissões. Além disso, o modelo RBAC permite a definição de funções que podem ser atribuídas a vários sujeitos, o que facilita a gestão das permissões e a manutenção do sistema. Os sistemas baseados em ACL, são mais utilizados em sistemas de ficheiros, onde é necessário uma gestão mais granular das permissões, podendo definir permissões específicas para cada objeto.

**2. As políticas de controlo de acesso baseadas em papéis (Role-Based Access Control, RBAC) podem ser aperfeiçoadas através da inclusão de mecanismos suplementares. É o caso do modelo NIST, onde o Flat RBAC permite o mecanismo user-role review, e do Symmetric RBAC, que permite o mecanismo permission-role review. Explique:** 
    
    a. Em que consiste o user-role review? 

R: O mecanismo user-role review envolve a revisão das associações entre utilizados e *roles* para garantir que a atribuição da *role* ainda é adequada
    
    b. Em que consiste o permission-role review?

R: O mecanismo *permission-role review* consiste em assegurar que os *roles* tenham apenas as permissões necessárias para desempenhar suas funções, evitando assim o excesso de privilégios que possam comprometer a segurança do sistema.

**3. O sistema operativo Windows tem mecanismos de controlo de integridade para processos e diretorias que são  parecidos com o modelo de integridade de Biba. Explique:**
    
    a. Como funciona o modelo de integridade de Biba?

R: O modelo de integridade de Biba é um modelo de controlo de acesso que define regras para a integridade de objetos no sistema. Este modelo foca-se em garantir a integridade através de regras como *no read down* e *no write up*, que impedem, respetivamente, que um sujeito de um nível de segurança superior leia um objeto de um nível de segurança inferior e que um sujeito de um nível de segurança inferior escreva num objeto de um nível de segurança superior.
    
    b. Como funcionam os mecanismos de controlo de integridade do Windows?

R: O Windows Mandatory Integrity Control é um modelo de controlo de acesso que define regras para a integridade de objetos no sistema operativo Windows. Este modelo permite o reforço de controlos de acesso mandatórios em objetos, garantindo que o acesso é negado caso o objeto não seja acedido e as DACLs não sejam verificadas, e que o acesso é permitido caso as DACLs sejam verificadas. Os processos no Windows têm um nível de integridade associado, que é normalmente *medium*/*high* para processos de utilizador e *high* para processos de serviços.

**4. As capabilities do Linux permitem associar privilégios a aplicações concretas. Explique:**
    
    a. Como é que são associadas às aplicações?

R: As capabilities do Linux são associadas às aplicações através de *capabilities sets*, que são conjuntos de capacidades que podem ser atribuídas a processos individuais.

    b. Quais as vantagens que têm relativamente ao uso do mecanismo Set-UID?

R: As capabilities têm a vantagem de permitir uma gestão mais granular dos privilégios, uma vez que é possível atribuir apenas as capacidades necessárias a cada aplicação, em vez de atribuir todos os privilégios de um utilizador. Além disso, as capabilities são mais seguras do que o mecanismo Set-UID, uma vez que permitem a execução de aplicações com privilégios reduzidos, o que reduz a superfície de ataque do sistema.

**5. O modelo de controlo de acesso baseado em papeis (Role-Based Access Control, RBAC) é normalmente preferível para sistemas de informação em vez dos sistemas baseados em ACL típicos dos sistemas de ficheiros. Explique em que consiste o modelo RBAC.** 

R: O modelo RBAC consiste na atribuição de funções a sujeitos, onde cada função tem associadas permissões que definem o acesso a objetos. As funções são atribuídas a sujeitos, que realizam todas as atividades através de transações autorizadas, permitidas pelas permissões associadas às funções.

**6. Considere os modelos de controlo de fluxos de informação. Explique como é que os mesmos atuam tendo em conta certificações de segurança (security clearances) e classificações de segurança (security classifications).**

R: Certificações de segurança (ou security clearances) consiste na atribuição de níveis de segurança a sujeitos, que determinam o acesso a objetos. As classificações de segurança (ou security classifications) consistem na atribuição de níveis de segurança a objetos, que determinam o acesso por parte dos sujeitos. Os modelos de controlo de fluxos de informação atuam sobre atributos de segurança associados a sujeitos e objetos, permitindo ou negando o acesso com base nas regras de controlo de acesso definidas.

## Aula 2

### OAuth

Protocolo de autorização que permite a um sujeito aceder a um recurso protegido. Tem como objetivo permitir a uma aplicação aceder a recursos mantidos por um servidor em nome de um utilizador.

#### *Roles* no OAuth

Temos os seguintes atores:
- **Resource Owner**: Entidade capaz de conceder acesso a um recurso protegido.
- **Resource Server**: Servidor que aloja os recursos protegidos.
- **Client**: Aplicação que acede aos recursos protegidos em nome do utilizador.
- **Authorization Server**: Servidor que autentica o utilizador e concede autorização ao cliente.

#### *Endpoints*

São *endpoints* que permitem a comunicação entre os atores.

Ao longo do fluxo de autorização, temos os seguintes *endpoints*:
- **Authorization Endpoint**: Endpoint onde o utilizador é autenticado e autoriza o cliente a aceder aos seus recursos.
- **Token Endpoint**: Endpoint onde o cliente troca o *authorization grant* por um *access token*.
- **Redirection Endpoint**: Endpoint onde o cliente é redirecionado após a autorização do utilizador.

### *Clients*

O tipo de *Client* está relacionado com a capacidade de manter a confidencialidade das credenciais.

Temos:
- **Public**: Não consegue manter a confidencialidade das credenciais (e.g. aplicações web, aplicações móveis).
- **Confidential**: Consegue manter a confidencialidade das credenciais (e.g. *secure server*).

Nota: Os *Clients* que acedem aos servidores OAuth devem ser registados posteriormente.

### *Tokens*

Os *tokens* são utilizados para representar a autorização de um sujeito para aceder a um recurso.

Temos os seguintes tipos de *tokens*:
- **Authorization grant**: Autorização concedida pelo utilizador ao cliente. Tem um tempo de vida curto (o suficiente para obter um *access token*).
- **Access token**: Representa a autorização do utilizador para aceder a um recurso.
  - *Bearer tokens*: São enviados em cada pedido HTTPS. O *Client* pode transferir o *token* para outro *Client*.
- **Refresh token**: Utilizado para obter um novo *access token* sem a necessidade de uma nova autorização do utilizador.

### *Flows* OAuth

No OAuth existem vários *flows* que permitem a comunicação entre os atores.

Temos os seguintes *flows*:

<p align="center">
  <img src="image-1.png" alt="Flows OAuth" width="400px">
</p>
<p align="center">
  <i>Fig. 2 - *Flows* OAuth</i>
</p>

#### *Authorization Code Flow*

Neste *flow* temos a verificação de três entidades:
- **Servidor OAuth verifica Resource Owner**: Através de username/password ou outro método.
- **Servidor OAuth verifica Client**: Através de *client_id* e *client_secret*.
- **Client verifica Servidor OAuth**: Através de certificado digital e URL.

Tem como requisitos:
- Aplicações *confidential*.
- Armazenamento seguro de *client_secret* e *client_id*.

Funciona da seguinte forma:

#### *Implicit flow (grant)* 

Normalmente utilizado em *Single Page Applications* (SPA), onde não existe um *backend*. É uma maneira de obter um *access token* sem a necessidade de um *client secret*.

Tem como requisitos:
- Aplicações *public*.

As suas limitações:
- Não tem *refresh token*.
- Não tem autenticação do *client*.

Funciona da seguinte forma:
1. O *Browser* faz pedido a API do *Resource Server* para obter o recurso;
2. *Authorization Server* autentica o *Resource Owner* (manda um *access token* logo a seguir);
3. O *Browser* usa outra vez a API do *Resource Server* para obter o recurso.

#### *Resource owner password credentials flow*

Normalmente utilizado em *confidential clients*. 

Existe a partilha das credenciais do *resource owner* com o *client* (para isto funcionar, o *client* deve ser confiável).

Tem como requisitos:
- Aplicações *confidential*.
- Partilha das credenciais do *resource owner* com o *client*.
- Armazenamento seguro dos *tokens*, *Client ID* e *Client Secret*.

As suas limitações:
- O *Resource Owner* precisa confiar no *client*.

Funciona da seguinte forma:
1. *Client* solicita um *access token* com as credenciais do *resource owner*;
2. *Client* recebe o *access token*.
3. *Client* pode aceder aos recursos.

#### *Client credentials flow*

Utiliza a arquitetura *2-legged* (*Client*, *Resource Server*). O *client* obtém um *access token* diretamente, **não necessitando de um *resource owner* para autenticação**.

Tem como requisitos:
- Aplicações *confidential*.
- Armazenamento seguro dos *tokens*, *Client ID* e *Client Secret*.

Funciona da seguinte forma:
1. *Client* solicita um *access token* com as suas credenciais (ID do cliente + segredo do cliente);
2. *Client* recebe o *access token*;
3. *Client* pode aceder aos recursos.

### *Proof Key for Code Exchange* (PKCE)

É um método de segurança para o *Authorization Code Flow*. Utiliza um *code challenge*, sendo este um *hash* de um *code verifier*.

### *Device authorization grant*

Utiliza um segundo dispositivo para fazer a autenticação e autorizar o acesso a um recurso (e.g. *smartphone*, *tablet*).

## Questões Aula 2

**1. O OAuth 2.0 é uma norma que permite conceder direitos de acesso a recursos. Indique quem são as entidades consideradas na mesma e qual o seu papel.**

R: As entidades consideradas no OAuth 2.0 são:

- Resource Owner: Entidade capaz de conceder acesso a um recurso protegido.
- Resource Server: Servidor que aloja os recursos protegidos.
- Client: Aplicação que acede aos recursos protegidos em nome do utilizador.
- Authorization Server: Servidor que autentica o utilizador e concede autorização ao cliente.

**2. O OAuth 2.0 é uma norma que permite conceder direitos de acesso a recursos. Indique:**
    
    a. Quem são as entidades consideradas na mesma.

R: As entidades consideradas no OAuth 2.0 são:

- Resource Owner: Entidade capaz de conceder acesso a um recurso protegido.
- Resource Server: Servidor que aloja os recursos protegidos.
- Client: Aplicação que acede aos recursos protegidos em nome do utilizador.
- Authorization Server: Servidor que autentica o utilizador e concede autorização ao cliente.

    b. Como se autenticam entre si (considere o fluxo base, authorization code flow). 

R: Segundo o fluxo base, *authorization code flow*, a autenticação é feito a três entidades:
- É feita a autenticação do Resource Owner pelo Servidor OAuth, através de username/password ou outro método.
- É feita a autenticação do Client pelo Servidor OAuth, através de *client_id* e *client_secret*.
- É feita a autenticação do Servidor OAuth pelo Client, através de certificado digital e URL.

**3. O OAuth 2.0 permite o acesso a recursos protegidos com base em access tokens. Explique:** 
    
    a. Que entidade fornece estes access tokens? 

R: Os *access tokens* são fornecidos pelo *Authorization Server*.
    
    b. Que entidade autoriza o fornecimento destes access tokens?

R: O *Resource Owner* autoriza o fornecimento dos *access tokens* autenticando-se no *Authorization Server*.

## Aula 3

### Privilégios de gestão no Linux

Na filosofia UNIX:
- Processos privilegiados (UID = 0): passam qualquer verificação de permissão no kernel.
- Processos não privilegiados (UID != 0): sujeito a verificação de permissões baseado nas credenciais do processo.

### *Special protection bits*

Existem *special protection bits* que permitem a execução de programas com privilégios especiais.

Temos:
- Set-UID: Permite a execução de um programa com um UID (identificador de utilizador) diferente.
- Set-GID: Permite a execução de um programa com um GID (identificador de grupo) diferente.
- Sticky bit: Permite que apenas o dono do ficheiro possa manipular o ficheiro.

#### *Set-UID*

O mecanismo Set-UID funciona mudando o effective UID do processo executando um programa. Permite aos utilizadores normais executar programas com privilégios de administrador (e.g. *passwd*).

Existem dois UID's:
- **Real UID**: UID do utilizador que criou o processo.
- **Effective UID**: UID que o processo está a usar.

### *Capabilities*

Permite dividir privilégios de *super-user* em várias capacidades. São um atributo por processo.

As *capabilities* são divididas em *sets*:
- *Effective*: conjunto de *capabilities* usadas pelo kernel para verificar permissões.
- *Permitted*: conjunto de *capabilities* que o processo pode usar. Uma vez que uma *capability* é removida do *permitted set*, não pode ser adicionada novamente.
- *Inherited*: conjunto de *capabilities* que são passadas para os processos filhos.
- *Bounding*: usadas para limitar as *capabilities* que são herdadas pelos processos filhos.
- *Ambient*: conjunto de *capabilities* que são passadas para os processos filhos que não têm *capabilities* herdadas (são *permitted* e *inherited*).

<p align="center">
  <img src="image-2.png" alt="Capabilities" width="400px">
</p>
<p align="center">
  <i>Fig. 3 - Capabilities transferidas entre processos </i>
</p>

### *Control groups* (cgroups)

Coleção de processos restritos pelo mesmo critério e associados a um conjunto de parametros/limites.

São usados para controlar o uso de recursos nos processos, através de um *subsystem*.

Este *filesystem* é montado em */sys/fs/cgroup* e contêm um conjunto de controladores que permitem controlar o uso de recursos, como:
- CPU
- Memória
- Dispositivos
- Rede
- ...

Um processo pode ser controlado por um número arbitrário de *control groups*, a lista é data pelo *filesystem* `/proc/[pid]/cgroup`.

### Linux Security Modules (LSM)

Permitem adicionar novas extensões MAC ao kernel Linux.

Nota: Essas extensões não são modulos do kernel, são embutidos no código do kernel e podem ou não ser ativados no arranque.

Exemplos de extensões:
- **Capabilities**;
- **AppArmor**: Permite definir políticas de controlo de acesso baseadas em *profiles*.
- **SafeSetID**;
- ...

### *Namespaces*

Permitem isolar recursos do sistema em *views*, criando um ambiente isolado para processos.

#### *Containers*

Explora os *namespaces* para fornecer uma visão virtual do sistema (isolamento de redes, etc.). Os processos são executados dentro dos *containers*.

## Questões Aula 3

**1. Considere o conceito de Control Groups (cgroups) do Linux. Explique de que forma os mesmos podem ser usados para controlar o uso de recursos por processos.** 

R: Os *control groups* (cgroups) do Linux são uma coleção de processos restritos pelo mesmo critério e associados a um conjunto de parâmetros/limites. Os cgroups são usados para controlar o uso de recursos nos processos, através de um *subsystem*. Permitem controlar o uso de recursos como CPU, memória, dispositivos, rede, entre outros. Um processo pode ser controlado por um número arbitrário de cgroups, e a lista dos cgroups a que um processo pertence é dada pelo *filesystem* `/proc/[pid]/cgroup`.

**2. Considere o conceito de Control Groups (cgroups) do Linux. Explique de que a sua organização hierárquica é usada para controlar o uso de recursos por processos.**

R: A organização hierárquica dos cgroups é usada para controlar o uso de recursos por processos de forma mais eficiente. Os cgroups são organizados numa árvore hierárquica, onde cada cgroup pode ter subcgroups. Os cgroups pai podem impor limites aos cgroups filhos, e os cgroups filhos podem herdar as configurações dos cgroups pais. Isto permite uma gestão mais eficiente dos recursos, uma vez que é possível definir limites globais para um conjunto de processos e limites específicos para subconjuntos de processos.

## Aula 4

### Requisitos de autenticação

- Quão bom é a provar a identidade de um sujeito?
- Quão dificil é de falsificar?
- Level of Assurance (LoA): Nível de confiança na autenticação.
  - **LoA 1**: Pouca confiança.
  - **LoA 2**: Confiança média.
  - **LoA 3**: Alta confiança.
  - **LoA 4**: Muito alta confiança.
- Robustez: Quão resistente é a ataques?
- Simplicidade: Quão fácil é de usar?
- Forma de tratar vulnerabilidades causadas por humanos.

### Deployment model

A forma como a autenticação é implementada.

Pode ser:
- Temporal:
  - Quando a interação começa;
  - Contínua.
- Direcional:
  - Unidirecional: Apenas o sujeito é autenticado.
  - Bidirecional: Ambas as partes são autenticadas.

### Abordagens de autenticação

Existem várias abordagens de autenticação:
- Abordagem direta: O sujeito fornece credenciais para autenticação, espera pela resposta e recebe a resposta.
- Abordagem em *challenge-response*: O sujeito recebe um desafio, responde ao desafio e recebe a resposta.

#### Biometria

Seguindo a abordagem direta, um tipo de credencial é a biometria. 

Tem como vantagens:
- Conveniente.
- Não pode ser transferida para outra pessoa.

Tem como desvantagens:
- Pode ser falsificada.
- Credenciais não podem ser alteradas.
- Risco à integridade física.

#### OTP (*One-Time Password*)

Ainda seguindo a abordagem direta, um tipo de credencial é o OTP.

Tem como vantagens:
- Pode ser gerado de forma segura.
- A alteração de credenciais é feita após cada utilização.
- Atacantes não podem reutilizar credenciais.

Tem como desvantagens:
- Utilizadores precisam de um dispositivo para gerar OTPs.
- Utilizadores precisam de saber qual o OTP a utilizar para cada autenticação.

Existem variantes, tais como:
- **TOTP (*Time-based OTP*)**: OTP gerado com base no tempo e uma chave partilhada (contador é gerado com base no tempo, `atual - inical / intervalo`).
- **HOTP (*HMAC-based OTP*)**: OTP gerado com um contador e uma chave partilhada (contador é atualizado independentemente).

#### Gerados OTP baseados em Tokens

Os OTPs podem ser gerados com base em dispositivos *hardware* (e.g. yubikey).

Gera um OTP com base no:
- **UID**: Identificador único do dispositivo.
- **Número do Token**: valor gerado aleatoriamente.

#### S/Key

Sistema de autenticação que utiliza uma sequência de palavras-passe.

O autenticador sabe:
- Último OTP usado.
- Valor da *seed* para o OTP de cada utilizador.

Funciona da seguinte forma:
1. O autenticador gera uma *seed* aleatória.
2. Gera um OTP inicial: `OTP = h(seed,pwd)`.
3. O autenticador armazena o OTP, a *seed* e o número de sequência.
4. O autenticador envia a *seed* e o número de sequência ao utilizador.
5. O utilizador gera n-1 OTPs e seleciona o último.
6. O autenticador computa o h(OTP) e compara com o OTP armazenado.

Tem como vantagens:
- Palavras-passe são desconhecidas para o autenticador.
- Os OTPs podem ser usados como palavras-passe ordinárias.

Tem como desvantagens:
- Necessidade de computar n-1 OTPs para autenticação (via aplicação ou dispositivo).
- Possível vulnerabilidade a ataques de dicionário.

#### Single Sign-On (SSO)

Permite a um utilizador autenticar-se uma vez e aceder a vários serviços sem necessidade de autenticação adicional. O autenticador é chamado de *Identity Provider* (IdP).

#### Key Distribuition Services (KDS)

Serviço que distribui chaves de sessão para entidades autenticadas. Essa chave pode depois ser usada por essas entidades para comunicação segura (e.g. Wi-Fi, Kerberos).

## Questões Aula 4

**1. Considere o protocolo de autenticação S/Key. Explique de que maneira explora uma hashing chain para gerar uma sequência de senhas descartáveis (One-Time Passwords, OTPs)?**

R: O autenticador define uma *seed* aleatória e gera um OTP inicial com base na *seed* e na palavra-passe do utilizador (fazendo o hash 'n' vezes). O autenticador armazena o OTP, a *seed* e o número de sequência. O autenticador envia a *seed* e o número de sequência ao utilizador, que gera n-1 OTPs e seleciona o último. O autenticador computa o h(OTP) e compara com o OTP armazenado.

**2. A gestão de identidades agregada, baseada num IdP (Identity Provider) para vários serviços (Service Providers) é normalmente usada para concretizar o conceito de Single Sign-On (SSO). Explique como é normalmente concretizado, na prática, para aplicações Web.**

R: A identidade de um cliente, após a autenticação, é fornecida a todos os serviços federados, os atributos correspondentes podem depender do serviço. O cliente pode então aceder a todos os serviços sem ter de se autenticar novamente.

**3. Explique em que consistem os ataques com dicionários a protocolos de autenticação.**

R: Os ataques de dicionário a protocolos de autenticação consistem em tentativas de autenticação com palavras-passe comuns ou previsíveis, com o objetivo de adivinhar a palavra-passe correta.

**4. O protocolo de autenticação do GSM é imune a ataques de dicionário. Explique porquê.**

R: O protocolo de autenticação do GSM utiliza um *challenge-response* para autenticação aleatório e único baseado num segredo partilhado entre o HRL e a BS, o que torna o protocolo imune a ataques de dicionário.

**5. Explique como é realizada a autenticação dos servidores no SSH.**

R: A autenticação dos servidores no SSH é realizada através de chaves públicas e privadas. O servidor SSH gera um par de chaves pública e privada, e envia a chave pública para o cliente. O cliente verifica a autenticidade do servidor através da chave pública, e envia uma mensagem cifrada com a chave pública do servidor. O servidor decifra a mensagem com a sua chave privada e autentica o cliente.

**6. Considere a arquitetura de autenticação 802.1X. Explique qual a relevância para a mesma da existência do protocolo EAP.**

R: Permite o encapsulamento de vários protocolos de autenticação, como o EAP-TLS, EAP-TTLS, EAP-PEAP, EAP-FAST, entre outros.

**7. Explique em que é que consiste o conceito de *Single Sign-On* (SSO).**

R: O *Single Sign-on* consiste num mecanismo que unifica e centraliza a autenticação entre um conjunto de serviços, permitindo que um utilizador autentique-se uma vez e aceda a vários serviços sem necessidade de autenticação adicional.

**8. Considere o conceito de autenticação biométrica. Na mesma é preciso calibrar o equipamento que faz a leitura da biometria de modo a ajustar duas taxas (falsos positivos e falsos negativos). Explique por que razão esta calibração pode ser complexa em cenários reais.**

R: A calibração do equipamento de leitura da biometria pode ser complexa devido a vários fatores, como a qualidade da imagem capturada, a variação da biometria ao longo do tempo, a variação da biometria entre diferentes utilizadores, a variação da biometria devido a fatores externos (e.g. temperatura, humidade), entre outros. Estes fatores podem afetar a precisão da leitura da biometria e, consequentemente, a taxa de falsos positivos e falsos negativos.

**9. Considere o protocolo de autenticação HOTP (HMAC-based One-Time Password), que permite calcular OTPs a partir de uma chave partilha e de um contador fracamente sincronizado. Explique:**

  **a. Como evolui o contador ao longo da utilização de OTPs gerados com este protocolo?**

R: O contador é atualizado após cada utilização de um OTP, de maneira independente (separado da geração de OTPs).

  **b. Que configurações podem ser feitas no validador para lidar com essa evolução?**

R: É feita a sincronização do contador entre o validador e o gerador de OTPs, de forma a garantir que o contador é atualizado corretamente.

**10. Explique como é realizada a autenticação de uma pessoa através de um cartão de cidadão.**

R: É feito um *challenge-response* usando assinaturas digitais, onde o autenticador gera um desafio aleatório, o cartão de cidadão assina o desafio com a chave privada e o autenticador verifica a assinatura com a chave pública.

**11. O SSH permite uma autenticação mútua dos interlocutores, mas não segundo o mesmo paradigma nos dois sentidos. Descreva:**

  **a. De que forma se autentica o extremo servidor?**

R: É autenticador através do par de chaves pública e privada.

  **b. De que forma se autentica o extremo cliente?**

R: É autenticado através de username/password ou par de chaves pública e privada.

## Aula 5

### PAM (*Pluggable Authentication Modules*)

Conjunto de bibliotecas que permitem a autenticação de utilizadores em sistemas UNIX.

Permite:
- Unificação de mecanismo de autenticação.
- Acesso autenticado a serviços independentemente do mecanismo de autenticação.
- Diversas abordagens de interface (e.g. consola, *web*, smart-cards).

Contêm as seguintes funções:
- **auth**: Autenticação do utilizador.
- **account**: Reforço das políticas de acesso com base em informações de conta.
- **password**: Gestão de palavras-passe.
- **session**: Inicialização e finalização de sessões.

### *Modules*

São *modules* que permitem a extensão de funcionalidades do PAM.

São carregados dinamicamente e podem ser configurados no ficheiro `/lib/security/pam.*.so/`.

### *Orchestration files*

Ficheiros que permitem a configuração do PAM, especificando como as funções são aplicadas.

Nota: Normalmente é utilizado um por aplicação.

<p align="center">
  <img src="image-3.png" alt="Arquitetura PAM">
</p>
<p align="center">
  <i>Fig. 4 - Arquitetura PAM</i>
</p>

### *Orchestration* de funções PAM

É uma sequência de invocações de módulos por função. 

Cada módulo tem os seus parametros e **semântica**:
- **required**: Se o módulo falhar, a autenticação falha e o processo é terminado.
- **requisite**: Se o módulo falhar, a autenticação falha e o utilizador é notificado.
- **sufficient**: Se o módulo falhar, a execução continua.
- **optional**: O resultado é ignorado.

A execução continua até ao fim ou até um módulo falhar.

Contém também *advanced decisions*, que permitem a execução de módulos com base em condições:
- **ignore**: Ignora o resultado do módulo.
- **bad**: Continua, porém a decisão é uma falha.
- **die**: termina o processo (c/ falha).
- **ok**: Continua, porém a decisão é um sucesso.
- **done**: Termina o processo (c/ sucesso).
- **reset**: Reinicia a pilha de decisões.
- **N**: mesmo que o ok, mas salta N módulos.

### *Module Invocation*

Cada módulo é invocado com um conjunto de argumentos e devolve um código de retorno.

Sintaxe:
```
função controlo módulo [parametros]
```
## Aula 6 - Smartcards

### Smartcards

- Definição: Um cartão com capacidades de processamento computacional, incluindo CPU, memória ROM, EEPROM, e RAM.
- Interfaces: Podem ter contacto (com chip visível) ou ser sem contacto (usando RFID ou NFC).

### Why smartcards

- Interoperabilidade: Os cartões inteligentes são projetados para funcionar em diversas indústrias e sistemas, facilitando a sua adoção em múltiplos contextos.
- Suporte a multi-aplicações: Podem ser utilizados para várias finalidades, como identificação, autenticação, transações financeiras e acesso a serviços.
- Transações seguras: Oferecem um elevado nível de segurança em transações devido à criptografia avançada.
- Aceitação pelo utilizador: A simplicidade e conveniência dos cartões inteligentes aumentam a aceitação e confiança do utilizador.
- Acessibilidade: Facilidade de uso e acessibilidade aumentada, permitindo a inclusão de diferentes grupos de utilizadores.

### Smartcard applications: Communication protocol stack

- Protocolos de Comunicação:
  - APDU (Application Protocol Data Unit): Conjunto de comandos e respostas usados para comunicação entre o cartão e o leitor.
  - T=0 e T=1: Protocolos de transmissão de dados; T=0 transmite byte a byte, enquanto T=1 transmite blocos de bytes, sendo mais rápido.

### T=0 and T=1

- T=0: Transmissão de cada byte separadamente, o que resulta numa comunicação mais lenta.
- T=1: Transmissão de blocos de bytes, permitindo uma comunicação mais rápida.
- ATR (Answer to Reset): A resposta do cartão a uma operação de reset, indicando o protocolo esperado pelo cartão.

### APDU (ISO 7816-4)

- Comando APDU: Estrutura de comando e resposta definida pela norma ISO 7816-4.
  - CLA (Class): Indica a classe da instrução.
  - INS (Instruction): Especifica o comando a ser executado.
  - P1 e P2 (Parameters): Parâmetros específicos do comando.
  - Lc: Comprimento dos dados opcionais do comando.
  - Le: Comprimento dos dados esperados na resposta.
- Resposta APDU: Estrutura de resposta com dados e códigos de estado.
  - SW1 e SW2 (Status Words): Bytes de status que indicam o resultado da operação (0x9000 significa sucesso).

### Smartcard: File system

- Sistema de Ficheiros: Estrutura de armazenamento de dados no cartão inteligente, organizada em diferentes tipos de ficheiros.
  - Master File (MF): Raiz do sistema de ficheiros, identificada por ID 0x3F00.
  - Dedicated File (DF): Similar a um diretório, pode conter outros DFs ou EFs.
  - Elementary File (EF): Ficheiro de dados comum, com tamanho fixo determinado na criação.

### Java cards

- Cartões Java: Cartões inteligentes que executam applets Java, utilizando o Java Card Runtime Environment (JCRE).
  - JCRE: Inclui a Máquina Virtual Java, Card Executive (gestão e comunicações) e Java Card Framework (funções de biblioteca).

### Cryptographic services

- Serviços Criptográficos:
  - Cifras: Algoritmos para cifragem e decifragem de dados.
  - Funções de Digestão: Algoritmos que produzem um resumo (hash) dos dados.
  - Geração e Gestão de Chaves: Criação e manutenção de chaves criptográficas.
  - Assinaturas Digitais: Criação e verificação de assinaturas eletrónicas.
  - Certificados de Chave Pública: Gestão de certificados que associam uma chave pública a uma entidade.

### Cryptographic services: Middleware

- Middleware Criptográfico: Software que fornece uma interface entre aplicações e dispositivos criptográficos, permitindo a utilização de serviços criptográficos.
  - PKCS #11: Interface de Token Criptográfico (Cryptoki), definida pela RSA Security Inc.
  - PKCS #15: Formato de Informação de Token Criptográfico, também definido pela RSA Security Inc.
  - CAPI CSP: Provedor de Serviço Criptográfico do CryptoAPI, definido pela Microsoft para sistemas Windows.
  - PC/SC: Estrutura padrão para acesso a cartões inteligentes em sistemas Windows.

### PKCS #11

- Integração Middleware Cryptoki: Interface de programação de aplicações (API) para acesso a dispositivos criptográficos, como cartões inteligentes.
  - Hierarquia de Objetos: Estrutura que define diferentes tipos de objetos como dados, chaves e certificados.
  - Sessões Cryptoki: Conexões lógicas entre aplicações e tokens, com sessões de leitura e escrita, geridas por diferentes proprietários (público, utilizador, oficial de segurança).
  - Operações de Sessão: Incluem login/logout, gestão de objetos e operações criptográficas.

### Cartão de Cidadão: Middleware

- Middleware para Unix (Linux/MacOS): Componentes de software específicos para permitir o uso do Cartão de Cidadão nestes sistemas operativos.
- Middleware para Windows: Componentes de software para uso do Cartão de Cidadão em sistemas Windows, integrando-se com CryptoAPI e outros padrões.

### Authentication with the PTEID

- Autenticação com PTEID: Utiliza um NONCE enviado ao Cartão de Cidadão para ser assinado com a chave privada. Enfrenta desafios como a falta de acesso direto do navegador ao cartão, exigindo o uso de plugins ou applets.

### PT Authentication Plugin

- Plugin de Autenticação PT: Solução que permite acesso ao cartão através de um servidor web local instalado no computador do utilizador. Este plugin lida com solicitações autenticadas.

### Mobile Digital Key (CMD)/Virtual Smart Card

- Chave Digital Móvel (CMD): Permite autenticação e assinatura sem necessidade do cartão físico, mas mantendo um nível de segurança semelhante. Utiliza autenticação de dois fatores (2FA), combinando um código PIN e um código enviado por outro canal, como SMS.

## Aula 7 - FIDO

### FIDO (Fast Identity Online) Alliance

- **Aliança FIDO**: Uma associação da indústria aberta com a missão de desenvolver padrões de autenticação e promover a sua adoção para reduzir o uso de senhas.
- **Abordagem**: Autenticação forte baseada em chaves públicas, resistência ao phishing e boa usabilidade.

### FIDO token-based authentication

- **Autenticação baseada em tokens**: As chaves de autenticação são armazenadas em tokens. A autenticação é feita por meio de assinaturas, que são difíceis de copiar manualmente.
- **Enrolamento de dispositivos**: Adicionar dispositivos aos perfis dos utilizadores é responsabilidade dos autenticadores, incluindo o processo de recuperação em caso de perda de um token.

### FIDO certification

- **Certificação FIDO**: Valida a qualidade dos produtos FIDO.
  - **Programas de certificação**: Funcionais (conformidade e interoperabilidade), autenticadores (proteção de segredos de nível L1 a L3+), e biométricos (taxas de falsos aceites e rejeições, IAPMR).

### Universal 2nd Factor (U2F) protocol

- **Protocolo U2F**: O utilizador possui um dispositivo U2F que cria um par de chaves único por serviço (baseado em URL). Cada serviço regista a chave pública na conta do utilizador.
- **Interação**: Usado por APIs JavaScript em navegadores e APIs nativas do sistema operativo.

### U2F devices

- **Dispositivos U2F**:
  - **USB, NFC e Bluetooth LE**: Dispositivos com interface HID reconhecível.
  - **Aplicações de software**: Podem ser suportadas por dispositivos de segurança de hardware.
  - **Presença do utilizador**: Necessário para prevenir o uso sem consentimento. O consentimento é normalmente dado através de toque num botão, impressão digital ou código PIN.

### U2F protocols

- **Camada superior**: Protocolo criptográfico central que define a semântica e os dados trocados.
- **Camada inferior**: Protocolo de transporte host-dispositivo, conhecido como CTAP (Client To Authenticator Protocol).

### U2F upper layer protocol: User registration

- **Registo do utilizador**: O dispositivo U2F gera um par de chaves específico para o serviço, identificando o serviço com um hash da sua identidade (protocolo, hostname, porta). O dispositivo retorna um Handle de Chave e a chave pública ao serviço.

### U2F upper layer protocol: User authentication (1)

- **Autenticação do utilizador**: O utilizador fornece o seu identificador no serviço. O serviço retorna o Handle de Chave do utilizador e um desafio aleatório. A aplicação cliente do utilizador utiliza um dispositivo local para assinar os dados fornecidos (Handle de Chave, hash da identidade do serviço e hash dos dados do cliente).

### U2F upper layer protocol: User authentication (2)

- **Processo de autenticação**: O dispositivo verifica se o hash da identidade do serviço é válido para o Handle de Chave. Em caso de sucesso, procura a chave privada correspondente e assina os dados do cliente, retornando a assinatura para validação pelo serviço.

### Certification of U2F devices

- **Certificação de dispositivos U2F**: Os provedores de serviços precisam garantir a qualidade dos dispositivos U2F, que devem ter um par de chaves de certificação com certificado de chave pública emitido pelo fabricante. Os fabricantes precisam ser certificados pela FIDO.

### Anonymity of attestation key pairs

- **Anonimato dos pares de chaves de certificação**: Os dispositivos U2F não podem ter pares de chaves de certificação únicos para evitar *tracking* de utilizadores. Em vez disso, os pares de chaves de certificação são partilhados por lotes.

### Uncertified U2F devices

- **Dispositivos U2F não certificados**: Podem existir e ser usados, dependendo do serviço, mas os serviços precisam ter a sua própria cadeia de confiança para esses dispositivos.

### FIDO2 and U2F

- **Compatibilidade**: O FIDO2 é compatível retroativamente com dispositivos U2F.

### U2F JS / MessagePort API

- **API JavaScript U2F**: Interface JavaScript usada por páginas web para interagir com dispositivos U2F, utilizando uma API MessagePort.

### WebAuthn

- **WebAuthn**: Parte do framework FIDO2, uma evolução da API U2F, especificada pela W3C e FIDO. Implementada por navegadores, permite lidar com o registo e autenticação de dispositivos U2F.

### Client to Authenticator Protocol (CTAP)

- **CTAP**: Protocolo para interoperabilidade entre uma plataforma de utilizador (e.g., um laptop) e um autenticador criptográfico controlado pelo utilizador. Baseado no padrão de autenticação U2F.

### CTAP variants

- **Variantes do CTAP**:
  - **CTAP1/U2F**: Também conhecido como FIDO U2F, utiliza formato de mensagem bruta.
  - **CTAP2**: Para autenticadores FIDO2 (também conhecidos como WebAuthn), utiliza o formato de serialização de dados CBOR (Concise Binary Object Representation).

### Use case: Passkeys

- **Chaves de Acesso (Passkeys)**:
  - Surgiram para evitar problemas comuns de autenticação, como senhas fracas, phishing, roubo de senhas/cookies, falta de um segundo fator, ataques MITM ou leaks, e custos com o segundo fator.
  - Melhoram a usabilidade, evitando a necessidade de gerar, memorizar e gerir múltiplas senhas.
  - **Definição**: Passkeys são uma tecnologia de autenticação que utiliza material de autenticação do utilizador diretamente no dispositivo, sem ser exposto a terceiros. Gera um par de chaves (pública e privada) para autenticação, onde a chave pública é armazenada no serviço.

### Use case: Passkeys Functionality

- **Funcionamento das Passkeys**:
  - Utilizam material de autenticação do utilizador diretamente no dispositivo, que nunca é exposto a terceiros.
  - Geram um par de chaves, sendo a chave pública armazenada no serviço.
  - A autenticação considera o serviço, dispositivo, chaves e utilizador, implicitamente usando 2FA.
  - **Certificação**: Capacidade de assegurar a proveniência do autenticador, garantindo que ele está realmente a fornecer os dados de autenticação. A chave pública é incluída num objeto de certificação, assinado por uma chave privada.

### Use case: Passkeys Limitations

- **Limitações das Passkeys**:
  - **Suporte de dispositivos**: Tecnologia ainda nova.
  - **Dependência do dispositivo**: As chaves de acesso são específicas do dispositivo e podem não ser funcionais entre diferentes ecossistemas.
  - **Segurança biométrica**: Biometria pode não ser segura contra ataques locais, mas é melhor que apenas senhas.

## Aula 8 - Kerberos e SAML

### Authentication with Trusted Third Parties / KDCs

- Introdução à autenticação com Terceiros de Confiança (TTP) e Centros de Distribuição de Chaves (KDC).

### Shared-key authentication

- **Autenticação com chave partilhada**:
  - **Orientada à conexão** e **sem conexão**.
  - **Problema**: Como distribuir a chave Kab para todos os pares A-B possíveis?

### Authentication with Trusted Third Party: Key Distribution Center (KDC) concept

- **Conceito de KDC**:
  - TTP é responsável por intermediar a comunicação entre pares.
  - A e B não possuem informações partilhadas, mas ambos possuem informações partilhadas com a TTP.

### Why KDC?

- **Porquê KDC?**:
  - Um TTP pode distribuir uma chave de sessão (KAB) para A e B, provando a identidade de cada um.
  - A chave de sessão KAB é temporária (apenas para uma sessão).
  - A e B usam KAB para provar a identidade um do outro de diferentes formas, no início ou durante cada interação da sessão.

### Session key distribution

- **Distribuição de chave de sessão**:
  - A TTP (Terceira Parte Confiável) gera e distribui a chave de sessão KAB.
  - **Processo**:
    1. **A TTP** distribui a chave KAB para A e B.
    2. **B** recebe a chave KAB juntamente com um timestamp TB da TTP.
    3. **B** solicita uma prova de identidade usando a chave KAB.
    4. **A** e **B** utilizam a chave KAB para autenticar a comunicação.
- **Exemplo Visual**:
  - **Passo 1**: A TTP envia a chave KAB para A e B.
  - **Passo 2**: A e B usam KAB para autenticar e proteger suas comunicações.
  - **Detalhes Adicionais**: A imagem no slide ilustra os fluxos de mensagens e como a chave é utilizada para estabelecer confiança entre A e B.

### Example: SAML Web Browser SSO Profile

- **Perfil de SSO (Single Sign-On) do SAML para navegadores**:
  - Processo de autenticação de utilizador com afirmação de identidade SAML, usando cookies de autenticação para manter a sessão.

### Kerberos: Goals

- **Objetivos do Kerberos**:
  - Autenticar pares num ambiente distribuído, inicialmente desenvolvido para o projeto Athena no MIT.
  - Distribuir chaves de sessão para adicionar segurança às sessões entre pares.
  - Objetivos incluem autenticação, confidencialidade (opcional) e SSO (Single Sign-On), permitindo ao utilizador lembrar-se de uma única senha.

### Kerberos background: Needham-Schroeder (1978)

- **Antecedentes do Kerberos**:
  - Baseado no protocolo de Needham-Schroeder.
  - A e B confiam num KDC comum.
  - KDC partilha uma chave com cada A e B, atuando como uma autoridade central de autenticação.

### Kerberos: Architecture and base concepts

- **Arquitetura e conceitos básicos do Kerberos**:
  - Serviços KDC do Kerberos: Serviço de Autenticação (AS) e Servidor de Concessão de Tickets (TGS).
  - Entidades (principais): Todas têm uma chave secreta partilhada com Kerberos (AS ou TGS).
  - Requisitos: Relógios bem sincronizados.
  - Elementos de autenticação: Ticket (necessário para solicitar um serviço) e autenticador (prova da identidade do solicitante).

### Kerberos: Tickets and authenticators

- **Tickets e autenticadores no Kerberos**:
  - **Ticket**: Dado que não pode ser forjado, interpretado apenas pelo serviço alvo, contendo a identidade do cliente e uma chave de sessão.
  - **Autenticador**: Contém um carimbo de tempo do pedido, a identidade do cliente e prova que o cliente conhece a chave de sessão.

### Overview of Kerberos SSO: 1st step: Login

- **Primeiro passo do SSO do Kerberos**:
  - Localização dos servidores Kerberos do domínio.
  - Autenticação do utilizador pelo Kerberos (AS).
  - O utilizador recebe um Ticket Granting Ticket (TGT) e uma chave de sessão (KTGT) para interagir com outro serviço Kerberos (TGS).

### Overview of Kerberos SSO: 2nd step: Authenticated access to servers

- **Segundo passo do SSO do Kerberos**:
  - O utilizador solicita ao Kerberos (TGS) um ticket para acessar um serviço (S).
  - O utilizador usa o TGT no pedido e deve provar que é o proprietário do TGT.
  - Recebe uma chave de sessão (KUS) e um ticket para o serviço (TUS), que é usado para fazer pedidos autenticados ao serviço.

### Kerberos: Protocol (of version V5)

- **Protocolo do Kerberos (versão V5)**:
  - Descreve o fluxo de mensagens e interações entre cliente (C), servidor (S), AS e TGS.

### Kerberos: Pre-authentication alternative

- **Alternativa de pré-autenticação no Kerberos**:
  - Previne ataques de dicionário proativos (Kerberoasting), filtrando pedidos ilegítimos.

### Kerberos: Scalability

- **Escalabilidade do Kerberos**:
  - Domínios de autenticação (realms).
  - Cada domínio tem um servidor Kerberos, com cooperação entre domínios para permitir acesso entre diferentes realms.
  - Chaves secretas partilhadas entre servidores TGS de diferentes domínios, associadas a um caminho de confiança.

### Kerberos V5: Security politics and mechanisms

- **Políticas e mecanismos de segurança do Kerberos V5**:
  - Autenticação de entidades usando chaves secretas, nomes e endereços de rede.
  - Períodos de validade com carimbos de tempo em tickets e autenticadores.
  - Proteções contra repetição usando nonces e carimbos de tempo/números de sequência.
  - Delegação e opções de autorização em tickets.
  - Autenticação entre domínios usando chaves secretas partilhadas e emissão de tickets de um TGS para outro.

### Kerberos: Security issues

- **Questões de segurança do Kerberos**:
  - O KDC pode se fazer passar por qualquer pessoa, necessitando de máxima segurança na sua administração.
  - Pode ser um ponto único de falha, mas a replicação é uma opção.
  - Senha roubada de um utilizador permite a outros fazerem-se passar pela vítima em todos os serviços do domínio.
  - Credenciais TGS roubadas são menos arriscadas, pois sua validade é limitada (geralmente um dia).

### Kerberos V5: Actual availability

- **Disponibilidade atual do Kerberos V5**:
  - Lançamentos do MIT disponíveis em [web.mit.edu/kerberos](http://web.mit.edu/kerberos).
  - Versões para Windows, com componentes modificados para acomodar credenciais do Windows.
  - Componentes incluem servidores/daemons Kerberos, bibliotecas para "kerberizar" aplicações, e aplicações de suporte como klogin, kpasswd, kadmin.
  - Aplicações kerberizadas (clientes e servidores).

## Aula 9 - Gestão de identidade

### Identidade Digital

- **Definição**: Um conjunto arbitrário de atributos de uma entidade, segregados em diferentes contextos.
- **Identificadores Contextuais**: Subconjuntos desses atributos usados para reconhecer a entidade em cada contexto.

### Identity Manager (IdM)

- **Função**: Gerir perfis de identidade em cada contexto.
- **Tarefas**:
  - Criar e eliminar perfis de identidade.
  - Recolher e atualizar atributos nos perfis.
- **Objetivos**: Identificação, autenticação, autorização, controlo de acesso, contabilização, vigilância e rastreamento.

### Identity Provider (IdP)

- **Função**: Fornecer atributos de identidade de um sujeito como afirmações (assertions).
- **Exemplo**: GitHub, Microsoft Azure AD.
- **Princípio**: "Need-to-know", ou seja, fornecer apenas os atributos necessários para cada solicitante, respeitando questões de privacidade.

### Fonte Autorizada

- **Definição**: A principal IdM responsável por fornecer um dado atributo de identidade de um sujeito.
- **Função**: Garantir que há apenas uma fonte autorizada, mesmo que possa ser replicada para redundância.

### Declaração de Identidade

- **Definição**: Uma afirmação que alguém faz sobre a identidade de si próprio ou de outro sujeito.
- **Função das IdMs/IdPs**: Prover conjuntos de declarações de identidade embaladas em afirmações confiáveis.

### Abordagem 1: IdM Isolado ou Orientado a Silo

- **Características**:
  - IdM por serviço, sem relação entre serviços na organização.
  - Atributos de identidade não são partilhados entre serviços, resultando em duplicação.
  - Cada pessoa possui um perfil de identidade em cada serviço.
  - Desafios na integração e remoção de identidades entre serviços.
- **Exemplo Prático**: Uma empresa onde cada aplicação interna (e.g., email, ERP, CRM) requer login separado e não partilha informações de identidade.

### Abordagem 2: IdM Agregado

- **Características**:
  - Um IdM para vários serviços, com um único perfil para cada entidade.
  - Mais eficiente na gestão, integração e remoção de identidades.
  - Utiliza um IdP central para autenticação e fornecimento de afirmações de identidade.
  - Serviços confiam no IdP.
- **Exemplo Prático**: Microsoft Office 365, onde um único login dá acesso a vários serviços (Outlook, Teams, SharePoint) usando Azure AD.

### Abordagem 3: Identidade Federada

- **Conceito**: Políticas, práticas e protocolos comuns para gerir identidade entre organizações.
- **Objetivo**: Permitir que uma entidade aceda a um serviço de outra organização com um conjunto de afirmações de identidade fornecidas por IdMs confiáveis.
- **Exemplo Prático**: eduGAIN, que permite que utilizadores de uma universidade acedam a recursos de outra instituição participante.

### Abordagem 4: Gestão de Identidade Baseada em Declarações

- **Características**:
  - Provisionamento de declarações de identidade por múltiplos IdPs.
  - O fornecedor de serviços solicita vários atributos de identidade como declarações e propõe IdMs alternativos.
  - O cliente do serviço utiliza um ou mais IdMs para obter todas as declarações necessárias.
- **Exemplo Prático**: OpenID Connect, onde utilizadores podem escolher autenticar-se através de Google, Facebook, ou outro provedor OpenID.

### Credenciais

- **Definição**: Conjunto de declarações de identidade de um sujeito, afirmadas por um IdM.
- **Metadados**: Data de emissão, períodos de validade, atributos de identidade do emissor, e propósito da emissão.
- **Exemplo**: Cartões de identidade, certificados digitais.

### Problemas de Privacidade

- **Questões**: Rastreamento, controle da apresentação das credenciais, e necessidade de auditoria.
- **Requisitos**: O proprietário da credencial deve provar a sua posse e controlar a sua apresentação.

### Credenciais Verificáveis (VC)

- **Definição**: Credenciais seladas criptograficamente fornecidas a um detentor, que pode ser verificadas quanto à sua autenticidade, validade e origem.
- **Exemplo**: Certificados de vacinação armazenados em uma blockchain.

### Provas de Conhecimento Zero (ZKP)

- **Definição**: Método que permite a uma entidade A provar a identidade de uma entidade B sem revelar informações adicionais.
- **Exemplo**: Provar que se sabe a localização de "Onde está o Wally?" sem revelar a localização exata.

### Identidade Auto-Soberana (SSI)

- **Definição**: Identidade descentralizada que requer uma carteira digital para guardar credenciais digitais verificáveis.
- **Tipos de Credenciais**:
  - **Credenciais Atestadas por Terceiros**: Verificadas criptograficamente e confiáveis pelo receptor.
  - **Credenciais Auto-Atestadas**: Declarações que um indivíduo faz sobre si próprio.
- **Exemplo Prático**: Soluções de identidade digital como a European Digital Identity Wallet.

### Interoperabilidade

- **Definição**: Capacidade de diferentes sistemas de cooperar, comunicando e entendendo-se mutuamente.
- **Tipos**:
  - **Interoperabilidade Sintática**: Capacidade de comunicar e analisar itens de comunicação.
  - **Interoperabilidade Semântica**: Capacidade de entender a informação trocada corretamente.

### eIDAS

- **Definição**: Regulamento da UE sobre sistemas de identificação eletrónica e serviços de confiança para transações eletrónicas no mercado interno.
- **Objetivo**: Estabelecer normas para assinaturas eletrónicas, certificados, e serviços de confiança.
- **Exemplo**: Utilização de identidades eletrónicas nacionais para aceder a serviços públicos em diferentes países da UE.

## Aula 10 - Anonimato e Privacidade

### Privacidade

- **Definição**: O direito de alguém manter os seus assuntos pessoais e relações em segredo. Inclui o estado de estar sozinho ou de manter informações pessoais conhecidas apenas por um grupo restrito.

### Tipos de Privacidade

- **Física**: Relacionada às propriedades do próprio corpo.
- **Vigilância**: Relacionada ao estado de ser observado.
- **Informação**: Relacionada à forma como as informações sobre si mesmo são manuseadas.

### Modelo de Privacidade Digital IEEE

- **Expectativas de Privacidade (EoP)**: Quando e como os utilizadores esperam privacidade, englobando seis características: Identidades, Comportamentos, Inferências, Transações, Confidencialidade & Integridade, Acesso & Observabilidade.
- **Influências na Privacidade (IoP)**: Influências que moldam a infraestrutura de privacidade digital, incluindo influências técnicas, regulatórias, económicas, legislativas, legais, individuais, sociais e culturais.

### Privacidade e Tecnologia

- **Problemas**: O uso da tecnologia cria informações (dados e metadados), processadas rapidamente e em grande volume, que podem ser vazadas.
- **Dilema**: É possível usar tecnologia sem fornecer dados pessoais?

### Privacidade e Empresas

- **Necessidade de Dados**: As empresas precisam de dados para modelos de negócio (financeiros, marketing, transacionais).
- **Compromisso da Privacidade**: A privacidade é frequentemente comprometida para fornecer produtos, causando potencial impacto legal e na perceção da marca pelos utilizadores.

### Privacidade e IAA (Identificação, Autenticação e Autorização)

- **Conexão**: A privacidade está fortemente ligada aos métodos e tecnologias de IAA, que lidam com utilizadores, seus atributos e relações.

### Identificação

- **Relevância da Privacidade**: Os dados de identificação podem revelar informações adicionais, facilitando rastreamento, roubo de identidade e outras ameaças.
- **Melhores Práticas**: Identificadores devem ser específicos do serviço, únicos dentro dos limites de usabilidade, e não devem revelar informações adicionais.

### Autenticação

- **Relevância da Privacidade**: Os dados de autenticação podem revelar informações pessoais adicionais e comportamentais, que podem ser usados para rastreamento e outras ameaças.
- **Melhores Práticas**: Dados de autenticação devem ser manuseados de acordo com o GDPR, com práticas claras de processamento de dados e consentimento do utilizador.

### Anonimato

- **Definição**: O estado de não ser observável dentro de um conjunto de sujeitos, definido pelo conjunto de anonimato.
- **Conceito Dependente do Contexto**: O contexto define o conjunto de anonimato em relação a uma ação particular.

### Problemas de Privacidade de Microdados

- **Microdados**: Informações ao nível de respondentes individuais.
- **Problemas**: Como compartilhar microdados sem expor a identidade das pessoas que os forneceram?

### Melhorias na Privacidade de Microdados

- **Remoção de IDs Potencialmente Únicos**: Remover identificadores únicos (nomes, IDs nacionais, números de telefone, etc.) para evitar a ligação de microdados entre várias bases de dados.
- **Adição de Ruído**: Adicionar ruído aos dados armazenados ou aos resultados das consultas para aumentar a privacidade, embora comprometa a integridade.
- **Truncamento**: Não fornecer dados completos, limitando a precisão para aumentar a privacidade.

### K-Anonimato

- **Definição**: Nenhuma consulta pode devolver um conjunto de anonimato com menos de k entradas.
- **Atributos Críticos**: Identificadores únicos, quase-identificadores (quando combinados produzem tuplas únicas) e atributos sensíveis.
- **Exemplo Prático**:
  - **Dados Originais**:

| Nome     | Idade | Sexo | Código Postal | Doença          |
|----------|-------|------|---------------|-----------------|
| Sam      | 29    | M    | 43102         | Diabetes        |
| Gloria   | 38    | F    | 43102         | Cancro da Mama  |
| Adam     | 51    | M    | 43102         | Cancro do Cólon |
| Eric     | 29    | M    | 43102         | Diabetes        |
| Tanisha  | 34    | F    | 43102         | HIV             |
| Don      | 51    | M    | 43102         | Doença Cardíaca |
  - **Após Remoção de Identificadores Únicos**:

| Idade | Sexo | Código Postal | Doença          |
|-------|------|---------------|-----------------|
| 29    | M    | 43102         | Diabetes        |
| 38    | F    | 43102         | Cancro da Mama  |
| 51    | M    | 43102         | Cancro do Cólon |
| 29    | M    | 43102         | Diabetes        |
| 34    | F    | 43102         | HIV             |
| 51    | M    | 43102         | Doença Cardíaca |
  - **Generalização para 2-anonimato**:

| Idade | Sexo | Código Postal | Doença          |
|-------|------|---------------|-----------------|
| 30    | M    | 43102         | Diabetes        |
| 40    | F    | 43102         | Cancro da Mama  |
| 50    | M    | 43102         | Cancro do Cólon |
| 30    | M    | 43102         | Diabetes        |
| 30    | F    | 43102         | HIV             |
| 50    | M    | 43102         | Doença Cardíaca |

### L-Diversidade

- **Problema com K-Anonimato**: Vulnerável a ataques de homogeneidade e conhecimento prévio.
- **Solução**: L-diversidade, onde os resultados de uma consulta devem conter pelo menos l valores diferentes para cada atributo sensível.
- **Exemplo**:
  - **2-anonimidade com 1-diversidade**:

| Idade | Sexo | Código Postal | Doença          |
|-------|------|---------------|-----------------|
| 30    | M    | 43102         | Diabetes        |
| 40    | F    | 43102         | Cancro da Mama  |
| 50    | M    | 43102         | Cancro do Cólon |
| 30    | M    | 43102         | Diabetes        |
| 30    | F    | 43102         | HIV             |
| 50    | M    | 43102         | Doença Cardíaca |
  - **2-anonimidade com 2-diversidade**:

| Idade | Sexo | Código Postal | Doença          |
|-------|------|---------------|-----------------|
| 30    | M    | 43102         | Diabetes        |
| 40    | F    | 43102         | Cancro da Mama  |
| 50    | M    | 43102         | Cancro do Cólon |
| 30    | M    | 43102         | Diabetes        |
| 30    | F    | 43102         | HIV             |
| 50    | M    | 43102         | Doença Cardíaca |

### Conclusão

- **Limitações**: Tanto k-anonimidade quanto l-diversidade têm falhas, sendo vulneráveis a vários tipos de ataques, como homogeneidade, conhecimento prévio, enviesamento e similaridade.
- **Exemplo de Ataque de Homogeneidade**: Se um atacante souber que Bob tem 27 anos e mora no código postal 47678, pode concluir que Bob tem doença cardíaca.
- **Exemplo de Ataque de Similaridade**: Se um atacante souber que Bob tem um salário baixo (3k-5k), pode inferir que ele tem uma doença relacionada ao estômago.