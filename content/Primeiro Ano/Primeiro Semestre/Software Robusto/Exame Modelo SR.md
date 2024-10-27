## Exemplo de Frequência + Soluções

O pessoal da EDP pretende ter acesso a um portal quando estão quer na empresa quer no terreno a efetuar instalações,
manutenções ou a corrigir problemas.

Neste contexto, o SecureSmartMeter foi contratado à tua empresa.

Ficará em <https://securesmartmeter.pt> e será apenas acessível para funcionários credenciados da EDP e os
subempreiteiros da EDP que efetuam trabalhos no terreno.

O que se pretende com este portal é dar, em tempo real, acesso às informações de todo e qualquer Smart Meter de energia
da rede da EDP, o portal deve permitir o acesso aos detalhes do Smart Meter (configurações, estado, versões, consumo
actual, hora, última atualização, detalhes do utilizador do serviço ...).

Esta informação deve ser complementada pela informação de histórico de cada Smart Meter que está centralizada na EDP.
Esta informação, acessível por internet através de um interface que pode ser explorado por webservices, existe em duas
bases de dados redundantes e contém o histórico de consumos, pagamentos, utilizações, alterações e manutenções, alarmes
e outras operações associadas a cada Smart Meter.

Se o primeiro caso é, geralmente mais interessante para os funcionários que se deslocam ao terreno, a segunda base de
dados não é menos interessante pois apresenta tendências de consumo, e pode permitir a identificação de utilização
fraudulenta dos equipamentos. Estes dados ficam registados sem cifragem pois a EDP pretende correr aplicações de
monitorização permanente de fraude e que exigem muito processamento não podendo suportar encriptação, estas aplicações
devem ser integradas no SafeSmartMeter e deves também implementar o envio de mensagens (email configurável) quando uma
certa tendência ou um alarme de fraude for detetado.

Há ainda, estranhamente, um requisito pedido a possibilidade de fazer o reset aos dados de um determinado Smart Meter
pelo funcionário (sem mais restrições para este reset), para reiniciar um serviço com um novo cliente ou para corrigir
problemas com determinado Smart Meter – A tua empresa tem levantado dúvidas relativamente a esta funcionalidade, que
apenas de ficar registado quem efetuou o reset dos dados, os mesmos acabam por ficar perdidos para sempre, podendo
levar a situações fraudulentas camufladas.

1. Pergunta:

a. Lista 3 razões pelas quais, para este projeto em específico, é importantíssimo considerar a formação da equipa de
projeto na área de cibersegurança e efetuar análises de "Threat Modelling" (dando, por exemplo, um exemplo para cada
razão).

R:

É de extrema importância considerar a formação da equipa de projeto na área de cibersegurança e efetuar análises de "
Threat Modelling", pois:

- Os requisitos de segurança têm de ser muito bem definidos, pois este portal trabalha com informação sensível que
  envolvem operações sobre dados que podem afetar a integridade do sistema.
- A equipa do projeto tem de tomar em conta na sua implementação a situação onde um funcionário é vítima de uma campanha
  de phishing, de modo a ter um sistema mais seguro a falsificação de identidade.
- A equipa tem de ter em conta na sua implementação, um modo de combater ataques de negação de serviço, pois este portal
  tem que estar sempre ativo para que os funcionários que não se encontram no terreno possam fazer as devidas
  manutenções.

b. Identifica 3 tópicos (assuntos) que deveriam fazer parte do Processo de Resposta a Incidentes que deve ser definido
no final do projeto.

R:

No processo de resposta a incidentes, deve ser definido:

Deteção de Atividades Suspeitas: Estabelecer processos para monitorizar e detetar atividades suspeitas no portal, como
múltiplos acessos não autorizados ou tentativas de reset excessivas. Definir procedimentos claros para investigação e
resposta a esses incidentes.

Gestão de Logs e Auditoria: Implementar um sistema robusto de logs que registe todas as ações realizadas no portal,
incluindo resets de dados. Desenvolver procedimentos para revisão periódica de logs e auditorias internas para
identificar padrões incomuns que possam indicar atividades fraudulentas.

Resposta a Incidentes de Fraude: Estabelecer um protocolo claro para responder a incidentes de fraude detetados,
incluindo a comunicação rápida com as partes interessadas, a revisão detalhada das atividades suspeitas e a
implementação de medidas corretivas, como o bloqueio de acessos ou a revogação de privilégios de reset de dados.

2. Considerando uma análise de ameaças de segurança (threats analysis) aplicável a este sistema:

