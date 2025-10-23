# 🛑 Alerta de Seguretat: Cibera atac a EverPia

**Alerta!!** EverPia ha estat atacada per ciberdelinqüents.  
La consultora on esteu de becaris ha patit una **fuita d’informació (data breach)**, i informació confidencial sobre un projecte en desenvolupament està ara en mans de delinqüents que amenacen amb publicar-la si no es paga un rescat.

Aquesta situació ha provocat una **gran alarma dins la companyia**, i s’ha creat un **comitè de crisi** per gestionar-la.  
La investigació interna ha revelat que **un dels comptes tècnics va ser compromès** a causa de l'ús d'una **contrasenya feble o reutilitzada**.

---

## 🧩 Directriu de la Direcció Tècnica

Com a resposta a aquesta crisi, la Direcció Tècnica ha emès una nova política de seguretat:

> Tot el personal tècnic ha de començar a utilitzar un **gestor de contrasenyes validat** per garantir l'ús de **credencials úniques i robustes**.

Se us encarrega la tasca de **avaluar les opcions disponibles** i **crear la documentació necessària per a la formació del personal.**

---

## 📘 Fase 1: Anàlisi i Justificació (Document d'Informe)

Heu de redactar un **informe tècnic** que justifiqui la decisió de la Direcció i compari diferents opcions de gestors de contrasenyes.

### Contingut de l’informe

#### 1. Introducció i Justificació
- Explicació de per què les **contrasenyes febles o reutilitzades** són un risc crític per a l'empresa (ex: **atacs de diccionari**, **credential stuffing**, etc.).
- Descripció de la **funció clau d’un gestor de contrasenyes** per mitigar aquests riscos.

#### 2. Comparativa Tècnica
Realitzeu una **taula comparativa detallada** entre:

| Eina | Tipus | Característiques a Analitzar |
|------|-------|------------------------------|
| **Bitwarden** | Online / Núvol | Sincronització, model de seguretat (xifratge end-to-end), accés multi-dispositiu, cost / model freemium |
| **KeePassX / KeePassXC** | Offline / Escriptori | Emmagatzematge local (KDBX), independència del núvol, model open source, portabilitat de l’arxiu |

#### 3. Avantatges i Inconvenients
- Resum dels **pros i contres** de cada model (online vs. offline) des del punt de vista de:
  - **Seguretat**
  - **Usabilitat**
  - **Continuïtat del negoci**

#### 4. Recomanació
Concloeu l’informe **escollint l’eina més adequada** per al personal tècnic i **justifiqueu la vostra elecció.**

📄 El fitxer d’aquesta fase s’ha d’anomenar:  
`informe.md`

---

## 🧰 Fase 2: Guia d’Ús Tècnica (Manual Operatiu)

Utilitzant **l’eina escollida a la Fase 1** (Bitwarden, KeePassX, o similar), creeu una **guia tècnica d’ús** per a l’equip tècnic.  
Aquesta guia ha de ser **clara, visual i basada en captures de pantalla.**

### Contingut obligatori de la guia

1. **Instal·lació i Configuració Inicial**  
   - Descàrrega, instal·lació i creació de la BBDD principal o compte mestre.

2. **Generació de Contrasenyes Segures**  
   - Com utilitzar el generador de contrasenyes (paràmetres, longitud, caràcters especials).

3. **Exemples d’Ús i Emplenament Automàtic**  
   - Com desar una credencial d’un **compte de correu electrònic**.  
   - Com desar una credencial d’una **aplicació o servei web**.  
   - Com fer servir **l’extensió del navegador** per emplenar automàticament les dades.

4. **Gestió de Còpies de Seguretat (Backup)**  
   - Com fer una **còpia de seguretat** de l’arxiu de contrasenyes (`.kdbx` en KeePass o exportació en Bitwarden).  
   - Recomanacions sobre com **emmagatzemar aquesta còpia de forma segura** (clau USB xifrada o emmagatzematge xifrat al núvol).

📄 El fitxer d’aquesta fase s’ha d’anomenar:  
`guia.md`

📂 Les **imatges** de la guia s’han de desar dins d’una carpeta específica:  
`img/` o `pics/`

---

- [Tornar pagina principal](../README.md)
- [Anar a la guia](guia.md)
- [Anar al informe](informe.md)


