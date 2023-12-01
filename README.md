# Projeto de Redes Convergentes

-   Alunos:
    -   Gabriel Fonseca Feitosa - 2111066
    -   Pedro Lucas Ribeiro - 2111131

## Introdução

![Screenshot da rede no Cisco Package Tracer](rede.png)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Projeto de rede feito no Cisco Package Tracer, para a disciplina Projeto de Redes Convergentes do 6º semestre do curso de Ciência da Computação da UNIFOR.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;O projeto de rede utiliza-se de um amalgamo de teorias que foram aprendidas no decorrer da disciplina, para atingir o objetivo de configurar uma rede que satisfaça as especificações realizadas pelo professor, com fins de avaliação e aprendizado.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dentre as tecnologias utilizadas, temos os principais protocolos de troca de dados em rede, como UDP, HTTP e o pai de todos os supracitados, o TCP/IP. Utilizaremos também conceitos de endereçamento como os IPs definidos estaticamente e dinamicamente através do DHCP, servidores DNS internos e externos às redes para resolução de nomes de domínio, LANs virtuais para isolamento e segmentação das redes em seus próprios ambientes e, finalmente, o protocolo RIP para roteamento das requisições.

## Dados de configuração das redes

### Tabela VLAN de DADOS

| Rede | Interface VLAN |     Host     |     Mask      |   Gateway    |   Broadcast    |      Servidor DHCP      | DHCP Interno |          Range DHCP           |      Servidor DNS       |      Servidor HTTP      |
| :--: | :------------: | :----------: | :-----------: | :----------: | :------------: | :---------------------: | :----------: | :---------------------------: | :---------------------: | :---------------------: |
|  1   |       11       | 192.168.11.0 | 255.255.255.0 | 192.168.11.1 | 192.168.11.255 | 192.168.11.2 (Estático) |      -       | 192.168.11.5 - 192.168.11.254 | 192.168.11.3 (Estático) | 192.168.11.4 (Estático) |
|  2   |       21       | 192.168.21.0 | 255.255.255.0 | 192.168.21.1 | 192.168.21.255 | 192.168.11.2 (Rede 01)  |      -       | 192.168.21.5 - 192.168.21.254 |            -            |            -            |
|  3   |       31       | 192.168.31.0 | 255.255.255.0 | 192.168.31.1 | 192.168.31.255 |            -            | 192.168.31.1 |               -               |            -            |            -            |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Com fins de organização e facilidade de leitura e interpretação, escolhemos as interfaces 11, 21 e 31 para as redes 01, 02 e 03 respectivamente, que é refletido em seus valores de host, que por consequência também reflete em todos os endereços restantes, como o gateway, broadcast, servidor de DHCP para o caso da rede 03 que é interno, e os servidores DNS e HTTP aonde se aplica (Apenas a rede 01 possui ditos servidores.).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A tabela acima refere-se aos valores e configuração do serviço de transmissão de dados especificamente, utilizando a interface do tipo FastEthernet. Pode-se notar que na rede 01 há 3 endereços IP estáticos, que são referentes ao servidor DHCP, DNS e HTTP. O servidor DHCP tem a necessidade de ser estático por ser utilizado como servidor DHCP também na rede 02, como nas especificações da rede descritas pelo professor. Os servidores DNS e HTTP necessitam de ser estáticos pois também foi especificado que todos os hosts devem ser capazes de acessar o site, que reside no servidor HTTP e terá seu endereço cadastrado no DNS com o nome `server02`. Os IPs estáticos dos servidores HTTP e DNS tornam o site acessível, através do nome, para todos os hosts da rede completa, inclusive os dispositivos fora da rede 01, onde o servidor HTTP reside.

### Tabela VLAN de VOIP

