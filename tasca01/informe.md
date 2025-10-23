
2n \- GM Sistemes microinformàtics i xarxes B Seguretat informàtica (B) \- (Classe) \- 25-26

# **Informe tècnic — Avaluació i justificació de l’ús d’un gestor de contrasenyes** 

## **Introducció i Justificació** 

Les contrasenyes febles o reutilitzades representen un **risc crític per a la seguretat de qualsevol empresa**. Quan un usuari utilitza contrasenyes curtes, previsibles o repetides entre diferents serveis, obre la porta a diversos tipus d’atacs:

* **Atac de diccionari o força bruta:** els atacants proven combinacions comunes o paraules habituals fins a endevinar la contrasenya.  
* **Moviment lateral i escalada de privilegis:** un cop dins, poden aprofitar altres comptes o sistemes amb contrasenyes similars.

Aquestes pràctiques han estat una de les causes més freqüents de fuites de dades i compromisos de comptes corporatius.

Per evitar-ho, **un gestor de contrasenyes** és una eina essencial.  
 Permet:

* **Generar contrasenyes úniques i complexes** de manera automàtica.  
* **Emmagatzemar-les de forma xifrada i segura**, sense que l’usuari hagi de memoritzar-les.  
* **Sincronitzar-les entre dispositius** de manera segura, facilitant el seu ús quotidià.  
* **Evitar la reutilització i reduir errors humans**, garantint credencials fortes a tots els comptes.

En conjunt, l’ús d’un gestor de contrasenyes redueix dràsticament el risc d’intrusió i millora la higiene de seguretat digital de l’organització.

## **Comparativa tècnica detallada: Bitwarden vs KeePassXC** 

| Àrea | Bitwarden (Online / Núvol o self-host) | KeePassXC (Offline / KDBX) |
| :---- | :---- | :---- |
| **Model d’emmagatzematge** | Cofre xifrat emmagatzemat en servidor (servici cloud o instància self-host). | Fitxer local **KDBX** (v4 recomanada) emmagatzemat en disc o en repositori controlat. |
| **Xifratge i KDF** | Xifratge client-side (E2EE). AES-256 per dades; KDF modern (Argon2 o PBKDF2 segons configuració), iteracions ajustables. | KDBX v4: AES-256 o ChaCha20 \+ **Argon2id** com a KDF; xifratge local del fitxer. |
| **Sincronització multi-dispositiu** | Nativa i automàtica entre apps (desktop, mòbil, extensions). Funciona instantàniament amb el núvol; self-host també permet sync. | No nativa: cal sincronitzar el fitxer KDBX via Nextcloud, OneDrive, SMB, rsync, Git, etc.; possible conflictes de fitxer. |
| **Accés i usabilitat** | Alt: extensions de navegador, autofill, apps mòbils, CLI i API. Bona adopció per usuaris tècnics i no tècnics. | Més tècnic: client d’escriptori (cross-platform), keepassxc-cli; autofill i integracions existents però menys polides. |
| **Compartició i col·laboració** | Suport per a «organizations/collections» (compartició granural, revocació, rols). | Compartició mitjançant còpia del fitxer o exportacions; no hi ha revocació granular nativa. |
| **Gestió empresarial** | Consola d’administració, SSO (SAML/OIDC), SCIM provisioning, logs d’auditoria, polítiques centrals (Enterprise/Teams). | No hi ha consola central nativa; administració via processos externs (scripts, repos controlats). |
| **Autenticació multifactor (2FA/FIDO2)** | Suport ferm per 2FA (TOTP, FIDO2/WebAuthn, U2F) i opcions d’aprovació. | Suport per 2FA a nivell d’endpoint (TOTP integrat), però no hi ha un servici central per forçar FIDO2; s’ha d’implementar proteccions d’endpoint. |
| **Portabilitat i recuperació** | Exportacions CSV/JSON i mecanismes de recuperació; integracions API per backup. | Fitxer KDBX és altament portable i interoperable entre implementacions KeePass; fàcil restauració local. |
| **Open source / Llicència** | Bitwarden és open-core; codi client i server parcialment open source; models comercials per funcions empresarials. | KeePassXC és completament open source (FOSS). Sense cost de llicència. |
| **Cost / Model** | Freemium per a usuaris individuals; plans Teams/Enterprise de pagament; self-host redueix subscripcions però té cost operatiu. | Gratuit; cost operatiu per sincronització/backups/gestió d’infraestructura si cal. |
| **Riscos operatius** | Concentració de cofres si s’usa cloud públic (però E2EE mitiga); dependència del servei per a sync. | Risc de corrupció o pèrdua del fitxer si no hi ha backups; més difícil d’escalar per a equips grans. |
| **Integracions DevOps / CLI** | API, CLI i SDKs disponibles; integració fàcil amb fluxos CI/CD i secrets automation. | keepassxc-cli permet automatitzar certes tasques; integracions més limitades i sovint caseres. |
| **Cas d’ús recomanat** | Equip tècnic que necessita sincronització, compartició segura, auditories i integració SSO/SCIM. | Usuari o rol que requereix control local total del fitxer (secrets molt sensibles, entorns air-gapped). |

