## CIA Triad

É um modelo guia que representa os três principais objetivos da segurança da informação:

- **Confidencialidade**: A informação só é acessível a quem tem permissão para a ver;
- **Integridade**: A informação não é alterada por quem não tem permissão para o fazer;
- **Disponibilidade**: A informação está disponível para quem tem permissão para a ver.

> [!note] 
> Também, o **não repúdio** que assegura que a pessoa que enviou essa informação não pode negar o envio da mesma.

## Protocolos AAA - Autenticação, Autorização, Contabilidade (Accounting)

Para um melhor controlo de acesso a um sistema, é necessário ter em conta a seguinte estrutura:
- **Autenticação**: Acesso a uma parte do sistema
- **Autorização**: Privilégios do utilizador
- **Contabilidade**: Gestão de registos das ações do utilizador do sistema

## Processos de Desenvolvimento de Software Seguro

As preocupações com a segurança devem ser consideradas desde do processo de desenvolvimento. A segurança deve ser uma
preocupação de todos os intervenientes no processo de desenvolvimento de software.

Exemplos de processos de desenvolvimento de software seguro:

- Microsoft SDL (Security Development Lifecycle);
- Software Security Touchpoints;
- Software Assurance Forum for Excellence in Code (SAFECode);

### Microsoft SDL (Security Development Lifecycle)

É uma abordagem de desenvolvimento de software que ajuda a reduzir as vulnerabilidades de segurança dos produtos de
software durante o desenvolvimento.

É composto pelas seguintes fases:

1. Educação e sensibilização:
    - Recolha de requisitos de segurança;
    - Formação em segurança para os colaboradores;
2. Início do projeto
3. Análise e requisitos:
    - Threat modeling;
    - Requisitos de segurança;
4. Conceção arquitetónica e detalhada
5. Implementação e testes:
    - Análise de testes de segurança;
6. Release, deploy e suporte:
    - Processos de resposta a incidentes;

### Software Security Touchpoints

É um processo de desenvolvimento de software seguro que se baseia em 4 princípios:

1. **Security is a process, not a product**: A segurança deve ser considerada durante todo o ciclo de vida do software;
2. **Security is a lifecycle concern**: A segurança deve ser considerada em todas as fases do ciclo de vida do software;
3. **Security is a people concern**: A segurança deve ser uma preocupação de todos os intervenientes no processo de
   desenvolvimento de software;
4. **Security is a technology concern**: A segurança deve ser considerada em todas as tecnologias utilizadas no
   desenvolvimento de software;

Elementos chave do Software Security Touchpoints:

1. Rever código (com ou sem ferramentas)
2. Análise do risco arquitetónico
3. Testes de penetração de software
4. Testes com base no risco de segurança
5. Casos de abuso (ex.: inserção inválida de datas/outro tipo de entrada)
6. Requisitos de segurança
7. Operações de segurança (não apenas a nível de software)

## Thread Modelling

O Threat Modelling é uma técnica que permite identificar, classificar e priorizar as ameaças a um sistema de informação.

Permite também ajudar a listas os ativos/componentes presentes no sistema, identificando as ameaças que podem afetar
esses ativos.

Existem várias metodologias de Threat Modelling, sendo as mais conhecidas:

- STRIDE;
- DREAD (Damage, Reproducibility, Exploitability, Affected users, Discoverability);
- PASTA (Process for Attack Simulation and Threat Analysis);

Ferramentas como
o [Microsoft Threat Modelling](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool-getting-started)
Tool permitem a criação de modelos de ameaças.

### STRIDE

É bastante útil na enumeração de ameaças a um sistema de informação.

Cada letra do acrónimo STRIDE representa um tipo de ameaça:

- Spoofing: Falsificação de identidade (Autenticação);
- Tampering: Alteração de dados (Integridade);
- Repudiation: Capacidade de negar a autoria de uma ação (Não repúdio);
- Information Disclosure: Divulgação de informação sensível (Confidencialidade);
- Denial of Service: Indisponibilidade de um serviço (Disponibilidade);
- Elevation of Privilege: Aumento de privilégios (Autorização);

