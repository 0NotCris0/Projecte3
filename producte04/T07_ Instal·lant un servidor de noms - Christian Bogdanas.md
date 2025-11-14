

**Accions a realitzar**

1. Configurar l’arxiu **named.conf.options** perquè accepti consultes recursives de la seva xarxa local, haurà d’usar com reenviador la IP 8.8.8.8. Mostra la captura. Un cop fet, reiniciar el servei i comprovar que funciona (mostra l’estat).  
2. Utilitzar un client, pot ser la màquina Zorin que has usat anteriorment, canviant l’adaptador a **adaptador pont**. La configuració que s’haurà d’utilitzar s’indicarà a l’inici del repte, però cal que servidor de noms (DNS) sigui la IP del vostre servidor. Comprova que el client té resolució a Internet (obrir una pàgina al navegador o fes un dig google.com)  
3. Editar l’arxiu **named.conf.local** per definir dues zones, les corresponents a la **zona directa** del domini **digicore-XX.test** i la corresponent a la **zona inversa** de la xarxa local, a la prova de concepte, l’adreça de xarxa local que s’està utilitzant.  
4. Crear l’arxiu corresponent a la zona directa (ha d’estar dins una carpeta que s’anomenarà **zones** que cal crear prèviament a /etc/bind. Per comoditat els pot crear copiant l’arxiu **db.local**.  
5. Configurar aquest arxiu amb els següents registres:  
   1. SOA (amb les dades correctament configurades)  
   2. NS que sigui el vostre servidor  
   3. Un registre A anomenat **server** amb la IP del servidor.  
   4. Un registre A anomenat **dbserver** amb la IP del client.  
   5. Un registre àlies (CNAME) amb nom **data** al registre **dbserver**  
6. Crear l’arxiu corresponent a la zona inversa (ha d’estar dins una carpeta que s’anomenarà **zones** que cal crear prèviament a /etc/bind. Per comoditat es pot crear copiant l’arxiu **db.127.**  
7. Configurar aquest arxiu:  
   1. SOA i NS adients.  
   2. Registres PTR corresponents al **server** i al **dbserver**.  
8. Reiniciar servei i fer les comprovacions des del client als diferents fent consultes directes i inverses.  
9. Editar l’arxiu **named.conf.local** per permetre la transferència  de la zona directa als companys de l’equip.  
10. Fer les configuracions necessàries per tenir una zona secundària del domini d’un dels companys. Forçar la transferència i comprovar el funcionament des del client.

![][image1]

![][image2]

![][image3]

![][image4]

![][image5]

![][image6]

![][image7]

![][image8]

![][image9]

![][image10]

![][image11]

![][image9]

![][image12]

![][image13]

![][image14]

![][image15]

![][image16]

![][image17]

![][image18]

![][image19]

![][image20]

![][image21]

![][image22]

![][image23]

![][image24]

![][image25]

![][image26]

![][image27]

![][image28]

![][image29]

![][image30]

![][image31]

![][image32]

![][image33]

![][image34]

![][image35]

![][image36]

![][image37]

![][image38]

![][image39]

![][image40]

![][image41]

![][image42]