| Rede | Interface VLAN |     Host     |     Mask      |   Gateway    |          DHCP          | Broadcast Voz  |        Range DHCP Voz         |
| :--: | :------------: | :----------: | :-----------: | :----------: | :--------------------: | :------------: | :---------------------------: |
|  1   |       12       | 192.168.12.0 | 255.255.255.0 | 192.168.12.1 |      192.168.11.2      | 192.168.12.255 | 192.168.12.5 - 192.168.12.254 |
|  2   |       22       | 192.168.22.0 | 255.255.255.0 | 192.168.22.1 | 192.168.11.2 (Rede 01) | 192.168.22.255 | 192.168.22.5 - 192.168.22.254 |
|  3   |       32       | 192.168.32.0 | 255.255.255.0 | 192.168.32.1 | 192.168.31.1 (Interno) | 192.168.32.255 |               -               |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A tabela acima estabelece os dados da configuração da VLAN de voz das 3 redes que foram especificadas. Continuando com o padrão estabelecido nas VLANs de dados, pode-se notar que as interfaces configuradas para as VLANs de voz são 12, 22 e 32 para as redes 01, 02 e 03 respectivamente, onde apenas a coluna de DHCP mostra um comportamento diferente, onde a rede 02, como dito previamente, utiliza o servidor DHCP da rede 01, e a rede 03 possui um servidor de DHCP que é o próprio roteador. Os dispositivos de voz irão se comunicar através do protocolo SIP.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;As duas VLANs (dados e voz) de cada rede, necessita de que a porta 1 do switch da sua rede esteja configurada no modo `TRUNK`, para que seja permitido a passagem de vários tipos de dados e comunicação entre as VLANs das redes vizinhas.

## Equipamentos utilizados

-   Rede 01:
    -   1 x Roteador 2811 + Módulo FastEthernet NM-1FE-TX
    -   1 x Switch 2950-24
    -   3 x Servidores
    -   2 x PCs
    -   2 x IP Phones 7960
    -   1 x AccessPoint-PT
    -   1 x SmartPhone-PT
    -   1 x TabletPC-PT

---

-   Rede 02
    -   1 x Roteador 2811 + Módulo FastEthernet NM-1FE-TX
    -   1 x Switch 2950-24
    -   2 x PCs
    -   2 x IP Phones 7960
    -   1 x AccessPoint-PT
    -   1 x SmartPhone-PT
    -   1 x TabletPC-PT

---

-   Rede 03
    -   1 x Roteador 2811 + Módulo FastEthernet NM-1FE-TX
    -   1 x Switch 2950-24
    -   2 x PCs
    -   2 x IP Phones 7960
    -   1 x AccessPoint-PT
    -   1 x SmartPhone-PT
    -   1 x TabletPC-PT

---

-   Total:

    -   3 x Roteadores 2811 + Módulo FastEthernet NM-1FE-TX
    -   3 x Switch's 2950-24
    -   3 x Servidores
    -   6 x PCs
    -   6 x IP Phone 7960
    -   3 x AccessPoint-PT
    -   3 x SmartPhone-PT
    -   3 x TabletPC-PT

---

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;O Roteador 2811 foi escolhido pois é o único que tem suporte a telefonia dos modelos disponíveis no Cisco Package Tracer. O módulo extra NM-1FE-TX foi necessário pois o modelo de roteador 2811 só possui duas entradas ethernet por padrão, e uma extra foi adicionada para que ele pudesse se comunicar internamente e com as outras duas redes. O switch escolhido (2950-14) foi escolhido puramente por razões de consistência com as atividades do professor, pois foi o mesmo modelo que ele utilizou, mas acreditamos que qualquer switch seria cabível, pois todos são switchs "inteligentes", capazes de gerenciar VLANs. Os 3 servidores foram os de DHCP, HTTP e DNS. Foram feitos separadamente para um melhor entendimento do trabalho, porém, seria possível prestar todos os 3 serviços em apenas um servidor. Um total de 18 dispositivos endpoint para testes das rotas e serviços configurados. 3 AccessPoints foram utilizados para configurar o wi-fi para dispositivos wireless.

## Comandos para configuração das redes

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A seguir serão apresentados os comandos necessários para configurar o hardware utilizado em cada uma das três redes.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A montagem da rede como um todo envolve muita repetição de comandos e configurações iguais que apenas mudam os valores utilizados. Por essa razão, será explicado e desenvolvido apenas os comandos para os equipamentos Switch, Router (Interfaces), Router (Telefonia), Router (Rotas), Router (Rotas VOIP) e o Router (Rotas) da rede 3.

### Rede 1

-   Equipamento: Switch

```sh
Switch> en
Switch# conf t
    > Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)# vlan 11
Switch(config-vlan)# name dados
Switch(config-vlan)# exit
Switch(config)# vlan 12
Switch(config-vlan)# name voice
Switch(config-vlan)# exit
Switch(config)# int fa 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch(config)# int range fa 0/2-24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 11
Switch(config-if-range)# exit
Switch(config)# int range fa 0/23-24
Switch(config-if-range)# switchport voice vlan 12
Switch(config-if-range)# exit
Switch(config)# exit
```

