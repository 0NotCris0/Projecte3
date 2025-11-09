# **T04: Serveis de Directori - LDAP**

Autor: *Christian Bogdanas*

---

## 1. Objecte de l’Encàrrec

Creem una màquina amb **Ubuntu Server**.

![server ubuntu](img/1.png)

En entrar a la màquina, el primer que farem serà executar un `sudo apt update && sudo apt upgrade` per actualitzar els paquets i evitar possibles errors més endavant.

![actualizxar paquets](img/2.png)

A continuació, editem el domini amb la comanda:

```
sudo nano /etc/hosts
```

![editar fitxer](img/3.png)

Configurem el fitxer com s’indica a continuació.

![editem domini](img/4.png)

Comprovem que s’hagi actualitzat correctament:

![comrpovar domini](img/5.png)  
![comrpovar domini](img/6.png)

---

## 2. Requeriments d’Infraestructura Inicial

El pas següent és configurar la màquina virtual.  
Anirem a la configuració de xarxa i posarem el **primer adaptador en NAT** i el **segon en mode només amfitrió (Host-Only)**.

![NAT](img/7.png)  
![Host-only](img/8.png)

Després de configurar el mode Host-Only, editarem la interfície de xarxa amb:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```

![editem fitxer](img/9.png)

Afegirem la interfície `enp0s8` i l’opció `dhcp4: true`.

![configurar interficie](img/10.png)

Desarem els canvis amb:

```
sudo netplan apply
```

![guardar confi](img/11.png)

Finalment, comprovarem amb `ip a` que la configuració s’ha aplicat correctament.

---

## 3. Tasques d'Implementació i Configuració del Servidor LDAP

### 3.1. Instal·lació i Configuració Bàsica d’OpenLDAP

Instal·lem el servidor i les utilitats LDAP amb la comanda:

```
sudo apt install slapd ldap-utils -y
```

![instalar utilitats](img/12.png)

Durant la instal·lació, se’ns demanarà establir una contrasenya per a l’administrador. Seguint el plec de condicions, farem servir **p@ssw0rd**.

![establir contrasenya](img/13.png)

Comprovem que el servei està actiu:

```
systemctl status slapd
```

![Comprovem que el servei està actiu](img/14.png)

Podem visualitzar la configuració amb:

```
sudo slapcat
```

![visualitzar la configuració](img/15.png)

Si el directori no s’ha creat correctament, podem reconfigurar el servei amb:

```
sudo dpkg-reconfigure slapd
```

Crearem dues unitats organitzatives: **users** i **groups**. Per fer-ho, generem un fitxer `OU_users.ldif`.

![Crearem dues unitats organitzative](img/16.png)

Editem el fitxer i afegim les OUs corresponents:

![Editem el fitxe](img/17.png)

Afegim les noves OUs amb:

![Afegim les noves OU](img/18.png)

Comprovem que s’han creat correctament:

![Comprovem que s’han creat correctament](img/19.png)

---

### 3.2. Gestió i Administració amb LAM

Per facilitar l’administració del servidor, farem servir **LDAP Account Manager (LAM)**.  
Primer, instal·lem el paquet necessari:

![nstal·lem el paquet necessari](img/20.png)

Obtenim la IP del servidor amb `ip a` per poder accedir-hi des del navegador:

![Obtenim la IP del servidor ](img/21.png)

Accedim a la pàgina del LAM escrivint a l’adreça del navegador:

```
http://<ip_del_servidor>/lam
```

![Accedim a la pàgina del LAM](img/22.png)

Entrem a **LAM Configuration** → **Edit Server Profiles**.

![Entrem a LAM Configuratio](img/23.png)

La contrasenya per defecte és `lam`.

![ contrasenya](img/24.png)

Configurem l’idioma, el compte d’administrador i altres paràmetres generals.

![Configurem l’idioma, el compte d’administrado](img/25.png)  
![altres paràmetres generals](img/26.png)

Definim els **Domain Names (DN)** per als usuaris i grups amb les seves respectives OUs.

![Definim els Domain Names ](img/27.png)

Guardem els canvis.

![Guardem els canvis](img/28.png)

Ara ja podem iniciar sessió com a administrador (`admin`) amb la contrasenya `p@ssw0rd`.

![Ara ja podem iniciar sessió](img/29.png)

Per crear grups, accedim a **Comptes → Grups**, i creem dos grups: `tech` i `manager`.

![accedim a **Comptes → Grups**](img/30.png)  
![creem dos grups](img/31.png)

Podem veure el missatge de confirmació de creació del grup.

![missatge de confirmaci](img/32.png)

Per crear usuaris, anem a **Comptes → Usuaris** i creem `tech01` i `manager01`.

![crear usuaris](img/33.png)  
![creem tech01 i manager01](img/34.png)

Assignem a cada usuari el seu grup principal i grups addicionals segons correspongui.

![Assignem a cada usuari el seu grup principal](img/35.png)  
![Assignem a cada usuari el seu grup principal](img/36.png)

I li posarem el grup tech en els grups addicionals, el que vam crear.

![grup tech](img/37.png) 

Creem la contrasenya per a l’usuari (`1234`) i la desem.

 
![Creem la contrasenya per a l’usuar](img/38.png)

I guardem.

![guardem](img/39.png)  

Repetim el procés amb `manager01`.


![Repetim el procés](img/40.png)  
![Repetim el procés](img/41.png)  
![Repetim el procés](img/42.png)
![Repetim el procés](img/43.png)

---

## 4. Integració del Client (Ubuntu Desktop)

Comprovarem que el servidor LDAP funciona correctament configurant un client **Zorin OS** amb les següents característiques:

El primer adaptador serà **NAT** i el segon **Host-Only**.

![zorinOS](img/44.png)
![adapatador host-only](img/45.png) 

Configurem la interfície de xarxa:

```
sudo nano /etc/netplan/50-cloud-init.yaml
```
 
![editem fitxer](img/46.png)
![editem fitxer](img/47.png)

Desem amb:

```
sudo netplan apply
```
![guardem](img/48.png)  


Editem el fitxer `/etc/hosts` per configurar el nom del equip perque formi part del mateix domini que el servidor.


![Editem el fitxer](img/49.png)

![posem la confi](img/50.png)

Comprovem que el nom del dispositiu s’ha actualitzat correctament.

![Comprovem](img/51.png) 

Creem una instantània de la màquina per seguretat.

 
![Creem una instantània](img/52.png)

![Creem una instantània](img/53.png)

Verifiquem la resolució DNS amb:

```
dig server.innovatech05.test
```

![Verifiquem la resolució DNS](img/54.png)

Fem una consulta LDAP des del client per comprovar la connectivitat:

```
ldapsearch -x
```
![Fem una consulta LDAP](img/55.png)  


Instal·lem els mòduls necessaris per integrar el client al domini:


![Instal·lem els mòduls](img/56.png)  
![Instal·lem els mòduls](img/57.png)  
![Instal·lem els mòduls](img/58.png)  
![Instal·lem els mòduls](img/59.png)  
![Instal·lem els mòduls](img/60.png)  
![Instal·lem els mòduls](img/61.png)  
![Instal·lem els mòduls](img/62.png)
![Instal·lem els mòduls](img/63.png)  

Editem `nsswitch.conf` per permetre la gestió d’usuaris i grups via LDAP:


![Editem fitxer](img/64.png)
![configuracio](img/65.png)

Modifiquem `common-password` eliminant la línia `use_authok`:

  
![Editem fitxer](img/66.png)
![configuracio](img/67.png)  

Editarem `common-session` i afegirem la línia següent per crear automàticament els perfils d’usuari:

```
session optional pam_mkhomedir.so skel=/etc/skel umask=077
```


![Editem fitxer](img/68.png)
![configuracio](img/69.png)

Reiniciem el servei:

![Reiniciem](img/70.png)

Comprovem que el sistema detecta correctament els usuaris LDAP:

![Comprovem que el sistema detecta correctament els usuaris LDA](img/71.png) 

Per permetre l’inici de sessió gràfica dels usuaris de domini, editem el fitxer corresponent:

 
![editem fitxer](img/72.png)
![configuracio](img/73.png)  

Reiniciem la màquina, seleccionem “No està a la llista” i iniciem sessió amb un dels usuaris.


![iniciem sessió amb un dels usuaris](img/74.png)  
![iniciem sessió amb un dels usuaris](img/75.png)
![iniciem sessió amb un dels usuaris](img/76.png)  
![iniciem sessió amb un dels usuaris](img/77.png)  
![iniciem sessió amb un dels usuaris](img/78.png)


Un cop dins, comprovem amb la comanda `id` que tot s’ha creat correctament.

![ comprovem amb la comanda](img/79.png)

Repetim el procés amb l’altre usuari.

![ comprovem amb la comanda](img/80.png)


- [Tornar al enunciat](README.md)

