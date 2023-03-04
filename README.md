Pickle Rick es un CTF de nivel inicial de THM, en el cual se nos encomienda convertir nuevamente en humano a rick, que en esos momentos se encuentra convertido en pepinillo. Para esa tarea debemos encontrar en la computadora de Rick los 3 ingredientes necesarios para que este regrese a su estado de humano.
Para ello primero realizamos a enumeración y el reconocimiento del sistema investigado
Enumeración
## nmap
Utilizando el comando `nmap -sC -sV 10.10.242.104 -oN nmapPick` obtenemos los siguientes resultados:

![Pasted image 20230218112511](https://user-images.githubusercontent.com/24280145/222928607-be1992f4-4dd1-4fa3-90a8-a47f34a60522.png)

**puertos abiertos

**http 80
**ssh 22