Os valores 11 e 12 escolhidos para a VLAN são iguais as interfaces nos valores de host apresentados inicialmente neste documento, apenas para facilidade de leitura e compreensão.

O comando `en` de enable trata-se do comando de enable, para entrar no root do roteador. `conf t` ou `configure terminal` para entrar no modo de configuração do switch ou roteador. O comando `vlan xx` serve para criar uma VLAN e entrar na configuração da mesma, onde `xx` é qualquer número, de 1 a 4096, que servirá de interface para a VLAN. O comando `name xxxx` serve apenas para nomear a VLAN, onde `xxxx` é o nome a ser dado para a VLAN. O comando `int fa x/x` ou `interface fastEthernet x/x` serve para acessar uma porta específica do switch, podendo-se também utilizar com um `range` (intervalo) de portas, para aplicar a mesma configuração à várias portas simultaneamente, como é feito no comando logo abaixo. O comando `switchport mode` serve para alterar o tipo de porta podendo ser os modos `TRUNK` ou `ACCESS`, sendo o `TRUNK` a porta que vai se comunicar com o roteador, pois ela necessita passar todas as VLANs. O `ACCESS` então seria acesso aos endpoints e VoIPs. Os comandos `switchport access vlan xx` e `switchport voice vlan xx` servem para atribuir os modos das VLANs criadas anteriormente, utilizando seu número como identificador. Pode-se notar que no colocamos a VLAN de voz apenas nas portas 23 e 24 do switch, pois serão utilizadas pelos telefones IPs.

-   Equipamento: Router (Interfaces)

```sh
Router> en
Router# conf t
    > Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# int fa 0/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
Router(config-if)# exit
Router(config)# int fa 0/1
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
Router(config-if)# ip address 10.0.0.1 255.0.0.0
Router(config-if)# exit
Router(config)# int fa 1/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet1/0, changed state to up
Router(config-if)# ip address 11.0.0.1 255.0.0.0
Router(config-if)# exit
Router(config)# int fastEthernet 0/0.11
    > %LINK-5-CHANGED: Interface FastEthernet0/0.11, changed state to up
Router(config-subif)# ip add
Router(config-subif)# encapsulation dot1Q 11
Router(config-subif)# ip address 192.168.11.1 255.255.255.0
Router(config-subif)# exit
Router(config)# int fastEthernet 0/0.12
    > %LINK-5-CHANGED: Interface FastEthernet0/0.12, changed state to up
Router(config-subif)# encapsulation dot1Q 12
Router(config-subif)# ip address 192.168.12.1 255.255.255.0
Router(config-subif)# exit
Router(config)# end
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

Como há alguns comandos repetidos, tal como o de configuração da interface de FastEthernet (`int fa x/x`), iremos pular estes comandos para fins de clareza.

O comando `no shutdown`, serve para que a porta seja habilitada no roteador, para que ela seja utilizável para comunicação, pois caso contrário ela não ficaria no estado "UP". O comando `ip address XXX.XXX.XXX.XXX XXX.XXX.XXX.XXX` serve para "settar" o IP juntamente com a máscara. O comando `int fastEthernet x/x.yy` serve para criar a sub-interface onde `yy` é o valor identificador da sub-interface, que usaremos para configurar as VLANs. O comando `encapsulation dot1Q yy` serve para atribuir a VLAN à sub-interface `yy`.

-   Equipamento: Router (Telefonia)

```sh
Router# conf t
    > Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# int fastEthernet 0/0.12
Router(config-subif)# ip helper-address 192.168.11.2
Router(config-subif)# exit
Router(config)# telephony-service
Router(config-telephony)# max-dn 10
Router(config-telephony)# max-ephones 10
Router(config-telephony)# ip source-address 192.168.12.1 port 2000
Router(config-telephony)# auto assign 1 to 10
Router(config-telephony)# exit
Router(config)# ephone-dn 1
Router(config-ephone-dn)# %LINK-3-UPDOWN: Interface ephone_dsp DN 1.1, changed state to up
Router(config-ephone-dn)# number 100
Router(config-ephone-dn)# exit
Router(config)# ephone-dn 2
Router(config-ephone-dn)# %LINK-3-UPDOWN: Interface ephone_dsp DN 2.1, changed state to up
Router(config-ephone-dn)# number 101
    > %IPPHONE-6-REGISTER: ephone-1 IP:192.168.12.6 Socket:2 DeviceType:Phone has registered.
    > %IPPHONE-6-REGISTER: ephone-2 IP:192.168.12.8 Socket:2 DeviceType:Phone has registered.
