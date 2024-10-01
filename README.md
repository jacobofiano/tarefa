1. Descargar e comprobar que unha imaxe está no teu equipo

Para descargar unha imaxe de Ubuntu e comprobar se xa está no equipo, usa o seguinte comando:

docker pull ubuntu

Isto amosará unha lista de imaxes dispoñibles localmente.

docker images

2. Crear un contedor sen nome. Queda arrincado? Como obtés o nome?

Para crear un contedor sen nome baseado na imaxe de Ubuntu:

docker run -d ubuntu

O contedor quedará arrincado en segundo plano debido á opción -d. Para obter o nome:

docker ps -a

Isto amosará o ID e o nome que Docker asignou automaticamente ao contedor.

3. Crear un contedor co nome 'u1'. Como accedes a el?

Para crear un contedor co nome 'u1' e acceder a el:

docker run -dit --name u1 ubuntu
docker exec -it u1 bash

Agora estarás dentro do contedor, interactuando coa súa terminal.
4. Comprobar a súa IP e facer ping a google.com

Dentro do contedor, obtén a súa IP e fai ping a Google:

apt-get update && apt-get install -y iproute2 iputils-ping

ip addr show: E nu comando utilizado en sistema linux para mostrar informacion sobre as interfaces de rede do sistema, incluindo enderezos  ip, mascaras de subrede e outros detalles.

ping google.com

Agora xa fixemos ping con google

5. Crear un contedor co nome 'bono'. Pódes facer ping entre os contedores?

Para crear outro contedor co nome 'bono':

docker run -dit --name bono ubuntu

Instalar as ferramentas necesarias:

docker exec -it bono bash, apt-get update && apt-get install -y iputils-ping. 
 
Este comando instala o paqueto que proporciona a utilidade ping para verificar a conectividade de rede.

Obtén a IP do contedor 'u1':

docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' u1

Este comando e uilizado para obter a direccion  ip dun contendor docker especifico. A ip e 172.17.0.2

Fai ping desde o contedor 'bono' ao contedor 'u1':

docker exec -it bono bash e ping <172.17.0.2>

6. Que pasa se pechas as terminais?

Se pechas a terminal onde estás interactuando co contedor, este continuará en execución en segundo plano se foi iniciado con -d. Para comprobalo:

docker ps

7. Canta memoria no disco duro ocupaches? Usa docker para calculalo

Para comprobar o espazo ocupado por imaxes, contedores, volumes e redes:

docker system df

Ocupamos en total 89.54 mb de contenedores activos e 339.2mb de imaxes

8. Canta RAM ocupan os contedores? Crea varios para calculalo

Podes ver o uso de memoria dos contedores con:

docker stats

Crea varios contedores para observar o uso de RAM:

docker run -dit --name u2 ubuntu
docker run -dit --name u3 ubuntu
Os dous creados agora ocupan pouca memoria RAM xa que non contenñen nada todavia os demais ocupan 36.61mib bono e 58.24mib
9. Como fixeches para clonar o repositorio?

Para clonar o repositorio usei o comando:

git clone https://github.com/jacobofiano/tarefa.git

10. Como engades o ficheiro readme2.md?

Para engadir o ficheiro readme2.md ao repositorio:

git add readme2.md

11. Pasos para subir o arquivo que estás editando e o ficheiro readme2.md

Para subir os ficheiros ao repositorio remoto:

git add README.md
git commit -m "Engadir os ficheiros README.md e readme2.md"
git push origin main

12. Como comprobarías que existen diferenzas entre o teu repositorio local e o remoto?

Para ver as diferenzas entre o repositorio local e o remoto:

git fetch
git diff origin/master

13. Subir os ficheiros ao repositorio

Unha vez editado o ficheiro README.md e engadido o ficheiro readme2.md, podes realizar o seguinte:

git add nome dos ficheiros
git commit -m "Engadir as respostas da tarefa de Docker"
git push origin master

14. Entregar o repositorio

O URL do meu repositorio sería:


https://github.com/teu-usuario/tarefa-docker

Este sería o enlace que debería compartir para a entrega da tarefa.