a. Identifica os principais atributos de segurança que se devem ter em conta neste caso (o que é mais importante), e explica brevemente cada um deles com um exemplo para cada um (3 atributos no mínimo, 6, no máximo). Considera pelo menos os atributos CIA.

R:

- Confidencialidade: Garante que apenas as partes autorizadas tenham acesso a informações sensíveis. Pois na gestão do histórico do Smart Meter, é crucial assegurar que apenas funcionários credenciados da EDP e subempreiteiros autorizados tenham acesso às informações detalhadas do consumo. Implementar controles de acesso rigorosos e criptografia de dados contribui para a confidencialidade.
- Integridade: Garante que os dados permaneçam precisos, completos e não sejam alterados indevidamente. O risco de manipulação de dados ao realizar um reset em um Smart Meter é uma ameaça à integridade. Para mitigar isso, é essencial implementar logs detalhados que registem todas as ações realizadas no sistema. Além disso, a autenticação forte para realizar operações críticas, como o reset de dados, ajuda a garantir a integridade dos dados.
- Disponibilidade: Garante que os serviços e dados estejam disponíveis quando necessário, sem interrupções indevidas. A disponibilidade é crucial para garantir que os funcionários da EDP acessem o portal SecureSmartMeter em tempo real durante instalações ou manutenções. Medidas como redundância de servidores, sistemas de backup e planos de recuperação de desastres garantem a disponibilidade contínua do sistema, mesmo em situações adversas.

b. Dá um exemplo de como se poderia monitorizar a Disponibilidade do sistema de forma eficaz. (Podes apresentar uma proposta de solução, arquitetura ou procedimentos...)

R: Implementar um sistema de balanceamento de carga para distribuir o tráfego entre servidores e granularidade nas bases de dados. Além disso, utilizar servidores redundantes e configurar failovers garante que, se um servidor falhar, o tráfego seja automaticamente redirecionado para um servidor funcional, minimizando o impacto. Utilização de sistemas de deteção de intrusão (IDS) de modo a procurar por anomalias no portal, como interseções de informação (pois os dados presentes nas bases de dados não se encontram cifrados), e definição de regras no firewall do portal.

Adicionalmente, para monitorizar a disponibilidade do sistema, é necessário implementar ferramentas de monitorização contínua que verifiquem o estado dos servidores e serviços em tempo real. Estas ferramentas devem ser configuradas para enviar alertas imediatos em caso de falhas ou degradação de desempenho, permitindo uma resposta rápida e eficaz para manter a continuidade do serviço.

c. Identifica uma vulnerabilidade (genérica) que poderia ser analisada para as possíveis tecnologias envolvidas.

R: Uma vulnerabilidade que poderia ser analisada dentro deste âmbito, seria SQLi (SQL injection), dado à importância dos dados do mesmo e do facto de eles encontrarem-se armazenados em texto limpo.

3. A FMEA é uma técnica para analisar concretamente modos de falha, e quais seriam as causas, efeitos, o método de deteção e possíveis alterações ao sistema para reduzir o impacto das falhas individuais.

Para o sistema a desenvolver, identifica 3 funções com impacto na segurança do sistema (por exemplo "Autenticar utilizador", “Fazer o log de operações críticas”, “emitir um alarme”) e analisa para cada função, com os modos de falha básicos (função não executada, função tardiamente executada e função mal executada), quais seriam:

- Possíveis métodos de deteção das falhas,
- Efeitos previstos se as falhas não forem eliminadas, e
- Uma sugestão para eliminar as falhas ou para controlar os seus efeitos.

R:

- Autenticar o Utilizador:
  - Modo de Falha 1: Função Não Executada
    - Métodos de Deteção: Monitorização de logs de sistema para verificar a ausência de tentativas de autenticação bem-sucedidas, alertas para a ausência de atividades de autenticação.
    - Efeitos Previstos: A não autenticação de nenhum utilizador, impossibilitando o acesso ao sistema. Se o princípio de fail-secure for aplicado, o sistema permanecerá inacessível para proteger a confidencialidade e integridade dos dados.
    - Sugestão de Eliminação/Controlo: Implementação de mecanismos de verificação periódica da funcionalidade do sistema de autenticação e autenticação de dois fatores para camadas adicionais de segurança. Além disso, garantir que existem procedimentos de fallback seguros para situações onde a função de autenticação falhe.
  - Modo de Falha 2: Função Tardiamente Executada
    - Métodos de Deteção: Registo de eventos com timestamp para detetar atrasos anormais no processo de autenticação.
    - Efeitos Previstos: Atrasos no acesso ao sistema, possivelmente resultando em frustração do utilizador e aumentando o risco de ataques de força bruta.
    - Sugestão de Eliminação/Controlo: Otimização do processo de autenticação, garantindo tempos de resposta aceitáveis. Implementação de caches de autenticação para reduzir a latência.
  - Modo de Falha 3: Função Mal Executada
    - Métodos de Deteção: Análise de logs para identificar padrões de comportamento anormal durante a autenticação.
    - Efeitos Previstos: Autenticação incorreta, permitindo acesso não autorizado ou negando acesso a utilizadores legítimos.
    - Sugestão de Eliminação/Controlo: Melhoria nos algoritmos de autenticação, incluindo a adoção de métodos mais seguros e a validação adequada de entradas.