Router(config-ephone-dn)# exit
Router(config)# end
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

Como o DHCP dessa rede é externo ao roteador, devemos configurar onde os telefones irão solicitar os IPs, com o comando `ip helper-address XXX.XXX.XXX.XXX` na sub-interface referente a rede de voz. Usamos o comando `telephony-service` para entrar na configuração da parte de telefonia do roteador. O comando `max-dn XX` indica um número de linhas `XX` que irão existir nesse roteador. O comando `max-ephones XX` indica o número máximo `XX` de telefones físicos presentes na rede. O comando `auto assign XX to YY` significa que ele irá atribuir automaticamente as linhas `XX` à `YY` conforme os telefones vão se registrando na rede. O comando `ip source-address XXX.XXX.XXX.XXX port YYYY` indica de onde o telefone IP irá fazer o download de sua configuração, normalmente sendo o próprio roteador onde o serviço de telefonia está sendo configurado. O comando `ephone-dn X` indica que estou entrando na linha `X` e atribuindo um número a ela com o comando `number Y`. Repete-se para os telefones restantes.

-   Equipamento: Router (Rotas)

```sh
Router> en
Router# config t
    > Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# router rip
Router(config-router)# network 192.168.11.0
Router(config-router)# network 192.168.12.0
Router(config-router)# network 10.0.0.0
Router(config-router)# network 11.0.0.0
Router(config-router)# end
Router#
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

O comando `router rip` serve para entrarmos na configuração de rotas utilizando o protocolo RIP, podendo alternar entre os diferentes protocolos, como BGP ou OSPF. Como estamos utilizando o protocolo RIP, precisamos apenas dizer quais redes estão presentes nele com o comando `network XXX.XXX.XXX.XXX`. Nota-se que as redes `192.168.11.0` e `192.168.12.0` são da rede LAN, e as redes `10.0.0.0` e `11.0.0.0` são para comunicação com as redes externas.

-   Equipamento: Router (Rotas VOIP)

```sh
Router# config t
    > Enter configuration commands, one per line. End with CNTL/Z.
