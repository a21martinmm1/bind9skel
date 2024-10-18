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

# Servizos de Rede e Internet Práctica 1.2 Instalación de zonas mestras primarias en Windows Server
O obxectivo desta tarefa é instalar o servidor DNS  nunha máquina Windows 2019 Server.

Partiremos dunha máquina virtual con Windows 2019 cun único adaptador en modo so anfitrión Antes de comezar comproba que desde ela se pode acceder a Internet. O nome da máquina debe ser "lukeskywalker" e o enderezo IP 192.168.20.101/24.

Deberás entregar un único documento de Google Drive onde pegues o resultado de cada unha das tarefas.


1. Instala o servidor DNS no equipo lukeskywalker. Comproba que xa funciona coma servidor DNS caché pegando no documento de entrega a saída deste comando  nslookup -norecurse www.starwars.com localhost

2. Configura o servidor DNS para que empregue como reenviador 8.8.8.8. pegando no documento de entrega a captura de pantalla da configuración do reenviador e a saída deste comando: nslookup -recurse www.starwars.com localhost

3. Instala unha zona primaria de resolución directa chamada "academia.jedi" e engade os seguintes rexistros de recursos (a maiores dos rexistros NS e SOA imprescindibles):
- Tipo A: lukeskywalker con IP 192.168.20.101
- Tipo A: benskywalker con IP 192.168.20.102
- Tipo A: obiwankenobi con IP 192.168.56.152 e 192.168.56.153
- Tipo A: hansolo con IP 192.168.56.105
- Tipo A: leia con IP 192.168.56.106
- Tipo A: anakinsolo con IP 192.168.56.106
- Tipo CNAME mestrejedi a obiwankenobi
- TIPO MX con prioridade 10 sobre o equipo hansolo
- TIPO TXT "thon" con "un Jedi debe sentir a tensión entre os dous lados da Forza"
- TIPO NS con benskywalker
- Pega no documento de entrega a captura dos rexistros creados

4. Instala unha zona de resolución inversa que teña que ver co enderezo do equipo lukeskywalker, e engade rexistros PTR para os rexistros tipo A do exercicio anterior. Pega no documento de entrega o a captura dos rexistros da zona.

5. Comproba que podes resolver os distintos rexistros de recursos. Pega no documento de entrega a saída dos comandos:
- nslookup lukeskywalker.academia.jedi localhost
- nslookup hansolo.academia.jedi localhost
- nslookup leia.academia.jedi localhost
- nslookup anakinsolo.academia.jedi localhost
- nslookup academia.jedi localhost
- nslookup -q=mx academia.jedi localhost
- nslookup -q=ns academia.jedi localhost
- nslookup -q=soa academia.jedi localhost
- nslookup -q=txt thon.academia.jedi localhost
- nslookup 192.168.56.101 localhost

# Servizos de Rede e Internet Práctica 1.3 Instalación de zonas secundarias.
Partindo da tarefa 1.1, engadiremos un servidor DNS secundario con BIND9 nunha máquina Debian

1. Tomaremos a máquina darthsidious, e configuraremola para ser servidor secundario, tanto da zona primaria de resolución directa como de resolución inversa. Captura os ficheiros de configuración en ambalas dúas máquinas. Fai unha captura onde se vexa o reinicio da máquina darthsidious, no que se vexa no log dos dous equipos e que se fixo a transferencia de zona.

2. Engade un rexistro tipo A (Chewbacca 192.168.0.28) na zona de resolución directa e tamén na de resolución inversa.  Fai unha captura no momento do reinicio do equipo darthvader, no que se vexa o log dos dous equipos e que se amose que se fixo a transferencia de zona. Adxunta tamén unha captura do ficheiro de zona no servidor secundario.

3. Comproba que o servidor secundario pode resolver ese nome.

4. Fai os cambios necesarios para que as trasferencias se fagan de forma segura empregando chaves.  Repite as capturas e vídeos do punto 2, engadindo o rexistro r2d2 (192.168.0.29)