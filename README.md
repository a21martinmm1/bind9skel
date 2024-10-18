# Servizos de Rede e Internet Práctica 1.1 Instalación de zonas mestras primarias
O obxectivo desta tarefa é instalar o servidor DNS BIND9 nunha máquina virtual con Debian 12. Podes descargar un esqueleto deste repo de github

https://github.com/brunosct/bind9skel


Partiremos do escenario facilitado.  Antes de comezar comproba que desde ela se pode acceder a Internet. O nome da máquina debe ser "darthvader" e o enderezo IP 192.168.20.10/24.

Podes empregar contedores, con debian 12 e un único interface de rede

Poderás necesitar instalar o paquete dnsutils

Crea un ficheiro Markdown con extension .md coas capturas que fagas para demostrar o funcionamento

1. Instala o servidor BIND9 no equipo darthvader. Comproba que xa funciona coma servidor DNS caché pegando no documento de entrega a saída deste comando dig @localhost www.edu.xunta.es

2. Configura o servidor BIND9 para que empregue como reenviador 8.8.8.8. pegando no documento de entrega contido do ficheiro /etc/bind/named.conf.options e a saída deste comando: dig @localhost www.mecd.gob.es

3. Instala unha zona primaria de resolución directa chamada "starwars.lan" e engade os seguintes rexistros de recursos (a maiores dos rexistros NS e SOA imprescindibles):
  - Tipo A: darthvader con IP 192.168.20.10
  - Tipo A: skywalker con IP 192.168.20.101
  - Tipo A: skywalker con IP 192.168.20.111
  - Tipo A: luke con IP 192.168.20.22
  - Tipo A: darthsidious con IP 192.168.20.11
  - Tipo A: yoda con IP 192.168.20.24 e 192.168.20.25
  - Tipo A: c3p0 con IP 192.168.20.26
  - Tipo CNAME palpatine a darthsidious
  - TIPO MX con prioridade 10 sobre o equipo c3po
  - TIPO TXT "lenda" con "Que a forza te acompanhe"
  - TIPO NS con darthsidious

  Pega no documento de entrega o contido do arquivo de zona, e do arquivo /etc/bind/named.conf.local

4. Instala unha zona de resolución inversa que teña que ver co enderezo do equipo darthvader, e engade rexistros PTR para os rexistros tipo A do exercicio anterior. Pega no documento de entrega o contido do arquivo de zona, e do arquivo /etc/bind/named.conf.local

5. Comproba que podes resolver os distintos rexistros de recursos. Pega no documento de entrega a saída dos comandos:
- nslookup darthvader.starwars.lan localhost
- nslookup skywalker.starwars.lan localhost
- nslookup starwars.lan localhost
- nslookup -q=mx starwars.lan localhost
- nslookup -q=ns starwars.lan localhost
- nslookup -q=soa starwars.lan localhost
- nslookup -q=txt lenda.starwars.lan localhost
- nslookup 192.168.20.11 localhost

# Servizos de Rede e Internet Práctica 1.2 Instalación de zonas secundarias.
Partindo da tarefa 1.1, engadiremos un servidor DNS secundario con BIND9 nunha máquina Debian

1. Tomaremos a máquina darthsidious, e configuraremola para ser servidor secundario, tanto da zona primaria de resolución directa como de resolución inversa. Captura os ficheiros de configuración en ambalas dúas máquinas. Fai unha captura onde se vexa o reinicio da máquina darthsidious, no que se vexa no log dos dous equipos e que se fixo a transferencia de zona.

2. Engade un rexistro tipo A (Chewbacca 192.168.0.28) na zona de resolución directa e tamén na de resolución inversa.  Fai unha captura no momento do reinicio do equipo darthvader, no que se vexa o log dos dous equipos e que se amose que se fixo a transferencia de zona. Adxunta tamén unha captura do ficheiro de zona no servidor secundario.

3. Comproba que o servidor secundario pode resolver ese nome.

4. Fai os cambios necesarios para que as trasferencias se fagan de forma segura empregando chaves.  Repite as capturas e vídeos do punto 2, engadindo o rexistro r2d2 (192.168.0.29)