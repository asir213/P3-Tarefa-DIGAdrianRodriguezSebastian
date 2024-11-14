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

Primeiro TTL significa Time To Live que indica durante canto tempo unha resposta DNS pode ser almacenada en caché polos servidores antes de volverse obsoletea.

dig google.com | grep TTL 
típicamente 300 segundos 

dig facebook.com | grep TTL
típicamente 60 segundos

dig twitter.com | grep TTL
típicamente 60 segundos.

Eu creo que é porque un TTL máis curto permite que os cambios DNS (por exemplo, cambios de IP) se propaguen máis rápido, pero tamén aumenta a carga nos servidores DNS xa que os rexistros deben ser solicitados con máis frecuencia. 

# 9Determina o TTL máximo (original) dun nome de dominio.
dig wikipedia.org +noall +answer +ttlid

wikipedia.org.		198	IN	A	185.15.58.224

Este é o valor actual do TTL (Time to Live) en segundos. Indica que quedan 198 segundos antes de que o rexistro se caduque na caché do servidor DNS resolutor


# 10Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

No meu caso, aparecíame que só a IP 142.250.184.3. Pero as IPs non son sempre as mismas e por tanto varian en cada consulta, polo sistema que usa Google de DNS.

# 11Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo

Utilizamos o comando:

dig @j.root-servers.net www.google.es

;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 26


# 12 Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados

Para ver todas as respuestas do servidor, debemos poñer o comando de dig con un +trace, por exemplo nesta direccion quedaria tal que asi : dig +trace www.timesonline.co.uk

# 13 Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org

Para descubrir estas maquinas debemos comezar polo comando : dig MX danielcastelao.org E como podemos observar na seccion de resposta, as maquinas que nos devolve esta consulta son as seguintes :
danielcastelao.org. 900 IN MX 130 aspmx4.googlemail.com.
danielcastelao.org. 900 IN MX 90 alt1.aspmx.l.google.com.
danielcastelao.org. 900 IN MX 110 aspmx2.googlemail.com.
danielcastelao.org. 900 IN MX 100 alt2.aspmx.l.google.com.
danielcastelao.org. 900 IN MX 140 aspmx5.googlemail.com.
danielcastelao.org. 900 IN MX 80 aspmx.l.google.com.
danielcastelao.org. 900 IN MX 120 aspmx3.googlemail.com.

# 14 Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?

Os rexistros AAAA en DNS corresponden ás direccions IPv6 asociadas co dominio. Para obter ditos rexistros de facebook utilizaremos o seguinte comando : dig AAAA www.facebook.com