## CI/CD (Continuous Integration/Continuous Deployment)

É a passagem do ambiente de desenvolvimento para produção de forma automática.

*Continuous Integration*, é na prática:

- Agregar o código de todos os desenvolvedores num repositório partilhado;
- Deteção de bugs/conflitos mais cedo;

*Continuous Deployment*, é na prática:

- Automatizar o processo de deploy de aplicações para ambientes de teste, staging e produção;
- Testes automatizados e verificação de qualidade;

## Quality Attributes

Os quality attributes são características de um sistema que são importantes para os stakeholders.

Podem ser:

- Estáticos: Representam a qualidade da estrutura do sistema, como:
  - Testável: Facilidade de testar o sistema;
  - Manutenção: Facilidade de manter o sistema;
  - Reusabilidade: Facilidade de reutilizar partes do sistema noutros sistemas;
  - Modularidade: Facilidade de alterar partes do sistema;
  - Extensibilidade: Facilidade de adicionar novas funcionalidades ao sistema;
- Dinâmicos: Representam o comportamento do sistema em determinadas circunstâncias, como:
  - Robustez: Capacidade de lidar com situações inesperadas;
  - Escalabilidade: Capacidade de lidar com um aumento de carga;
  - Tolerância a falhas: Capacidade de continuar a funcionar mesmo com falhas;
  - Latência: Tempo de resposta do sistema;
  - Produtividade: Rentabilidade do sistema;

A nível de segurança, estes atributos são o foco:

- Confidencialidade: A informação só é acessível a quem tem permissão para a ver;
- Integridade: A informação não é alterada por quem não tem permissão para o fazer;
- Não repúdio: Garantir que uma entidade não pode negar a autoria de uma ação;
- Responsabilidade: Garantir que as ações de uma entidade são atribuídas a essa entidade;
- Autenticidade: Garantir que a entidade é quem diz ser.
- Compliance: Garantir que a aplicação cumpre com as normas e regulamentos aplicáveis.

## Requisitos de Segurança

Representam as necessidades de segurança de um sistema de informação.

Podem ser:

- **Requisitos de segurança funcionais**: Capacidade para o sistema se proteger a si próprio.
  - Exemplo: Todos os utilizadores devem autenticar-se antes de aceder ao sistema;
- **Requisitos de segurança não funcionais**: Comportamento de segurança, força de desempenho, características e
  atributos de qualidade.
  - Exemplo: O sistema deve ser capaz de lidar com 1000 pedidos por segundo;
- **Requisitos de garantia (*assurance*) de segurança**: Técnicas e métodos para verificar que os requisitos funcionais
  e não funcionais são cumpridos.
  - Exemplo: O sistema deve ser testado por um especialista em segurança;

Os requisitos de segurança devem ser:

- **Claros**: A intenção deve ser de fácil compreensão;
- **Concisos**: Deve ser curto e direto;
- **Espécificos**: Em requisitos que quantificam, o valor deve ser definido;

### Medidas de segurança e mecanismos associados

![[Primeiro Ano/Primeiro Semestre/Software Robusto/imgs/securitymeasures.png]]

### Exemplos de Requisitos de Segurança
![[Primeiro Ano/Primeiro Semestre/Software Robusto/imgs/examplerequirements1.png]]

![[Primeiro Ano/Primeiro Semestre/Software Robusto/imgs/examplerequirements2.png]]

## Análise de Segurança

### Fuzzing (Fuzz Testing)

É uma técnica de teste de software que consiste em fornecer dados inválidos, inesperados ou aleatórios como entrada a um
programa de computador.

Exemplo:

- Se tivermos o seguinte pedido HTTP: `GET /index.html HTTP/1.1`
- Podemos tentar enviar um pedido com um URL gerado aleatoriamente: `GET /////index.html HTTP/1.1`

Para isso é necessário:

- Indentificar o alvo;
- Identificar o input;
- Gerar os dados de teste;
- Executar o teste;
- Monitorizar o comportamento do sistema;
- Detetar falhas.

### Static Analysis security testing (SAST)

