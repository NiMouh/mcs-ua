
> [!WARNING]
> As firewalls são as fronteiras das zonas! Se colocam firewalls, isso cria uma separação de zonas.
> Numa firewall só podem colocar regras entre zonas ligadas a essa firewall. Se tiverem várias zonas/FW ao longo do caminho tem de definir regras nelas todas (com as respetivas zonas).
> Tem de definir regras nos dois sentidas das Zonas!

1. No contexto de fases de um ataque a uma rede empresarial:

    a. Explique o impacto do fator humano nas diferentes fases de um possível ataque externo.

    b. Proponha soluções de segurança ao nível da rede passíveis de mitigar um ataque externo que use vetores de ataque focados em fatores humanos.

R:

a.

- Aquisição de conhecimento: informações obtidas seja através de má configuração da rede ou engenharia social tem um grande impacto no avanço do ataque.
- Infiltração: impacto maior, pois esta fase foi com base da informação anteriormente obtida. Isto pode ser conseguido através de métodos como phishing ou injeção de malware numa máquina na rede.
- Propagação: o fator humano pode ser um facilitador na propagação do ataque, pois através de ataques como phishing ou spoofing dentro da rede (e.g. fingir se passar o administrador da rede) pode contribuir para a propagação do ataque.
- Exfiltração: Dependendo do tipo de ataque, se o humano tiver acesso a informação sensível, pode ser um facilitador na exfiltração de dados.

b.

- Bloquear o acesso a DNSs ou endereços blacklisted, pois isto pode ser um indicativo de um ataque (e.g. C2 server).
- Uso de IDS (Intrusion Detection System) pois permite detetar atividades consideradas anormais feitas por um utilizador.
- Uso de IPS (Intrusion Prevention System) para bloquear atividades consideradas anormais.

2. No contexto de uma rede empresarial:

    a. Do lado da Internet, FW Stateless-Routers-LB-FW Statefull (ligação à DMZ)-Core. Depois FW statefull à entrada de cada DC. As zonas de rede existentes são DCB (Data-center B), DCC (Data-center C), DMZ, C-INTERNO (Cliente interno), C-EXTERNO (Cliente Externo).

    b.

i. Vários servidores Web HTTPS na DMZ com vários sites/dominios (porta 443) públicos que deverão estar disponíveis para o exterior
	
	Na(s) firewall(s) da DMZ, definir regras que inicialmente bloqueia todo o tráfego. Permitir o apenas o tráfego da zona C-EXTERNO para a DMZ sobre a porta 443 dos servidores Web HTTPS. Permitir o tráfego da zona DMZ para o C-EXTERNO que já tenha sido estabelecido (established connections).

ii. Dois servidores de email na DMZ (porta TCP 465 para clientes e servidores) públicos que deverão estar disponíveis para clientes externos e internos
	
	Na(s) firewall(s) da DMZ, definir regras que inicialmente bloqueia todo o tráfego. Permitir o tráfego da zona C-EXTERNO para DMZ sobre a porta 465 dos servidores de email. Permitir o tráfego da zona C-EXTERNO para a DMZ que já tenha sido estabelecido (established connections). Mesma coisa para o tráfego da zona C-INTERNO para a DMZ.

iii. Um servidor Web HTTPS com intranet da empresa (porta 443) no Datacenter B que deverá estar disponível apenas para os terminais internos das VLAN 5 e 6
	
	Na(s) firewall(s) do Datacenter B, definir regras que inicialmente bloqueia todo o tráfego. Permitir o tráfego da zona C-INTERNO, que tenham a gama de IP's das VLANs 5 e 6, para a DMZ sobre a porta 443 do servidor Web HTTPS

