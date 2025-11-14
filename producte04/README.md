# P04: Documentació servidor DNS

## Breu descripció
Com a membres de l'equip de sistemes d'EverPia, us heu enfrontat al repte de configurar un servidor de noms com a prova de concepte pel nostre client **Digicore**, però ara mateix el resultat de la vostra feina es troba en una màquina virtual.

L’objectiu és poder publicar aquestes configuracions a **GitHub**, d’aquesta manera assegurem que quan es vulgui replicar la configuració, no caldrà començar des de zero; només caldrà descarregar els arxius dins del servidor Linux triat i reiniciar el servei per tenir el servidor completament operatiu.

---

## Fase 1: Preparació de la Connectivitat i Extracció dels Arxius
Per poder copiar fitxers de la vostra màquina virtual **Ubuntu Server** a la vostra màquina física de treball (host), heu d'assegurar la connectivitat de xarxa.

### Pas 1.1: Configuració de la Interfície Host-Only
1. Afegir la Interfície Virtual: A la configuració de la vostra màquina virtual Ubuntu Server, afegiu una segona interfície de xarxa i assigneu-li el mode **Host-Only**.  
2. Configureu-la i activeu-la.  
3. Comproveu que teniu connectivitat des de la màquina física.

### Pas 1.2: Còpia Segura dels Fitxers Clau amb SCP
Un cop establerta la connectivitat Host-Only, utilitzareu el protocol **SCP (Secure Copy Protocol)**, que és segur i ve inclòs amb el servei **SSH**, per transferir els fitxers de configuració a la vostra màquina física.

Els arxius a copiar seran:

/etc/bind/named.conf.options
/etc/bind/named.conf.local

css
Copiar código

I els arxius de zones creats a la carpeta:

/etc/bind/zones

css
Copiar código

Per copiar els arxius a la màquina física, cal obrir un terminal al PC i executar la comanda **scp**. Exemple:

```bash
scp usuari@ip_maquina_virtual:/etc/bind/named.conf.options .
```

# Fase 2: Integració a GitHub

## Pas 2.1: Crear carpeta i arxiu README.md

1. Creeu la carpeta `producte04` i el seu arxiu `README.md`.
2. Podeu fer-ho directament des de GitHub donant a l’opció **New File** i indicant el nom complet:
producte04/README.md

yaml
Copiar código
3. A l’arxiu `README.md` cal incloure:
- El **títol del producte**.
- Una **explicació del contingut dels arxius pujats**.

---

## Pas 2.2: Pujar arxius

1. Creeu la carpeta `zones` dins del repositori abans de pujar els arxius de les zones.
2. Podeu crear un **arxiu temporal** dins de `zones` anomenat `esborrar` per poder pujar la carpeta inicialment.
3. Un cop pujats els arxius, esborreu aquest arxiu temporal.

---

## Objectius específics de la tasca / Finalitat

- **Usar GitHub** per documentar configuracions de servidors.  
- Valorar els avantatges de poder **replicar configuracions de forma ràpida i segura** (repetibilitat).

- [Tornar pagina principal](../README.md)
- [Anar a la guia](guia.md)
- [Anar a la activitat](activitats.md)

