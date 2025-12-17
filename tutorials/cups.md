<div align="center">

<img src="/img/logo_ubuntu.png" alt="Logo Ubuntu" width="100"/>

# 🐧 Ubuntu Tutorials  
### Impressores en xarxa: CUPS

Tutorial per aprendre a **instal·lar i configurar els servei CUPS (Common Unix Printing System)**, aplicant totes les configuracions necessaries.

---

</div>

# 🔄 Compartició de impressores en Linux: CUPS

Tutorial per aprendre a **instal·lar i configurar els servei CUPS (Common Unix Printing System)**, aplicant totes les configuracions necessaries.

---

### 🧩 Objectiu

- Configurar un servidor de impressió de de Ubuntu Server. 
- Configuració adequadament CUPS  
- Instal·lar una impressora virtual PDF al servidor.  
- Accés des del client Web.

---

### 1️⃣ Instal·lació del servei

La primera activitat serà instal·lar el CUPS per gestionar les impressores, cues.

```bash
sudo apt install cups
```

### 2️⃣Instal·lació impressora virtual PDF

Instal·lació de la impressora virtual PDF

```bash
sudo apt install cups-pdf
```
### 3️⃣ Configuració CUPS

Editarem l'arxiu de configuració /etc/cups/cupsd.conf amb el nano

```bash
sudo nano /etc/cups/cupsd.conf
```

Afegim la següent configuració

```bash
# Only listen for connections from the local machine.
Port 631
Listen /run/cups/cups.sock
# Show shared printers on the local network.
Browsing On
```

```bash
# Restrict access to the server...
<Location />
  Order allow,deny
  Allow @LOCAL
</Location>

# Restrict access to the admin pages...
<Location /admin>
  AuthType Default
  Require user @SYSTEM
  Order allow,deny
  Allow @LOCAL
</Location>
```

### 4️⃣ Iniciar el servei i verificar el seu funcionament

```bash
sudo systemctl restart cups && systemctl status cups
```

### 5️⃣ Comprovacions

Administració web del CUPS, introduir usuari i contrasenya del nostre usuari Ubuntu

```bash
https://192.168.56.101:631
```
Anar al menú **Administració** i fer clic en el botó d'**afegir impressora**

### 6️⃣ Error al voler afegir la nova impressora

En intentar afegir la nova impressora, es produirà un error. Per solucionar-ho, cal afegir el nostre usuari al grup lpadmin. Això permet que l’usuari pugui administrar les impressores (afegir-ne, eliminar-ne o configurar-les) sense necessitat de ser administrador del sistema.

```bash
sudo usermod -aG lpadmin usuari
```

### 7️⃣Afegir impressora
- Ara dins les "Local Printers" afegirem: (*) CUPS-PDF (Virtual PDF Printer)
- Marcar l'opció [v] Compartir aquesta impressora i fer següent
- Escollir model: Generic CUPS-PDF Printer (no options) (en)


### 8️⃣ Instal·lar la impressora en el nostre client
- Anar al nostres Ubuntu Desktop / Zorin a la configuració de les impressores
- Fem afegir nova impressora
- Mirem de fer algunes proves d'impressió i verifiquem que surten els treballs en la cua
- Per ultim mostrar el contigut de la carpeta ~/PDF (tree / ls -al) en el nostre servidor.

