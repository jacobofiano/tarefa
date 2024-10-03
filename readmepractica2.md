1. Para comprobar se temos a imaxe httpd introducimos o seguinte comando:
docker images
2. *Crear o primeiro contedor: asir_httpd*

Este contedor executará Apache HTTPD, mapeando o porto 80 do contedor co porto 8080 da túa máquina e montando o directorio htdocs dun directorio da túa máquina. Primeiro, asegurate de estar no directorio onde queiras montar o teu volume.

3. *Crear o directorio htdocs no directorio actual:*

mkdir -p htdocs
4. *Crear un arquivo HTML básico dentro deste directorio.*
Executar o seguinte comando para crear o contedor asir_httpd:docker run --name asir_httpd -d -p 8080:80 -v "$PWD/htdocs:/usr/local/apache2/htdocs" httpd

Neste comando:

--name asir_httpd dá nome ao contedor.
-d executa o contedor en modo detached.
-p 8080:80 mapea o porto 80 do contedor ao 8080 da túa máquina.
-v "$PWD/htdocs:/usr/local/apache2/htdocs" fai o bind mount do directorio htdocs ao directorio de Apache htdocs.

Agora podes comprobar se funciona accedendo a http://localhost:8080 no teu navegador.
5. *Crear o contedor asir_web1 no porto 8000*

Agora que temos un directorio htdocs preparado, podemos reutilizalo para crear outro contedor, asir_web1, co porto 8000:

docker run --name asir_web1 -d -p 8000:80 -v "$PWD/htdocs:/usr/local/apache2/htdocs" httpd

Este comando é similar ao anterior, pero mapea o porto 8000 no host co porto 80 do contedor.
Comproba o contedor en http://localhost:8000.4. 

6. *Crear o contedor asir_web2 no porto 8090*

Para o terceiro contedor, seguimos os mesmos pasos, pero mapeamos o porto 8090:

docker run --name asir_web2 -d -p 8090:80 -v "$PWD/htdocs:/usr/local/apache2/htdocs" httpd

Comproba o contedor en http://localhost:8090.
7. Verificar o estado dos contedores
Para comprobar que todos os contedores están en execución, podes usar:

docker ps

Debes ver tres contedores en execución: asir_httpd, asir_web1, e asir_web2, cada un mapeando diferentes portos.