**1º Realiza unha consulta "dig danielcastelao.org" e identifica cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)**<br>

**IN, CNAME, A:**<br>
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> danielcastela.org<br>
;; global options: +cmd<br>
;; Got answer:<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 45991<br>
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1<br>

**QUERY SECTION:**<br>
;; Query time: 97 msec<br>

**AUTHORITY SECTION:**<br>
;; AUTHORITY SECTION:<br>
org.                    1800    IN      SOA     a0.org.afilias-nst.info.<br> 
hostmaster.donuts.email. 1728413625 7200 900 1209600 3600<br>

**2º Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org**<br>
Estas son as unicas diferenzas que encontrei.<br>

**moodle.danielcastela.org**<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 21890<br>
;; MSG SIZE  rcvd: 135<br>

**www.danielcastela.org**<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 19831<br>
;; MSG SIZE  rcvd: 132<br>

**3º Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?**<br>
Co comando `dig ns www.danielcastelao.org`podemos ver os nombres dns<br>
ns1.hover.com. dnsmaster.hover.com.<br>

**4º Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.**<br>
Para realizar as consultas de maneira inversa temos que añadir o parámetro `-x`ao comando anterior `dig -x www.danielcastelao.org`.<br><br>
**IP 130.206.164.68**<br>
;; ANSWER SECTION:<br>
68.164.206.130.in-addr.arpa. 7200 IN    PTR     pluto.tlm.unavarra.es.<br>
68.164.206.130.in-addr.arpa. 7200 IN    PTR     s164m68.unavarra.es.<br><br>
**IP 8.8.8.8**<br>
;; ANSWER SECTION:<br>
8.8.8.8.in-addr.arpa.   474     IN      PTR     dns.google.<br><br>
**IP 130.206.164.2**<br>
;; ANSWER SECTION:<br>
2.164.206.130.in-addr.arpa. 7200 IN     PTR     s164m2.unavarra.es.<br><br>

**5º A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?**<br>
Co comando `cat /etc/resolv.conf` poderiamos ver que o DNS co que estamos consultando.<br>

Para poder cambiar o DNS o podemos facer con `@` antes do comando `dig` e seguido da IP do DNS que queremos consultar: `dig @8.8.8.8 danielcastelao.org`. <br>

**6º Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.**<br><br>

**dig @8.8.8.8 SOA moddle.danielcastelao.org**<br>
; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> @8.8.8.8 SOA moddle.danielcastelao.org<br>
; (1 server found)<br>
;; global options: +cmd<br>
;; Got answer:<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 9597<br>
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1<br><br>

;; OPT PSEUDOSECTION:<br>
; EDNS: version: 0, flags:; udp: 1220<br>
; COOKIE: 8be52bc7e732c5474cc78c5d670e9934ed72703c67d27c8e (good)<br>
;; QUESTION SECTION:<br>
;moddle.danielcastelao.org.     IN      SOA<br><br>

;; AUTHORITY SECTION:<br>
danielcastelao.org.     300     IN      SOA     ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 <br>300<br><br>

;; Query time: 140 msec<br>
;; SERVER: 8.8.8.8#53(8.8.8.8) (UDP)<br>
;; WHEN: Tue Oct 15 18:32:52 CEST 2024<br>
;; MSG SIZE  rcvd: 141<br><br>

**dig @ns1.dreamhost.com SOA moodle.danielcastelao.org**<br><br>

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> @ns1.dreamhost.com SOA moodle.danielcastelao.org<br>
; (1 server found)<br>
;; global options: +cmd<br>
;; Got answer:<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 31518<br>
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1<br><br>

;; OPT PSEUDOSECTION:<br>
; EDNS: version: 0, flags:; udp: 1220<br>
; COOKIE: 6ac00a6855b9386f5ea9c793670e9b32763f09a5c3375317 (good)<br>
;; QUESTION SECTION:<br>
;moodle.danielcastelao.org.     IN      SOA<br><br>

;; AUTHORITY SECTION:<br>
danielcastelao.org.     5       IN      SOA     ns1.hover.com. dnsmaster.hover.com. 1720467415 1800 900 604800 <br>300<br><br>

;; Query time: 6 msec<br>
;; SERVER: 162.159.26.14#53(ns1.dreamhost.com) (UDP)<br>
;; WHEN: Tue Oct 15 18:41:22 CEST 2024<br>
;; MSG SIZE  rcvd: 141<br><br>

**7º Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?**<br><br>
;; ANSWER SECTION:<br>
www.elpais.com.         168     IN      CNAME   prisa-us-eu.map.fastly.net.<br>
prisa-us-eu.map.fastly.net. 11  IN      A       199.232.194.133<br>
prisa-us-eu.map.fastly.net. 11  IN      A       199.232.198.133<br><br>

Ao lanzar o comando `dig www.elpais.com` podemos ver o tempo no que guarda en caché que neste caso e 168 segundos.<br><br>
**8º Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?**<br><br>
**`dig www.marca.com`**<br><br>
;; ANSWER SECTION:<br>
www.marca.com.          131     IN      CNAME   unidadeditorial.map.fastly.net.<br>
unidadeditorial.map.fastly.net. 58 IN   A       199.232.197.50<br>
unidadeditorial.map.fastly.net. 58 IN   A       199.232.193.50<br><br>

**`dig www.elmundo.es`**<br><br>
;; ANSWER SECTION:<br>
www.elmundo.es.         74      IN      CNAME   unidadeditorial.map.fastly.net.<br>
unidadeditorial.map.fastly.net. 24 IN   A       151.101.133.50br><br><br>

As diferenzas se debe a que non a garda no caché a de <br><br>

