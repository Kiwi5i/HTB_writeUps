# Cap

A principio, me era disponibilizado apenas um IP (10.129.39.137)
Fazendo um nmap, percebemos que existem 3 portas abertas, 21 para ftp, 22 para ssh e 80 para http. Isso será importante mais tarde.

![nmap](IMG1.png)

Tentando acessar esse IP pelo navegador (server http), somos direcionados para um site que contem um dashboard.
Clicando na aba de "security snapshot", aparece a segunte página com um botão de download:

![dashboard](IMG2.png)

Ao clicar no botão de download, é fornecido um arquivo pcap, que pode ser analisado pelo wireshark, mas ele não contem nenhuma informação interessante, apenas tráfego de mim mesmo.

Esse site, porém, possui uma janela para IDOR, visto que o endpoint que fornece a snapshot de segurança contem um numero facilmente alterável. Por exemplo, o meu pacote está no endpoint /data/1. 
Tentando alterar para /data/0, eu consigo ver uma snapshot de segurança passada, pertencente ao user Nathan.

Abrindo ela no wireshark, agora existem muito mais informações interessantes, e ao seguir o stream ftp, informações de login e senha do Nathan são mostradas.

![ftp-stream](IMG3.png)

Percebemos que ele utiliza o login "nathan" e a senha "Buck3tH4TF0RM3!". E essas credenciais funcionam tambem no ssh.

$ ssh nathan@10.129.39.137
$ Buck3tH4TF0RM

Com isso conseguimos a primeira flag de usuário, que etá no diretório ~ do nathan:
fe1c24c2ac5e9717f882ef7f11820e5

![ssh](IMG4.png)

Agora, para conseguir a flag de root, presente no diretório /root, precisamo escalonar previlégios. De cara, é poivel perceber que a maquina possui o python3 intalado. E é posível usá-lo para conseguir root, ja que ele está com o cap_setuid e o cap_net_bind_service ativados.

Portanto, uando os comandos python a seguir, é possivel conseguir uma shell com root:
> import os
> os.setuid(0)
> os.system("/bin/bash")

![shell](IMG5.png)

E com isso coneguir a flag de root: d72d6f11cec9c0bae534755b2f190b1c 
