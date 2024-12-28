
## Frequências do Ano 21/22

![[TPR_ExameRecurso_28Fevereiro2022.pdf]]

#### Respostas

1.

	a. (ACESSO INDEVIDO) Para a aquisição, obter os logs dos servidores de autenticação (AD, RADIUS, LDAP) de modo a permitir monitorizar as tentativas de acesso, autenticações bem sucedidas e mal sucedidas bem como o seu horário e centrar os logs usando um SIEM (e.g. Wazuh ou UTMStack) permitindo correlacionar esta informação e definir metricas para detetar atividade anómala. Para o tratamento, implementar regras de correlação para identificar tentativas de acesso vindas de localizações diferentes das habituais, múltiplas tentativas de autenticação incorretas num curto espaço de tempo e possivelmente em diferentes localizações (brute-force), tentativas de acesso com a mesma palavra-passe em diferentes serviços (password-spraying), e tentativas de autenticação fora do horário laboral.
	
	b. (C2 ATTACK) Para a aquisição, obter os logs dos terminais e serviços da rede da empresa (Syslog, Sysmon) de modo a permitir monitorizar atividades como criação de processos, eventos de rede e manipulação de ficheiros, algo frequente em botnets, e centrar os logs usando um SIEM (e.g. Wazuh ou UTMStack), detetando padrões que seriam invisíveis caso fossem analisados isoladamente. Para o tratamento, implementar regras de correlação para identificar conexões curtas em intervalos regulares entre os dispositivos e serviços da mesma rede, identificar uso isolado de portas num dado serviço com destino na mesma rede com o uso de protocolos como DNS, HTTP ou HTTPS para mascarar comunicações, comparar o rácio do tráfego interno com outras linhas temporais definindo um *threshold* daquilo que seria o normal com base no comportamento típico de cada dispositivo.

	 
	c. (EXFILTRATION) Para a aquisição, obter os logs dos terminais e serviços que foram anteriormente alertados como possivelmente comprometidos (Syslog, Sysmon) e centrar os logs usando um SIEM (e.g. Wazuh ou UTMStack). Para o tratamento, implementar regras de correlação para identificar acessos externos, seja um endereço apenas ou uma gama de endereços associados a um serviço, em comum entre essas máquinas, identificar o periodo temporal onde cada uma comunicou com estes serviços externos de modo a saber quais máquinas acederam a essas máquinas externas em alturas diferentes, identificar periodicidade com que os terminais comunicam com as máquinas externas.

1. O Ataque DDoS provoca uma disrupção no serviço e durante um ataque o foco será a identificação de clientes lícitos e ilícitos de modo que o serviço continue disponível para os demais. 

![[TPR_Exame_14Fevereiro2022.pdf]]

1.

	a. (C2 ATTACK e CRIPTO-MINING) Para a aquisição de dados de modo a identificar as máquinas comprometidas, obter os fluxos feitos por os servidores da rede (e.g. Netflow) para a rede interna, de modo a conseguir caracterizar o tipo e quantidade de tráfego feito entre eles. Além disso, obter logs que forneçam informação do desempenho da máquina (SNMP), de modo a conseguir detetar a existência de aumentos súbitos no consumo de energia ou desempenho.

	b. Para as métricas, obter o número de pacotes downloads e uploads dos fluxos, bem como o número de bytes de download e upload dos fluxos e duração dos fluxos. Para as *features* numa janela de observação, obter o número de fluxos, a média e desvio padrão do número de bytes (*download* e *upload*), a média e desvio padrão do número de pacotes (*download* e *upload*) e a média e desvio padrão da duração dos fluxos.

	c. Para o tratamento, centrar os logs dos dispositivos (e.g. Syslog) usando um SIEM (e.g. Wazuh ou UTMStack),  depois implementar regras de correlação, no caso da deteção de C2, para  obter comunicações de curta duração (maioritariamente downloads) para máquinas externas com uma periodicidade de 10 segundos. No caso da deteção do software de mineração, filtrar para uma periodicidade de 2 minutos (downloads e uploads), correlacionando estes periodos com o uso de recursos da máquina interna. Para a análise de dados, usar escalogramas para obter a periodicidade.

2. Num ataque de exfiltração, o foco é a exportação intencional e não autorizada de dados de um dispositivo para um destino externo (afeta a confidencialidade), enquanto no caso dos ataques de disrupção é tornar o serviço/servidor inutilizável (afeta a disponibilidade). Para detetar exfiltração, é necessária uma monitorização continua do tráfego da rede para identificar padrões de comunicação anómalos, como destinos desconhecidos, mudanças na variação do volume de tráfego enviado para endereços externos e envios para destinos externos com uma certa periodicidade. Para detetar ataques de disrupção, o foco é a monitorização de picos de tráfego externo, múltiplos pedidos simultâneos do mesmo serviço de várias origens e aumento exponencial de sessões de curta duração.