ChatGPT
1. Consulta "dig danielcastelao.org"

Ejecutamos el comando:dig danielcastelao.org

QUESTION SECTION: Es la parte de la consulta. Aquí se especifica qué dominio estamos consultando y qué tipo de registro buscamos (en este caso, un registro A, que nos dará la IP asociada).

IN: Indica que estamos trabajando en el espacio de nombres de Internet.
A: Registro A, que contiene la dirección IP.

ANSWER SECTION: Es la respuesta a la consulta. Aquí se muestra la IP del dominio consultado.
danielcastelao.org. 3600 IN A 213.60.236.57: El dominio danielcastelao.org tiene la IP 213.60.236.57 con un TTL (Time To Live) de 3600 segundos.

AUTHORITY SECTION: Muestra los servidores de nombres autoritativos para el dominio.
NS: Registros de servidores de nombres (Name Server) que son autoritativos para el dominio.

ADDITIONAL SECTION: Muestra información adicional como las IPs de los servidores de nombres autoritativos.

2. Consultas a "moodle.danielcastelao.org" y "www.danielcastelao.org"
dig moodle.danielcastelao.org:

el nombre moodle.danielcastelao.org es un CNAME (alias) que apunta a aula.danielcastelao.org, que a su vez tiene una IP asociada (213.60.236.58).

dig www.danielcastelao.org:
www.danielcastelao.org tiene un registro A directamente asociado con la IP 213.60.236.57.

3. Nombre e IP de los servidores DNS autoritativos de www.danielcastelao.org

Ejecutamos el comando:
dig ns www.danielcastelao.org
Los servidores autoritativos son:

ns1.dominioabsoluto.com (IP: 213.60.236.50)
ns2.dominioabsoluto.com (IP: 213.60.236.51)

Por qué suelen ser 2 servidores autoritativos?

Para redundancia y disponibilidad. Si uno de los servidores falla, el otro puede seguir respondiendo a las consultas DNS.

4. Consultas inversas

Para realizar consultas inversas (obtener el nombre de dominio asociado a una IP), usamos el comando dig con la opción -x:
IP: 130.206.164.68

dig -x 130.206.164.68
El nombre de dominio asociado a la IP 130.206.164.68 es irene.dit.upm.es.

Otras IPs:
IP: 8.8.8.8

dig -x 8.8.8.8
El nombre asociado a la IP 8.8.8.8 es dns.google.
dig -x 1.1.1.1
El nombre asociado a la IP 1.1.1.1 es one.one.one.one.
5. ¿A qué servidor DNS estás consultando? ¿Cómo cambiarlo sin tocar los ficheros de configuración?

Para saber qué servidor DNS estás utilizando, puedes usar el comando:

nmcli dev show | grep DNS

Si quieres cambiar temporalmente el servidor DNS sin modificar archivos de configuración, puedes usar el comando dig con la opción @

dig @8.8.8.8 www.danielcastelao.org

Esto enviará la consulta al servidor DNS de Google (8.8.8.8), sin alterar la configuración del sistema.

6. Obtener el registro SOA de moodle.danielcastelao.org

Primero, con el servidor DNS de Google:

dig @8.8.8.8 moodle.danielcastelao.org SOA

Ahora, consultando directamente el servidor primario (ns1.dominioabsoluto.com):
dig @ns1.dominioabsoluto.com moodle.

danielcastelao.org SOA

El registro SOA contiene información sobre el servidor primario y los tiempos de refresco del dominio.
7. Consulta la IP de www.elpais.com y el TTL

dig www.elpais.com

En la respuesta, verás el campo TTL:
El TTL (1000 segundos en este caso) indica cuánto tiempo se almacena la respuesta en la caché DNS. Si consultas nuevamente antes de que expire el TTL, obtendrás la misma respuesta sin que se consulte a un servidor autoritativo.

8. TTL de distintos nombres de dominio

Para obtener el TTL de distintos dominios, usa el comando dig. Por ejemplo:

dig google.com
dig facebook.com
Los TTL pueden variar dependiendo de las políticas de caché de cada dominio. Los servicios que cambian frecuentemente sus IPs (como servidores de contenido o CDN) suelen tener TTLs más bajos.

9. TTL máximo (original)

El TTL máximo se puede consultar usando dig. 
Es el valor mostrado en la respuesta antes de que se cachee. Generalmente, los TTLs originales pueden ser de horas o días.
10. Máquinas detrás de www.google.es

dig www.google.es

Al consultar este dominio varias veces, obtendrás diferentes IPs en cada