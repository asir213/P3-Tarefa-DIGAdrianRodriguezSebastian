# Tarefa-DIG


# 1 Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)

IN: Clase da resposta (Internet).

CNAME: O rexistro CNAME úsase cando un dominio é un alias doutro dominio, e se devolvería na ANSWER SECTION se existise.

Query section: Query time-> 121 msec

ANSWER section: danielcastelao.org.	900	IN	A	178.211.133.37

Authority Section: AUTHORITY: 0
, o 0  indica que non hai información de autoridade. O servidor devolveu correctamente a dirección IP do dominio, pero non indica quen é responsable do dominio.

A: Tipo de rexistro, que neste caso devolve unha dirección IPv4.


# 2 Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org  
Tipo de rexistro:

    O rexistro de moodle.danielcastelao.org pode ser un A ou CNAME, dependendo de como está configurado.
    O rexistro de www.danielcastelao.org normalmente sería un A ou un CNAME apuntando a outro dominio.

    Presence de CNAME:

    O moddel e un subdominio do outro dominio a través dun rexistro CNAME.

# 3  Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?
Mediante o uso do seguinte comando poderemos ver os servers que son autoritativos para o dominio danielcastelao.org

dig ns danielcastelao.org

Os nomes son 
ns2.hover.com.
ns1.hover.com
As IPs respectivamente
64.98.148.13
216.40.47.26

Unha vez que temos os nomes dos servidores autoritativos, podemos obter os seus IPs co seguinte comando:

dig A nome do servidor

Por que adoitan ser 2 servidores autoritativos?

Alta dispoñibilidade: Se un dos servidores DNS falla ou deixa de estar accesible, o outro servidor autoritativo pode seguir respondendo ás consultas. 



# 4 Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.

Abre o terminal e introduce o seguinte comando:
dig -x 130.206.164.68
pluto.tlm.unavarra.es e s164m68.unavarra.es

dig -x 130.206.164.79 
s166m78.unavarra.es.

dig -x 130.206.164.70
s168m79.unavarra.es

# 5 A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?
mediante el uso del comando cat /etc/resolv.conf 
nameserver 127.0.0.53

# 6 Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.

Abre o terminal e usa o seguinte comando para preguntar ao servidor DNS de Google (8.8.8.8):
dig @8.8.8.8 moodle.danielcastelao.org SOA

# 7 Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?

Usando o comando dig www.elpais.com podemos ver o rexistro

www.elpais.com.		7	IN	CNAME	prisa-us-eu.map.fastly.net.

Neste caso o tempo no cache sera de 7 segundos



# 8 Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?

Determina o TTL máximo (original) dun nome de dominio.
Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

    Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo
    Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados
     Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org
    Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
