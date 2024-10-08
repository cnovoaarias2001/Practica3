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
Estas son as unicas diferenzas que encontrei.<br><br>

moodle.danielcastela.org<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 21890<br>
;; MSG SIZE  rcvd: 135<br>

www.danielcastela.org<br>
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 19831<br>
;; MSG SIZE  rcvd: 132<br>

**3º Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?**<br>
Co comando `dig ns www.danielcastelao.org`podemos ver os nombres dns<br>
ns1.hover.com. dnsmaster.hover.com.<br>

**4º Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.**<br>
Para realizar as consultas de maneira inversa temos que añadir o parámetro `-x`ao comando anterior `dig -x www.danielcastelao.org`.<br>
**IP 130.206.164.68**<br>
;; ANSWER SECTION:<br>
68.164.206.130.in-addr.arpa. 7200 IN    PTR     pluto.tlm.unavarra.es.<br>
68.164.206.130.in-addr.arpa. 7200 IN    PTR     s164m68.unavarra.es.<br>
**IP 8.8.8.8**<br>
;; ANSWER SECTION:<br>
8.8.8.8.in-addr.arpa.   474     IN      PTR     dns.google.<br>
**IP 130.206.164.2**<br>
;; ANSWER SECTION:<br>
2.164.206.130.in-addr.arpa. 7200 IN     PTR     s164m2.unavarra.es.<br>
**5º A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?**<br>


**6º Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.**<br>


**7º Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?**<br>


**8º Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?**<br>


**9ºDetermina o TTL máximo (original) dun nome de dominio.**<br>


**10º Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?**<br>


**11º Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo.**<br>


**12º Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados**<br>


**13º Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org**<br>


**14º Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?**