- Efetuar o Log do Histórico de Consumo:
  - Modo de Falha 1: Função Não Executada
    - Métodos de Deteção: Monitorização proativa dos logs para identificar lacunas nas entradas de histórico.
    - Efeitos Previstos: Perda de dados históricos essenciais para análises de consumo e tendências.
    - Sugestão de Eliminação/Controlo: Implementação de mecanismos de redundância nos logs e processos automatizados para alertar quando ocorrerem lacunas.
  - Modo de Falha 2: Função Tardiamente Executada
    - Métodos de Deteção: Comparação entre o timestamp esperado e o timestamp real nas entradas de log.
    - Efeitos Previstos: Atrasos na atualização do histórico, prejudicando a análise em tempo real e a deteção precoce de anomalias.
    - Sugestão de Eliminação/Controlo: Otimização dos processos de log e utilização de técnicas de paralelização para melhorar a eficiência.
  - Modo de Falha 3: Função Mal Executada
    - Métodos de Deteção: Análise automática de anomalias nos padrões de consumo registados.
    - Efeitos Previstos: Dados de consumo incorretos, comprometendo a precisão das análises e deteção de fraudes.
    - Sugestão de Eliminação/Controlo: Implementação de validações de integridade nos dados de consumo e deteção automática de padrões suspeitos.
- Efetuar Reset de um Smart Meter:
  - Modo de Falha 1: Função Não Executada
    - Métodos de Deteção: Registo de eventos associados ao pedido de reset não processado.
    - Efeitos Previstos: Incapacidade de reiniciar um serviço ou corrigir problemas em Smart Meters, impactando as operações no terreno.
    - Sugestão de Eliminação/Controlo: Implementação de procedimentos de gestão de filas de pedidos para garantir que todos os resets solicitados sejam processados.
  - Modo de Falha 2: Função Tardiamente Executada
    - Métodos de Deteção: Comparação entre o timestamp esperado e o timestamp real para o reset.
    - Efeitos Previstos: Atrasos na execução de resets, afetando a eficiência das operações no terreno.
    - Sugestão de Eliminação/Controlo: Otimização do processo de reset e utilização de notificações automáticas para informar sobre o estado do pedido.
  - Modo de Falha 3: Função Mal Executada
    - Métodos de Deteção: Monitorização de logs para identificar padrões suspeitos ou resets inesperados.
    - Efeitos Previstos: Possíveis ações fraudulentas ou reinicializações indevidas de serviços.
    - Sugestão de Eliminação/Controlo: Implementação de autenticação adicional para realizar operações sensíveis, além de revisão rigorosa dos logs para identificar atividades suspeitas.

4. Descrever 6 requisitos relacionados com a segurança funcional do sistema. Caso a descrição do sistema a desenvolver não permita identificar claramente requisitos fazer pressupostos (o cliente na maioria das vezes não faz bem ideia do que precisa, é perfeitamente normal fazer propostas lógicas e com sentido).

Para cada requisito identificar quais os atributos de segurança que estão relacionados, garantido que existe pelo menos um requisito relacionado com o atributo "Integridade/Integrity".

R:

**REQ-01:** O sistema deve garantir a integridade dos dados armazenados, processados e transmitidos, prevenindo alterações não autorizadas. Isso inclui a proteção contra qualquer forma de corrupção, manipulação ou destruição não autorizada dos dados.

**Atributos de Segurança Relacionados:** Integridade, Autenticidade.

**REQ-02:** O sistema deve atribuir e gerir permissões e acessos de forma precisa e auditável, assegurando que cada utilizador tem apenas as autorizações necessárias para realizar as suas funções específicas. Isso inclui a capacidade de revogar rapidamente privilégios de utilizadores que não necessitam mais de acesso, com base em mudanças de função ou desligamento.