**9ºDetermina o TTL máximo (original) dun nome de dominio.**<br><br>
;; ANSWER SECTION:<br>
www.google.es.          68      IN      A       142.250.184.163<br>
El TLL es de 68 segundos.<br><br>

**10º Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?**<br><br>

Neste caso utilizaremos `dig www.google.com +short` para ver as maquinas asociadas ao dominio google e neste caso so temos una máquina asociada al dominio pero poden ser varias.<br><br>
**`dig www.google.com +short`**
dig www.google.com +short<br>
216.58.215.132<br>


**11º Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo.**<br><br>

Co comando `dig @J.ROOT-SERVERS.NET www.danielcastelao.org` podemos ver si acepta o modo recursivo el cual si lo acepta ya que en el apartado `flags` está el atributo `ra`.<br> 
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1<br><br>

**12º Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados**<br><br>

Para ver todas as consultas simplemente añadimos al dig `+trace`.<br><br>
`dig www.timesonline.co.uk +trace`<br><br>

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> www.timesonline.co.uk +trace<br>
;; global options: +cmd<br>
.                       3983    IN      NS      f.root-servers.net.<br>
.                       3983    IN      NS      a.root-servers.net.<br>
.                       3983    IN      NS      k.root-servers.net.<br>
.                       3983    IN      NS      d.root-servers.net.<br>
.                       3983    IN      NS      c.root-servers.net.<br>
.                       3983    IN      NS      j.root-servers.net.<br>
.                       3983    IN      NS      g.root-servers.net.<br>
.                       3983    IN      NS      b.root-servers.net.<br>
.                       3983    IN      NS      l.root-servers.net.<br>
.                       3983    IN      NS      e.root-servers.net.<br>
.                       3983    IN      NS      h.root-servers.net.<br>
.                       3983    IN      NS      i.root-servers.net.<br>
.                       3983    IN      NS      m.root-servers.net.<br>
;; Received 239 bytes from 127.0.0.53#53(127.0.0.53) in 14 ms<br><br>

;; communications error to 198.97.190.53#53: timed out<br>
uk.                     172800  IN      NS      nsa.nic.uk.<br>
uk.                     172800  IN      NS      nsb.nic.uk.<br>
uk.                     172800  IN      NS      nsc.nic.uk.<br>
uk.                     172800  IN      NS      nsd.nic.uk.<br>
uk.                     172800  IN      NS      dns1.nic.uk.<br>
uk.                     172800  IN      NS      dns2.nic.uk.<br>
uk.                     172800  IN      NS      dns3.nic.uk.<br>
uk.                     172800  IN      NS      dns4.nic.uk.<br>
uk.                     86400   IN      DS      43876 8 2 <br>A107ED2AC1BD14D924173BC7E827A1153582072394F9272BA37E2353 BC659603<br>
uk.                     86400   IN      RRSIG   DS 8 1 86400 20241028050000 20241015040000 61050 . vgPsl<br>+2ZwsSpGX+dUWh7ClhWO+3m73LcZegTxWlhcvsINin1jO5TXpnp dGEFfXY415h4egrJwczxzdnTM35HGyqYoqkDbbztZJNHOgmqp21iXnvP <br>JKa2suj+b1vTiAN4+8Q+gq4OWhKn29GOiWC/qqU0vymFKHTY9Xq1Ds4Z VR/Q9GhUi/WPxrxXJyFG0tvP3Zh<br>+gEM4t9rPp2btnWtsVpHC7UtxI0Lq D7YoMOKMz3CI+KrU90QdUbDUrFSE7bwXImj3ZRe4r2gwCiooPuqHZYp7 /<br>qZVzS2dJisjaV6XJUbRYv9f0RmbZMIFcQ/iipxE3Q8u1q1kIFuoK1Xj KI6zvg==<br>
;; Received 889 bytes from 198.97.190.53#53(h.root-servers.net) in 119 ms<br><br>

;; Received 50 bytes from 156.154.100.3#53(nsa.nic.uk) in 3 ms<br><br>


**13º Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org**<br><br>
Estos son todos os servidores de correo do dominio danielcastelao.org<br><br>
 
`dig MX danielcastelao.org`<br><br>

;; ANSWER SECTION:<br>
danielcastelao.org.     900     IN      MX      120 aspmx3.googlemail.com.<br>
danielcastelao.org.     900     IN      MX      90 alt1.aspmx.l.google.com.<br>
danielcastelao.org.     900     IN      MX      110 aspmx2.googlemail.com.<br>
danielcastelao.org.     900     IN      MX      100 alt2.aspmx.l.google.com.<br>
danielcastelao.org.     900     IN      MX      80 aspmx.l.google.com.<br>
danielcastelao.org.     900     IN      MX      130 aspmx4.googlemail.com.<br>
danielcastelao.org.     900     IN      MX      140 aspmx5.googlemail.com.<br><br>


**14º Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?**<br><br>
Corresponde `www.facebook.com.       1235    IN      CNAME   star-mini.c10r.facebook.com.`<br><br>

`dig AAAA www.facebook.com`<br><br>

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> AAAA www.facebook.com<br>
;; global options: +cmd<br>
;; Got answer:<br>
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45823<br>
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1<br><br>

;; OPT PSEUDOSECTION:<br>
; EDNS: version: 0, flags:; udp: 65494<br>
;; QUESTION SECTION:<br>
;www.facebook.com.              IN      AAAA<br><br>

;; ANSWER SECTION:<br>
www.facebook.com.       1235    IN      CNAME   star-mini.c10r.facebook.com.<br><br>

;; Query time: 10 msec<br><br>
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)<br>
;; WHEN: Tue Oct 15 21:01:14 CEST 2024<br>
;; MSG SIZE  rcvd: 74