# **T04: Serveis de Directori - LDAP**

Autor: *Christian Bogdanas*

---

## 1. Objecte de l’Encàrrec

Creem una màquina amb **Ubuntu Server**.

![Imatge 1](img/1.png)

En entrar a la màquina, el primer que farem serà executar un `sudo apt update && sudo apt upgrade` per actualitzar els paquets i evitar possibles errors més endavant.

![Imatge 2](img/2.png)

A continuació, editem el domini amb la comanda:

```
sudo nano /etc/hosts
```

![Imatge 3](img/3.png)

Configurem el fitxer com s’indica a continuació.

![Imatge 4](img/4.png)

Comprovem que s’hagi actualitzat correctament:

![Imatge 5](img/5.png)  
![Imatge 6](img/6.png)

---

## 2. Requeriments d’Infraestructura Inicial

El pas següent és configurar la màquina virtual.  
Anirem a la configuració de xarxa i posarem el **primer adaptador en NAT** i el **segon en mode només amfitrió (Host-Only)**.

![Imatge 7](img/7.png)  
![Imatge 8](img/8.png)

Després de configurar el mode Host-Only, editarem la interfície de xarxa amb:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

![Imatge 9](img/9.png)

Afegirem la interfície `enp0s8` i l’opció `dhcp4: true`.

![Imatge 10](img/10.png)

Desarem els canvis amb:

```
sudo netplan apply
```

![Imatge 11](img/11.png)

Finalment, comprovarem amb `ip a` que la configuració s’ha aplicat correctament.

---

## 3. Tasques d'Implementació i Configuració del Servidor LDAP

### 3.1. Instal·lació i Configuració Bàsica d’OpenLDAP

Instal·lem el servidor i les utilitats LDAP amb la comanda:

```
sudo apt install slapd ldap-utils -y
```

![Imatge 12](img/12.png)

Durant la instal·lació, se’ns demanarà establir una contrasenya per a l’administrador. Seguint el plec de condicions, farem servir **p@ssw0rd**.

![Imatge 13](img/13.png)

Comprovem que el servei està actiu:

```
systemctl status slapd
```

![Imatge 14](img/14.png)

Podem visualitzar la configuració amb:

```
sudo slapcat
```

![Imatge 15](img/15.png)

Si el directori no s’ha creat correctament, podem reconfigurar el servei amb:

```
sudo dpkg-reconfigure slapd
```

Crearem dues unitats organitzatives: **users** i **groups**. Per fer-ho, generem un fitxer `OU_users.ldif`.

![Imatge 16](img/16.png)

Editem el fitxer i afegim les OUs corresponents:

![Imatge 17](img/17.png)

Afegim les noves OUs amb:

![Imatge 18](img/18.png)

Comprovem que s’han creat correctament:

![Imatge 19](img/19.png)

---

### 3.2. Gestió i Administració amb LAM

Per facilitar l’administració del servidor, farem servir **LDAP Account Manager (LAM)**.  
Primer, instal·lem el paquet necessari:

![Imatge 20](img/20.png)

Obtenim la IP del servidor amb `ip a` per poder accedir-hi des del navegador:

![Imatge 21](img/21.png)

Accedim a la pàgina del LAM escrivint a l’adreça del navegador:

```
http://<ip_del_servidor>/lam
```

![Imatge 22](img/22.png)

Entrem a **LAM Configuration** → **Edit Server Profiles**.

![Imatge 23](img/23.png)

La contrasenya per defecte és `lam`.

![Imatge 24](img/24.png)

Configurem l’idioma, el compte d’administrador i altres paràmetres generals.

![Imatge 25](img/25.png)  
![Imatge 26](img/26.png)

Definim els **Domain Names (DN)** per als usuaris i grups amb les seves respectives OUs.

![Imatge 27](img/27.png)

Guardem els canvis.

![Imatge 28](img/28.png)

Ara ja podem iniciar sessió com a administrador (`admin`) amb la contrasenya `p@ssw0rd`.

![Imatge 29](img/29.png)

Per crear grups, accedim a **Comptes → Grups**, i creem dos grups: `tech` i `manager`.