## **Avantatges i Inconvenients** 

### **Model Online – Bitwarden (núvol / self-host)** 

**Avantatges:**

* **Seguretat:**  
  * Xifratge end-to-end (E2EE): ni el servidor ni l’administrador poden veure les contrasenyes.  
  * Suport natiu de **2FA** i integració amb **FIDO2** o aplicacions TOTP.  
  * Possibilitat de **self-hosting**, mantenint el control total de les dades.

* **Usabilitat:**  
  * Sincronització automàtica entre dispositius (ordinador, mòbil, navegador).  
  * Interfície intuïtiva i integració amb navegadors i aplicacions.  
  * Compartició fàcil i segura de credencials entre membres d’un equip.

* **Continuïtat del negoci:**  
  * Gestió centralitzada, auditories i polítiques corporatives.  
  * Escalable i adequat per a equips grans i treball remot.  
  * Backups automàtics i mecanismes de recuperació ràpida.

**Inconvenients:**

* Dependència d’un **servidor** (núvol o intern): una caiguda o error pot afectar temporalment l’accés.  
* Pot tenir **cost econòmic** (subscripció o manteniment del servidor).  
* En mode cloud públic, tot i el xifratge, hi ha una **mínima exposició de confiança** en el proveïdor.

### **Model Offline – KeePassXC (fitxer local KDBX)**

**Avantatges:**

* **Seguretat:**  
  * Control total sobre l’arxiu i la seva ubicació (no passa per cap servidor).  
  * Xifratge robust amb **AES-256 \+ Argon2id**.  
  * Possibilitat d’afegir **keyfile** per doble autenticació local.

* **Usabilitat:**  
  * Senzill per a ús individual o en entorns sense connexió a Internet.  
  * Portable i compatible amb múltiples sistemes (Windows, macOS, Linux).

* **Continuïtat del negoci:**  
  * No depèn de serveis externs; operatiu fins i tot en entorns aïllats o amb restriccions de xarxa.  
  * Open source i sense cost de llicència.

**Inconvenients:**

* **Risc de pèrdua** del fitxer si no es fan còpies de seguretat adequades.  
* **Sincronització manual** o a través de serveis de tercers (pot generar conflictes).  
* **Compartició d’equip limitada** i sense control centralitzat ni auditories.  
* Menor facilitat d’ús per a personal no tècnic.

## **Recomanació** 

Després d’analitzar les dues opcions, **es recomana implantar *Bitwarden*** com a gestor de contrasenyes corporatiu per al personal tècnic de l’empresa.

### **Justificació de la decisió**

* **Equilibri entre seguretat i usabilitat:** Bitwarden ofereix **xifratge end-to-end**, suport de **2FA/FIDO2** i una interfície fàcil d’utilitzar. Això garanteix un alt nivell de protecció sense dificultar el treball diari.  
* **Sincronització i treball en equip:** permet accedir a les credencials des de qualsevol dispositiu (ordinador, mòbil o navegador) i facilita la **compartició segura** entre membres d’un projecte.  
* **Control i gestió centralitzada:** la versió d’empresa inclou **polítiques corporatives, auditories, integració amb SSO** i possibilitat de desplegament **self-host** per mantenir el control sobre les dades.  
* **Continuïtat i escalabilitat:** és una solució fàcil d’integrar, amb mecanismes de **backup, recuperació i supervisió**, adaptada al creixement de l’organització.

**Conclusió:**  
Bitwarden és la millor opció global per a la companyia: combina **seguretat robusta, facilitat d’ús i control corporatiu**, contribuint a evitar incidents com el que ha motivat aquesta mesura i a reforçar la cultura de seguretat dins l’organització.