Router(config)# dial-peer voice 1 voip
Router(config-dial-peer)# destination-pattern 300
Router(config-dial-peer)# session target ipv4:11.0.0.2
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 2 voip
Router(config-dial-peer)# destination-pattern 301
Router(config-dial-peer)# session target ipv4:11.0.0.2
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 3 voip
Router(config-dial-peer)# destination-pattern 200
Router(config-dial-peer)# session target ipv4:10.0.0.2
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 4 voip
Router(config-dial-peer)# destination-pattern 201
Router(config-dial-peer)# session target ipv4:10.0.0.2
Router(config-dial-peer)# exit
Router(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

O comando `dial-peer voice X voip` configura um "dial peer" para lidar com, usando o número `X` como identificador. Esse "dial peer" determina como o roteador encaminha as chamadas com base em critérios específicos, como o destino da chamada. O `dial-peer` necessita de configurações/parâmetros extras para o seu funcionamento, onde um desses parâmetros é o `destination-pattern X` que define o padrão de discagem para o ramal com o `destination-pattern` que se encaixe no valor "curinga" `X` informado, podendo ser um valor mais específico, ou generalizado, dependendo do seu tamanho. O próximo parâmetro é o `session target`, que define para qual endereço ele deve enviar esta chamada, podendo ser um telefone, ou um IPv4 referente ao endereço do roteador da rede, que foi nosso caso, onde o endereço `11.0.0.2` trata-se do roteador da rede 03, e o `10.0.0.2` é da rede 02. Repete-se o processo para os roteadores restantes, mudando o `destination-pattern` e o `session target`.

### Rede 2

-   Equipamento: Switch

```sh
Switch> en
Switch# conf t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)# vlan 21
Switch(config-vlan)# name dados
Switch(config-vlan)# exit
Switch(config)# vlan 22
Switch(config-vlan)# name voice
Switch(config-vlan)# exit
Switch(config)# int fa 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch(config)# int range fa 0/2-24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 21
Switch(config-if-range)# exit
Switch(config)# int range fa 0/23-24
Switch(config-if-range)# switchport voice vlan 22
Switch(config-if-range)# exit
Switch(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Interfaces)

```sh
Router> en
Router# conf t
    Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# int fa 0/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
Router(config-if)# exit
Router(config)# int fa 0/1
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
Router(config-if)# ip address 10.0.0.2 255.0.0.0
Router(config-if)# exit
Router(config)# int fa 1/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet1/0, changed state to up
Router(config-if)# ip address 12.0.0.1 255.0.0.0
Router(config-if)# exit
Router(config)# int fastEthernet 0/0.21
    > %LINK-5-CHANGED: Interface FastEthernet0/0.21, changed state to up
Router(config-subif)# ip add
Router(config-subif)# encapsulation dot1Q 21
Router(config-subif)# ip address 192.168.21.1 255.255.255.0
Router(config-subif)# ip helper-address 192.168.11.2
Router(config-subif)# exit
Router(config)# int fastEthernet 0/0.22
    > %LINK-5-CHANGED: Interface FastEthernet0/0.22, changed state to up
Router(config-subif)# encapsulation dot1Q 22
Router(config-subif)# ip address 192.168.22.1 255.255.255.0
Router(config-subif)# ip helper-address 192.168.11.2
Router(config-subif)# exit
Router(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Telefonia)

```sh
Router> en
Router# conf t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# telephony-service
Router(config-telephony)# max-dn 10
Router(config-telephony)# max-ephones 10
Router(config-telephony)# ip source-address 192.168.22.1 port 2000
Router(config-telephony)# auto assign 1 to 10
Router(config-telephony)# exit
Router(config)# ephone-dn 1
Router(config-ephone-dn)# %LINK-3-UPDOWN: Interface ephone_dsp DN 1.1, changed state to up
Router(config-ephone-dn)# number 200
Router(config-ephone-dn)# exit
Router(config)# ephone-dn 2
Router(config-ephone-dn)# %LINK-3-UPDOWN: Interface ephone_dsp DN 2.1, changed state to up
Router(config-ephone-dn)# number 201
    > %IPPHONE-6-REGISTER: ephone-1 IP:192.168.22.6 Socket:2 DeviceType:Phone has registered.
    > %IPPHONE-6-REGISTER: ephone-2 IP:192.168.22.8 Socket:2 DeviceType:Phone has registered.
Router(config-ephone-dn)# exit
Router(config)# end
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Rotas)

```sh
Router> en
Router# config t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# router rip
Router(config-router)# network 192.168.21.0
Router(config-router)# network 192.168.22.0
Router(config-router)# network 10.0.0.0
Router(config-router)# network 12.0.0.0
Router(config-router)# end
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Rotas VOIP)

```sh
Router# config t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# dial-peer voice 1 voip
Router(config-dial-peer)# destination-pattern 300
Router(config-dial-peer)# session target ipv4:12.0.0.2
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 2 voip
Router(config-dial-peer)# destination-pattern 301
Router(config-dial-peer)# session target ipv4:12.0.0.2
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 3 voip
Router(config-dial-peer)# destination-pattern 100
Router(config-dial-peer)# session target ipv4:10.0.0.1
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 4 voip
Router(config-dial-peer)# destination-pattern 101
Router(config-dial-peer)# session target ipv4:10.0.0.1
Router(config-dial-peer)# exit
Router(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

### Rede 3

-   Equipamento: Switch

```sh
Switch> en
Switch# conf t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)# vlan 32
Switch(config-vlan)# name voice
Switch(config-vlan)# exit
Switch(config)# vlan 31
Switch(config-vlan)# name dados
Switch(config-vlan)# exit
Switch(config)# int fa 0/1
Switch(config-if)# switchport mode trunk
Switch(config-if-range)# exit
Switch(config)# int range fa 0/2-24
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 31
Switch(config-if-range)# exit
Switch(config)# int range fa 0/23-24
Switch(config-if-range)# switchport voice vlan 32
Switch(config-if-range)# exit
Switch(config)# end
Switch#
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Interfaces)