**Atributos de Segurança Relacionados:** Responsabilidade, Controlo de Acesso.

**REQ-03:** O sistema deve garantir a confidencialidade das informações sensíveis, assegurando que apenas utilizadores autorizados têm acesso a esses dados. Informações sensíveis incluem dados pessoais, financeiros, e qualquer outro dado que, se divulgado indevidamente, possa comprometer a privacidade ou segurança da organização. Mesmo utilizadores autorizados devem ter acesso limitado baseado no princípio do menor privilégio.

**Atributos de Segurança Relacionados:** Confidencialidade, Controlo de Acesso.

**REQ-04:** O sistema deve garantir a disponibilidade contínua dos serviços críticos, definidos como aqueles que são essenciais para a operação diária da organização. Deve minimizar o tempo de inatividade para não mais que X horas por ano (onde X deve ser especificado de acordo com as necessidades da organização), assegurando que os utilizadores autorizados tenham acesso ao sistema quando necessário.

**Atributos de Segurança Relacionados:** Disponibilidade, Continuidade de Serviço.

**REQ-05:** O sistema deve manter registos detalhados de todas as atividades relevantes, incluindo autenticações, alterações de permissões e eventos críticos como tentativas de acesso não autorizado e falhas do sistema. Estes registos devem incluir detalhes como identidades dos utilizadores, timestamps, ações realizadas e resultados dessas ações. Os registos devem ser monitorizáveis para permitir a deteção de comportamentos anómalos ou tentativas de violação de segurança.

**Atributos de Segurança Relacionados:** Integridade, Auditoria, Não Repúdio.

**REQ-06:** O sistema deve ter procedimentos claros e eficazes para a resposta a incidentes de segurança. Isso inclui a identificação, análise e mitigação rápida de incidentes, bem como a comunicação transparente com as partes interessadas. A eficácia desses procedimentos deve ser avaliada através de testes regulares e revisões pós-incidente para garantir que eles são capazes de lidar com diferentes tipos de ameaças e responder adequadamente.

**Atributos de Segurança Relacionados:** Disponibilidade, Resposta a Incidentes.

5. Definir um conjunto de testes (sob a forma de uma especificação simples) para confirmar a correta implementação dos requisitos que especificaste para o sistema. Mapear cada caso de teste ao(s) respetivo(s) requisito(s).

Nota: Exemplo de especificação simples:

Testar que no momento de registo de um novo utilizador, o mesmo recebe um email para confirmar o seu registo em menos de 5 minutos. Caso o mesmo nunca receber o email o registo fica pendente. Caso o email chegue depois de 5 minutos, o registo não deve ser confirmado e um novo email deve ser gerado.

Nota: Um requisito pode perfeitamente ser não testável de forma dinâmica, nesse caso apresenta como o mesmo poderá ser verificado.

R:

**TST-01:** Testar a capacidade do sistema de garantir a integridade dos dados armazenados, processados e transmitidos, prevenindo alterações não autorizadas. Deve ser testado efetuando várias modificações de diferentes tipos (ex.: alteração de dados, deleção de dados, inserção de dados) e verificar se o sistema bloqueia cada tipo de alteração não autorizada. O sistema deve prevenir todas as alterações não autorizadas e manter a integridade dos dados.

**TST-02:** Testar a capacidade do sistema de atribuir e gerir permissões e acessos de forma precisa e auditável, garantindo que cada utilizador tem apenas as autorizações necessárias. Deve ser testado atribuindo permissões específicas a diferentes tipos de utilizadores (administradores, utilizadores comuns, convidados) e verificar se o sistema as aplica corretamente. Cada utilizador deve ter acesso apenas às funcionalidades autorizadas e restrições aplicáveis ao seu perfil.

**TST-03:** Testar a capacidade do sistema de garantir a confidencialidade das informações sensíveis, assegurando que apenas utilizadores autorizados têm acesso a dados sensíveis. Deve ser testado tentando efetuar o acesso a dados confidenciais sem as devidas permissões, usando perfis de utilizador com diferentes níveis de acesso. O sistema deve negar o acesso a dados sensíveis para qualquer utilizador sem autorização adequada.