Consiste na análise do código fonte de uma aplicação para detetar problemas de segurança.

Pontos fortes:

- Cobertura completa do código (em teoria)
- Verifica potencialmente a ausência/comunicação de todas as instâncias de toda a classe de erros
- Deteta erros diferentes da análise dinâmica
- Análise repetível

Pontos fracos:

- Taxas elevadas de falsos positivos
- Muitas propriedades não podem ser facilmente modeladas - Difícil de construir
- Quase nunca tem todo o código fonte em sistemas reais (sistema operativo, bibliotecas partilhadas, carregamento
  dinâmico, etc.)

### Dynamic Analysis security testing (DAST)

- Verificação em tempo de execução de software compilado ou packaged para verificar a funcionalidade que só é aparente
  quando todos os componentes estão integrados e a funcionar.
- Utilização de um conjunto de ataques pré-construídos e strings malformadas que podem detetar corrupção de memória,
  problemas de privilégio do utilizador, ataques de injeção e outros problemas críticos de segurança.
- Pode utilizar o fuzzing, uma técnica automatizada de introdução de casos de teste conhecidos, inválidos e inesperados
  numa aplicação, frequentemente em grande volume.

### Penetration Testing

É uma técnica de teste de segurança que envolve a simulação de ataques de um atacante malicioso a um sistema de
computador para avaliar a segurança do sistema.

Por norma, *Penetration Testing* usa três tipos de abordagens:

- *exploits*: code que é executado para explorar uma vulnerabilidade (ex.: buffer overflow);
- *payloads*: código que é executado após a exploração de uma vulnerabilidade (ex.: shellcode);
- *auxiliary*: código que é executado para ajudar a explorar uma vulnerabilidade (ex.: scanners de versões);

## Ataques Comuns

### Secure Coding Practices

1. **Input Validation**: Validar a entrada do utilizador;
2. **Heed compiler warnings**: Prestar atenção às mensagens de aviso do compilador;
3. **Architect and design for security policies**: Definir políticas de segurança com base nas necessidades do sistema;
4. **Keep it simple**: Evitar complexidade desnecessária que pode aumentar a probabilidade de erros feitos na sua
   implementação;
5. **Default deny**: Definir sempre uma política de negação por defeito;

### 7 Pernitious Kingdoms

Os 7 Pernicious Kingdoms são uma classificação de erros de programação que podem levar a vulnerabilidades de segurança.

1. Input Validation and Representation
2. API Abuse
3. Security Features
4. Time and State
5. Error Handling
6. Code Quality: Insecure Coding Practices
7. Encapsulation: Proteção de dados
8. Environment (+1)

## Safety e Security

### Safety

"*'Safety' indicates a state of being safe or protected from harm or danger.*"

Exemplos:

- **Deteção de fumo**: Avisar os ocupantes de um edifício de um incêndio;
- **Portas dos comboios**: Garantir que as portas dos comboios estão fechadas antes de o comboio partir;

### Security

"*'Security' refers to protective measures against threats or dangers, often physical in nature.*"

Exemplos:

- **Câmaras de vigilância**: Monitorizar a atividade de um local;
- **Firewall**: Proteger uma rede de computadores de acessos não autorizados;

### Safety Standards

Three clear examples of industries that rely on safety:

Três exemplos de indústrias que dependem da safety:

- Automotive (Automóvel):
  - ISO 26262, "Road vehicles – Functional safety"
- Aeronautics (Aeronáutica):
  - DO-178C, “Software Considerations in Airborne Systems and Equipment Certification”
- Railway (Ferroviário):
  - CENELEC EN 50128, “Railway applications - Communication, signalling and processing systems - Software for railway
      control and protection systems”

### Hazard Analysis

É o processo de identificação dos perigos que podem potencialmente surgir num sistema ou ambiente, documentando as suas
consequências indesejadas e analisando as suas causas subjacentes.

Tem como objetivo identificar:

- Perigos;
- Causas dos perigos;
- Consequências dos perigos;
- Medidas de mitigação dos perigos;
- Medidas de controlo dos perigos;