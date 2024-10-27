# Prática 2 - Configuração de um servidor RADIUS

Nesta prática é configurado um servidor RADIUS para autenticação de utilizadores.

Na infraestrutura temos o nosso servidor RADIUS, que se encontra ligado a um *ethernet switch* que irá servir de autenticador, e o mesmo está ligado a um cliente que irá ser autenticado.

Primeiramente vamos instalar o *FreeRADIUS* no nosso servidor:
```bash
$ sudo apt-get install freeradius
```

Depois de instalado, vamos configurar o *FreeRADIUS* para que o mesmo possa ser utilizado para autenticação. 

Para isso, vamos editar o ficheiro `/etc/freeradius/3.0/clients.conf` e adicionar o seguinte conteúdo:
```conf
client 10.0.0.1 {
    secret = radiuskey
}
```
Isto irá definir um segredo partilhado entre o servidor RADIUS e o autenticador.

Depois disso vamos definir um utilizador no ficheiro `/etc/freeradius/3.0/users`:
```conf
"labredes" Cleartext-Password := "labcom"
```
Depois de configurado, vamos reiniciar o serviço.

Depois terá de ativar a funcionalidade do *RADIUS* autenticar pedidos. Para isso terá de editar o ficheiro `/etc/freeradius/3.0/radiusd.conf` e modificar a linha `auth` para:
```conf
auth = yes
```

Seguidamente vamos adicionar os endereços de IP no autenticador:
```cli
ESW1(config)# ip routing
ESW1(config)# int vlan 1
ESW1(config-if)# ip address 10.1.0.1 255.255.255.255
ESW1(config-if)# no shutdown
ESW1(config-if)# int fa 0/0
ESW1(config-if)# ip address 10.0.0.1 255.255.255.255
ESW1(config-if)# no shutdown
```

Seguidamente será configurar o autenticador. Isto será feito habilitando localmente o *802.1x* na porta ligada ao cliente e habilitar a autenticação RADIUS.
```cli
ESW1(config)# aaa new-model
ESW1(config)# aaa authentication dot1x default group radius
ESW1(config)# dot1x system-auth-control
ESW1(config)# radius-server host 10.0.0.100 auth-port 1812 key radiuskey
ESW1(config)# interface FastEthernet1/0
ESW1(config-if)# dot1x port-control auto
```

Depois irá adicinar as credenciais do utilizador `labredes/labcom` no cliente e o respetivo ip (10.1.0.100) e *gateway* (10.1.0.1).


E finalmente para ligar o servidor apenas terá de executar o seguinte comando:
```bash	
$ sudo systemctl start freeradius
```

# Prática 3 - Configuração de uma firewall (VyOS)

Neste guia é simulado o controlo de trafego entre uma rede interna, uma DMZ (rede de perímetro) e uma rede externa.

## Configuração PC1 - Rede interna

```console
ip 10.1.1.100/24 10.1.1.1
```

## Configuração PC2 - Rede Externa

```console
ip 200.1.1.100/24 200.1.1.1
```

## Configuração PC3 e PC4 - DMZ

Para o PC3:

```console
ip 192.1.1.40/24 192.1.1.1
```

Para o PC4:

```console
ip 192.1.1.140/24 192.1.1.1
```

## Configuração do VyOS

Para atribuir um endereço IP à interfaces ligadas às redes:

```console
# set interfaces ethernet eth0 address 200.1.1.1/24
# set interfaces ethernet eth1 address 192.1.1.1/24
# set interfaces ethernet eth2 address 10.1.1.1/24
# commit
# save
```

**Nota**: Na *firewall* o simbolo `$` no prompt indica que está a usar o **modo de utilizador**, enquanto que o simbolo `#` indica que está a usar o **modo de administrador**.

Para configurar o *NAT*:

```console
# set nat source rule 100 outbound-interface eth0
# set nat source rule 100 source address 10.1.1.0/24
# set nat source rule 100 translation address 192.1.0.1-192.1.0.10
# commit
# save
```

Este comando permite que o tráfego da rede interna seja traduzido para um endereço IP da DMZ.

Para testar, basca usar o comando `$ show nat source rules`.

*Network security zones* permitem definir uma rede ou um conjunto de redes que estão protegidas por uma *firewall*.

Aqui vamos definir quais são as zonas existentes e qual a sua interface correspondente:

```console
# set zone-policy zone INSIDE description "Inside (Internal Network)"
# set zone-policy zone INSIDE interface eth2
# set zone-policy zone DMZ description "DMZ (Server Farm)"
# set zone-policy zone DMZ interface eth1
# set zone-policy zone OUTSIDE description "Outside (Internet)"
# set zone-policy zone OUTSIDE interface eth0
# commit
# save
```

Para verificar as zonas criadas, basta usar o comando `$ show zone-policy`.

*Zone-Policies* permitem definir o que entra/sai entre as zonas.

Aqui vamos definir as regras de tráfego entre as zonas:

```console
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 description "Accept ICMP Echo Request"
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 action accept
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 protocol icmp
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 icmp type 8
# set firewall name TO-INSIDE rule 10 description "Accept Established-Related Connections"
# set firewall name TO-INSIDE rule 10 action accept
# set firewall name TO-INSIDE rule 10 state established enable
# set firewall name TO-INSIDE rule 10 state related enable
# set zone-policy zone INSIDE from OUTSIDE firewall name TO-INSIDE
# set zone-policy zone OUTSIDE from INSIDE firewall name FROM-INSIDE-TO-OUTSIDE
# commit
# save
```

Nós aqui podemos verificar que criamos uma regra com duas ações:

- Para sair: é permitido o tráfego ICMP;
- Para entrar: é permitido o tráfego que foi iniciado a partir do interior da rede.