![Imatge 30](img/30.png)  
![Imatge 31](img/31.png)

Podem veure el missatge de confirmació de creació del grup.

![Imatge 32](img/32.png)

Per crear usuaris, anem a **Comptes → Usuaris** i creem `tech01` i `manager01`.

![Imatge 33](img/33.png)  
![Imatge 34](img/34.png)

Assignem a cada usuari el seu grup principal i grups addicionals segons correspongui.

![Imatge 35](img/35.png)  
![Imatge 36](img/36.png)

I li posarem el grup tech en els grups addicionals, el que vam crear.

![Imatge 37](img/37.png) 

Creem la contrasenya per a l’usuari (`1234`) i la desem.

 
![Imatge 38](img/38.png)

I guardem.

![Imatge 39](img/39.png)  

Repetim el procés amb `manager01`.


![Imatge 40](img/40.png)  
![Imatge 41](img/41.png)  
![Imatge 42](img/42.png)
![Imatge 43](img/43.png)

---

## 4. Integració del Client (Ubuntu Desktop)

Comprovarem que el servidor LDAP funciona correctament configurant un client **Zorin OS** amb les següents característiques:

El primer adaptador serà **NAT** i el segon **Host-Only**.

![Imatge 44](img/44.png)
![Imatge 45](img/45.png) 

Configurem la interfície de xarxa:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```
 
![Imatge 46](img/46.png)
![Imatge 47](img/47.png)

Desem amb:

```
sudo netplan apply
```
![Imatge 48](img/48.png)  


Editem el fitxer `/etc/hosts` per configurar el nom del equip perque formi part del mateix domini que el servidor.


![Imatge 49](img/49.png)

![Imatge 50](img/50.png)

Comprovem que el nom del dispositiu s’ha actualitzat correctament.

![Imatge 51](img/51.png) 

Creem una instantània de la màquina per seguretat.

 
![Imatge 52](img/52.png)

![Imatge 53](img/53.png)

Verifiquem la resolució DNS amb:

```
dig server.innovatech05.test
```

![Imatge 54](img/54.png)

Fem una consulta LDAP des del client per comprovar la connectivitat:

```
ldapsearch -x
```
![Imatge 55](img/55.png)  


Instal·lem els mòduls necessaris per integrar el client al domini:


![Imatge 56](img/56.png)  
![Imatge 57](img/57.png)  
![Imatge 58](img/58.png)  
![Imatge 59](img/59.png)  
![Imatge 60](img/60.png)  
![Imatge 61](img/61.png)  
![Imatge 62](img/62.png)
![Imatge 63](img/63.png)  

Editem `nsswitch.conf` per permetre la gestió d’usuaris i grups via LDAP:


![Imatge 64](img/64.png)
![Imatge 65](img/65.png)

Modifiquem `common-password` eliminant la línia `use_authok`:

  
![Imatge 66](img/66.png)
![Imatge 67](img/67.png)  

Editarem `common-session` i afegirem la línia següent per crear automàticament els perfils d’usuari:

```
session optional pam_mkhomedir.so skel=/etc/skel umask=077
```


![Imatge 68](img/68.png)
![Imatge 69](img/69.png)

Reiniciem el servei:

![Imatge 70](img/70.png)

Comprovem que el sistema detecta correctament els usuaris LDAP:

![Imatge 71](img/71.png) 

Per permetre l’inici de sessió gràfica dels usuaris de domini, editem el fitxer corresponent:

 
![Imatge 72](img/72.png)
![Imatge 73](img/73.png)  

Reiniciem la màquina, seleccionem “No està a la llista” i iniciem sessió amb un dels usuaris.


![Imatge 74](img/74.png)  
![Imatge 75](img/75.png)
![Imatge 76](img/76.png)  
![Imatge 77](img/77.png)  
![Imatge 78](img/78.png)


Un cop dins, comprovem amb la comanda `id` que tot s’ha creat correctament.

![Imatge 79](img/79.png)

Repetim el procés amb l’altre usuari.

![Imatge 79](img/80.png)