iv. 3 servidores de backup de dados (TCP 5001 a 5002) no Datacenter C que apenas deverão estar disponíveis pelos servidores Web HTTPS e por um servidor pré-definido externos para sincronização/replicação de dados.
	
	Na(s) firewall(s) do Datacenter C, definir regras que inicialmente bloqueia todo o tráfego. Permitir o tráfego da zona DMZ para o DCC sobre as portas 5001 e 5002 dos servidores de backup de dados para os servidores Web HTTPS. Permitir o tráfego da zona C-EXTERNO para o DCC sobre as portas 5001 e 5002 dos servidores de backup de dados para o servidor pré-definido externo. Permitir o tráfego da zona DCC para a DMZ e C-EXTERNO que já tenha sido estabelecido (established connections).

3. Proponha uma solução de comunicação e encaminhamento IPv4 ao nível da rede, e respetivas alterações nas regras das firewalls, que garanta que o tráfego TCP para os servidores de backup no datacenter C (via WAN) seja encaminhado de forma que garanta confidencialidade.

    R: Para garantir a confidencialidade entre os servidores de backup na DCC e os respetivos recetores, vai ser implementado um tunel IPsec Site-to-Site com politicas de encaminhamento (PBR) para garantir que o tráfego entre os servidores de backup e os recetores seja encriptado.

    Para isso será necessário definir as seguintes regras na firewall do Datacenter C
       - Para o estabelecimento na comunicação, permitir o IKE (UDP 500) entre as zonas DCC (apenas para os servidores de backup) e C-EXTERNO/DMZ (para os recetores)
       - Para o tráfego de dados em si, permitir o tráfego ESP (IP protocol 50) entre as zonas DCC (apenas para os servidores de backup) e C-EXTERNO/DMZ (para os recetores)
       - Adicionalmente, permitir o tráfego UDP 4500 para o NAT-T (Network Address Translation Traversal) para permitir a comunicação entre os servidores de backup e os recetores que estejam atrás de um NAT.

4. Proponha um sistema SIEM, incluindo o processo de colega de dados e a definição de regras de alerta, capaz de alertar para:

    a. Tentativas de acesso a objetos não autorizados nos servidores HTTPS.

    b. Clientes externos a participar num ataque DDoS. Indique pelo menos 3 regras.

    c. Possível atividade botnet.

    d. Possível exfiltração encobertas (stealth) de dados terminais internos utilizando serviços externos legitimos e autorizados.

    R:

    a. SIEM: Rsyslog
        - Processo de coleção de dados: Rsyslog vai recolher os logs da(s) firewall(s) da DMZ referentes ao tráfego direcionado aos servidores HTTPS.
        - Definição de regras de alerta: Emitir alerta sempre que um IP tenta aceder a um objeto não autorizado nos servidores HTTPS (e.g. /etc/passwd)

    b. SIEM: Rsyslog
        - Processo de coleção de dados: Rsyslog vai recolher os logs da(s) firewall(s) na extremidade da rede interna.
        - Definição de regras de alerta:
          - Emitir um alerta sempre que um IP externo tenta aceder a um serviço interno (e.g. SSH) e envia um número anormal de pacotes.
          - Emitir um alerta sempre que seja detetado picos de conexões SYN sem completar a sessão TCP (SYN flood).
          - Emitir um alerta sempre que seja detetado um alto volume de pedidos HTTPS do mesmo IP ou gama de IPs num curto período.

    c. SIEM: Rsyslog
        - Processo de coleção de dados: Rsyslog vai recolher os logs da(s) firewall(s) que delimitam zonas internas.
        - Definição de regras de alerta: Emitir um alerta sempre que um terminal interno tenta criar comunicações com um outro terminal interno sem qualquer tipo de precedente.

    d. SIEM: Rsyslog
        - Processo de coleção de dados: Rsyslog vai recolher os logs da(s) firewall(s) na extremidade da rede interna.
        - Definição de regras de alerta: Emitir um alerta sempre que um terminal interno tenta aceder a um serviço externo autorizado e legítimo (e.g. Dropbox) e envia uma quantidade anormal de dados.
