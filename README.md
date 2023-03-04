Pickle Rick es un CTF de nivel inicial de THM, en el cual se nos encomienda convertir nuevamente en humano a rick, que en esos momentos se encuentra convertido en pepinillo. Para esa tarea debemos encontrar en la computadora de Rick los 3 ingredientes necesarios para que este regrese a su estado de humano.
Para ello primero realizamos a enumeración y el reconocimiento del sistema investigado
Enumeración
## nmap
Utilizando el comando `nmap -sC -sV 10.10.242.104 -oN nmapPick` obtenemos los siguientes resultados:

![Pasted image 20230218112511](https://user-images.githubusercontent.com/24280145/222928607-be1992f4-4dd1-4fa3-90a8-a47f34a60522.png)

**puertos abiertos**

`http 80`

`ssh 22`

## curl
utilizando el comando  `curl 10.10.242.104 > cPick`

![Pasted image 20230218110137](https://user-images.githubusercontent.com/24280145/222929129-a3ba3365-6c73-4dac-93e1-e80f1da6bb2b.png)

Encontramos un nombre de usuario en el documento HTML 

`Username: R1ckRul3s`


## Gobuster
Utilizando el comando `gobuster -u http://10.10.242.104 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt` obtenemos lo siguiente

![Pasted image 20230218113243](https://user-images.githubusercontent.com/24280145/222929984-b355969d-1b50-49a6-a771-f3c85499b9b2.png)

Buscamos directorios con extensión .php y .html  `gobuster -u http://10.10.242.104 -t 50 -w /usr/share/wordlists/dirbuster/common.txt -x .php,.html`

**Nota**: La lista common.txt fue extraida de: https://gitlab.com/kalilinux/packages/dirb/blob/f43c03a2bef91118debffd6cec9573f21bb5f9e8/wordlists/common.txt

Utilizamos el comando `sudo mv common.txt /usr/share/wordlists/dirbuster/common.txt` para mover el archivo a la carpeta dirbuster (no es obligatorio)

![Pasted image 20230218120112](https://user-images.githubusercontent.com/24280145/222931429-c6f3160d-2b68-4314-8626-86964a4cc6de.png)

Con este informe conocemos que:
**index.html**: Es la página de inicio
**robots.txt**: contiene la cadena *Wubbalubbadubdub*
**login.php**: Nos muestra el siguietne acceso:


![Pasted image 20230218121122](https://user-images.githubusercontent.com/24280145/222931472-ad4667ac-1308-471a-8f55-769c46c0aebe.png)

# Obtención de acceso
Utilizando el username encontrado en el código *html de la web* y la cadena encontrada en *robots.txt*. Accedemos como usuarios del sistema en el **Potal Login Page**:

`username: R1ckRul3s`

`password: Wubbalubbadubdub`

![Pasted image 20230218121459](https://user-images.githubusercontent.com/24280145/222931603-18fac2c4-282a-44c7-b3c7-8ca1131fdee5.png)

### Ejecutando comandos

`whoami`

![Pasted image 20230218122054](https://user-images.githubusercontent.com/24280145/222931694-116e2af5-70e2-4953-9cba-38fac3088d00.png)

`pwd`


![Pasted image 20230218122147](https://user-images.githubusercontent.com/24280145/222931709-50e0e38b-7484-4872-9cac-169d3a2421e5.png)

`ls`

![Pasted image 20230218122256](https://user-images.githubusercontent.com/24280145/222931737-3a581e02-86e7-4dac-ac5d-5e128010fe91.png)

¡¡hemos hallado el primer ingrediente...¡¡ pero los comandos estan filtrados de lectura de texto, y no podemos ver el contenido del fichero que contiene el segundo ingrediente

![Pasted image 20230218122725](https://user-images.githubusercontent.com/24280145/222931819-4bf64ac4-2de0-435b-a6ac-f7fe8f0ad763.png)

En este escenario podemos buscar nuevas soluciones (como acceder al sistema) o buscar un comando que si funcione (no este filtrado). realizando la prueba con los comandos `more`,`head`,`vim` ... Realizando prueba y error hallamos el comando `tac`. 


**Nota**: Para conocer los comandos de lectura de texto podemos visitar: https://www.geeksforgeeks.org/tac-command-in-linux-with-examples/