**TST-04:** Testar a capacidade do sistema de garantir a disponibilidade contínua dos serviços críticos. Deve ser testado gerando uma sobrecarga simulada e verificando como o sistema responde, incluindo cenários de falha como quedas de rede ou falhas de hardware. O sistema deve manter a disponibilidade e responder de maneira adequada, minimizando o tempo de inatividade e assegurando a continuidade do serviço. O tempo de resposta deve ser medido e comparado com os objetivos de desempenho definidos (ex.: tempo máximo de inatividade permitido).

**TST-05:** Testar a capacidade do sistema de manter registos detalhados de atividades relevantes, permitindo a deteção de comportamentos anómalos ou tentativas de violação. Deve ser testado realizando diversas tentativas de violação e comportamentos anómalos (ex.: tentativas de acesso não autorizado, modificações de dados sem permissão, falhas de autenticação) e verificar se o sistema regista todas as atividades. O sistema deve registar cada tentativa de violação ou comportamento anómalo para posterior auditoria.

**TST-06:** Testar os procedimentos de resposta a incidentes do sistema. Deve ser testado simulando diferentes tipos de incidentes de segurança (ex.: ataque de malware, tentativa de invasão, falha de sistema) e verificar como o sistema responde. O sistema deve ser capaz de identificar, analisar e mitigar rapidamente cada tipo de incidente, com comunicação transparente às partes interessadas. A eficácia dos procedimentos deve ser avaliada através de revisões pós-incidente e testes regulares.

6. Para testar a robustez da solução, foi planeado efetuar alguns testes de Fuzzing e contratar um especialista para executar Penetration Testing ao sistema, nesse sentido:

a. Lista duas vantagens em fazer Fuzzy testing no contexto da solução. (podes identificar dois exemplos do que poderia ser encontrado com Fuzzy testing)

R: Fazer Fuzzy testing no contexto da solução tem as seguintes vantagens:

Gera automaticamente casos de teste, facilitando a deteção dos mesmos: A introduzir entradas inesperadas, como formatos de dados não convencionais ou tamanhos extremos, o Fuzzing pode revelar vulnerabilidades na validação e processamento de informações.
A aplicação é monitorizada para erros, tendo uma melhor ideia como depois os mitigar: A introduzir entradas inesperadas nas operações de autenticação e autorização, o Fuzzing pode expor potenciais falhas na gestão de permissões.

b. Identifica e descreve brevemente (até 100 palavras cada) dois ataques de segurança que poderiam ser descobertos ao aplicar a metodologia de penetration testing. (Podes identificar a vulnerabilidade e o interface relacionado por onde o PenTester pode explorar a vulnerabilidade)

R: A ser aplicadas metodologias de Penetration testing (visão do atacante), podiam ser descobertos os seguintes ataques de segurança:

- CSRF (Cross-site request forgery): Pode ser feito enganando um utilizador legítimo para executar ações não desejadas. Isto poderia incluir a manipulação de configurações de Smart Meters, ou a realização de ações críticas sem a devida autorização.
- SQLi (SQL injection): Pode ser feito injetando comandos SQL maliciosos. Isto poderia comprometer a integridade dos dados, permitindo ao atacante acessar ou manipular informações sensíveis dos Smart Meters.

7. Apresenta dois exemplos de procedimentos que deveriam fazer parte de um manual de instalação ou de utilização do sistema (nota que pode haver vários tipos de utilizadores: administrador, utilizador x, utilizador y, apenas consulta, etc.) para garantir que o sistema é utilizado/operado de forma segura e robusta.

Nota: Procedimentos, regras, policies, restrições, etc. devem existir em todos os sistemas e podem inclusive estar especificados nos requisitos.

R: Os seguintes procedimentos deveriam fazer parte do manual de utilização do sistema:

- Reinicio de um serviço (p/ novo cliente ou correção de problemas): Este procedimento destina-se a utilizadores com permissões de administrador ou técnicos autorizados e visa garantir o reinício seguro de um serviço associado a um Smart Meter. É de notar que esta operação é irreversível, pois os mesmo dados são perdidos para sempre.
- Envio e troca de mensagem no portal: Este procedimento destina-se a utilizadores autorizados para garantir a comunicação eficaz através do portal SecureSmartMeter. Pode ser utilizado para enviar mensagens informativas, alertas ou para realizar trocas de informações relevantes. O envio de anexos é bastante limitado, podendo apenas enviar anexos até 5mb e num conjunto de formatos que se encontram conforme as políticas de segurança. Por motivos de segurança e confidencialidade, o email utilizado neste portal deve ser somente usado para efeitos, não podendo aceder a mais nenhum serviço externo com o mesmo.