Para verificar as regras criadas, basta usar o comando `$ show firewall`.

(POR ACABAR A PARTIR DA ALINEA 6)

Aqui vamos definir as regras que permitem os dispositivos da rede interna aceder aos servidores DMZ (ICMP):

```console
 # set firewall name FROM-INSIDE-TO-DMZ rule 10 description "Accept ICMP Echo Request"
 # set firewall name FROM-INSIDE-TO-DMZ rule 10 action accept
 # set firewall name FROM-INSIDE-TO-DMZ rule 10 protocol icmp
 # set firewall name FROM-INSIDE-TO-DMZ rule 10 icmp type 8
 # set firewall name FROM-INSIDE-TO-DMZ rule 10 destination address 192.1.1.0/24
 # set zone-policy zone INSIDE from DMZ firewall name TO-INSIDE
 # set zone-policy zone DMZ from INSIDE firewall name FROM-INSIDE-TO-DMZ
 # commit
# save
```

Ou seja, vamos conseguir pingar os servidores da DMZ a partir da rede interna, ao contrário apenas é enviado tráfego que foi iniciado a partir da rede interna.

Aqui vamos definir as regras que permitem os dispositivos da rede externa aceder aos servidores DMZ (ICMP):

```console
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 10 description "Accept ICMP Echo Request"
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 10 action accept
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 10 protocol icmp
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 10 icmp type 8
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 10 destination address 192.1.1.40
 # set firewall name FROM-DMZ-TO-OUTSIDE rule 10 description "Accept Established-Related Connections"
 # set firewall name FROM-DMZ-TO-OUTSIDE rule 10 action accept
 # set firewall name FROM-DMZ-TO-OUTSIDE rule 10 state established enable
 # set firewall name FROM-DMZ-TO-OUTSIDE rule 10 state related enable
 # set zone-policy zone OUTSIDE from DMZ firewall name FROM-DMZ-TO-OUTSIDE
 # set zone-policy zone DMZ from OUTSIDE firewall name FROM-OUTSIDE-TO-DMZ
 # commit
# save
```

Ou seja, vamos conseguir pingar o servidor `192.1.1.40` a partir da rede externa, ao contrário apenas é enviado tráfego que foi iniciado a partir da rede externa.

De seguida vamos definir também que os dispositivos da rede externa podem mandar pacotes UDP (apenas pela porta `8080`) para o servidor `192.1.1.140`

```console
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 12 description "Accept UDP-8080"
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 12 action accept
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 12 protocol udp
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 12 destination address 192.1.1.140
 # set firewall name FROM-OUTSIDE-TO-DMZ rule 12 destination port 8080
 # commit
# save
```

# Prática 4 - *High Availability* em *Firewalls*

Nesta prática é simulado o controlo de tráfego entre uma rede interna e uma rede externa, com duas *firewalls*.

Primeiro vamos carregar a configuração default do VyoS:

```bash
sudo cp /opt/vyatta/etc/config.boot.default /config/config.boot
reboot
```

Depois de dar os endereços IP às interfaces, vamos adicionar nos routers (interno e externo) as rotas para a rede um do outro.

Para o router interno, onde qualquer tráfego que não seja para a rede interna será redirecionado para a firewall FW2:

```cli
ip route 0.0.0.0 10.1.1.2
```

Para o router externo, onde qualquer tráfego que seja para a rede interna (endereço NAT), será redirecionado para a firewall FW1:

```cli
ip route 192.1.0.0 255.255.254.0 200.1.1.1
```

Depois de configurar os IP's nas firewall FW1 e FW2, vamos configurar o *NAT/PAT* na firewall FW1:

```cli
# set nat source rule 10 outbound-interface eth0
# set nat source rule 10 source address 10.0.0.0/8
# set nat source rule 10 translation address 192.1.0.1-192.1.0.10
```

Ou seja, qualquer tráfego que saia da rede interna, será traduzido para um endereço da rede 192.1.0.0.

Para configurar o *high-availability* nas firewalls, vamos configurar o *VRRP* (Virtual Router Redundancy Protocol) de modo a que as duas firewalls tenham o mesmo endereço IP virtual:

```cli
# set high-availability vrrp group FWCluster vrid 10
# set high-availability vrrp group FWCluster interface eth5
# set high-availability vrrp group FWCluster virtual-address 192.168.100.1/24
# set high-availability vrrp sync-group FWCluster member FWCluster
# set high-availability vrrp group FWCluster rfc3768-compatibility
```

De seguida vamos configurar o *conntack sync* para sincronizar as tabelas de estado entre as duas firewalls, para os protocolos `TCP`, `UDP`, e `ICMP`:

```cli
# set service conntrack-sync accept-protocol 'tcp,udp,icmp'
 # set service conntrack-sync failover-mechanism vrrp sync-group FWCluster
 # set service conntrack-sync interface eth5
 # set service conntrack-sync mcast-group 225.0.0.50 // multicast address
 # set service conntrack-sync disable-external-cache
```

De seguida resta apenas criar uma regra de *firewall* para permitir o tráfego entre a rede interna e a rede externa, apenas através do protocolo `UDP`:

```cli
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 action accept
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 description "Allow UDP traffic from inside to outside"
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 protocol udp
# set firewall name FROM-INSIDE-TO-OUTSIDE rule 10 destination port 5000-6000

# set firewall name FROM-OUSIDE-TO-INSIDE rule 10 action accept
# set firewall name FROM-OUSIDE-TO-INSIDE rule 10 description "Established-Related Connections"
# set firewall name FROM-OUSIDE-TO-INSIDE rule 10 state established enable
# set firewall name FROM-OUSIDE-TO-INSIDE rule 10 state related enable
```