```sh
Router> en
Router# conf t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# int fa 0/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up
Router(config-if)# exit
Router(config)# int fa 0/1
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
Router(config-if)# ip address 11.0.0.2 255.0.0.0
Router(config-if)# exit
Router(config)# int fa 1/0
Router(config-if)# no shutdown
    > %LINK-5-CHANGED: Interface FastEthernet1/0, changed state to up
Router(config-if)# ip address 12.0.0.2 255.0.0.0
Router(config-if)# exit
Router(config)# int fastEthernet 0/0.31
    > %LINK-5-CHANGED: Interface FastEthernet0/0.31, changed state to up
Router(config-subif)# ip add
Router(config-subif)# encapsulation dot1Q 31
Router(config-subif)# ip address 192.168.31.1 255.255.255.0
Router(config-subif)# exit
Router(config)# int fastEthernet 0/0.12
    > %LINK-5-CHANGED: Interface FastEthernet0/0.32, changed state to up
Router(config-subif)# encapsulation dot1Q 32
Router(config-subif)# ip address 192.168.32.1 255.255.255.0
Router(config-subif)# exit
```

-   Equipamento: Router (Telefonia)

```sh
Router(config)# telephony-service
Router(config-telephony)# max-dn 10
Router(config-telephony)# max-ephones 10
Router(config-telephony)# ip source-address 192.168.32.1 port 2000
Router(config-telephony)# auto assign 1 to 10
Router(config-telephony)# exit
Router(config)# ephone-dn 1
    > %LINK-3-UPDOWN: Interface ephone_dsp DN 1.1, changed state to up
Router(config-ephone-dn)# number 300
Router(config-ephone-dn)# exit
Router(config)# ephone-dn 2
    > %LINK-3-UPDOWN: Interface ephone_dsp DN 2.1, changed state to up
Router(config-ephone-dn)# number 301
Router(config-ephone-dn)# exit
Router(config)# exit
```

-   Equipamento: Router (DHCP)

```sh
Router(config)# ip dhcp pool dados
Router(dhcp-config)# network 192.168.31.0 255.255.255.0
Router(dhcp-config)# dns-server 192.168.11.3
Router(dhcp-config)# default-router 192.168.31.1
Router(dhcp-config)# exit
Router(config)# ip dhcp pool voice
Router(dhcp-config)# network 192.168.32.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.32.1
Router(dhcp-config)# option 150 ip 192.168.32.1
Router(dhcp-config)# exit
Router(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

Com o comando `ip dhcp pool dados` estamos criando um `pool` de DHCP com o nome `dados`, onde informamos a rede a qual ele pertence com o comando `network 192.168.31.0 255.255.255.0`, a informação do servidor DNS com o comando `dns-server 192.168.11.3`, e a rota padrão, que trata-se da rota do próprio roteador com o comando `default-router 192.168.31.1`. O comando `default-router` também é conhecido como `gateway` da rede em outros roteadores. Os comandos então repetem-se para a VLAN de voz, acrescentando apenas o `option 150 ip 192.168.32.1` sendo a configuração utilizada apenas por telefones IP, sendo um servidor TFTP, onde os dispositivos fazem download de suas respectivas configurações.

-   Equipamento: Router (Rotas)

```sh
Router> en
Router# config t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# router rip
Router(config-router)# network 192.168.31.0
Router(config-router)# network 192.168.32.0
Router(config-router)# network 11.0.0.0
Router(config-router)# network 12.0.0.0
Router(config-router)# end
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```

-   Equipamento: Router (Rotas VOIP)

```sh
Router# config t
    > Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)# dial-peer voice 1 voip
Router(config-dial-peer)# destination-pattern 100
Router(config-dial-peer)# session target ipv4:11.0.0.1
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 2 voip
Router(config-dial-peer)# destination-pattern 101
Router(config-dial-peer)# session target ipv4:11.0.0.1
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 3 voip
Router(config-dial-peer)# destination-pattern 200
Router(config-dial-peer)# session target ipv4:12.0.0.1
Router(config-dial-peer)# exit
Router(config)# dial-peer voice 4 voip
Router(config-dial-peer)# destination-pattern 201
Router(config-dial-peer)# session target ipv4:12.0.0.1
Router(config-dial-peer)# exit
Router(config)# exit
    > %SYS-5-CONFIG_I: Configured from console by console
    > Building configuration...
    > [OK]
```
