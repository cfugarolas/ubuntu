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

### 4️⃣ Iniciar el servei

```bash
sudo systemctl restart cups && systemctl status cups
```

### 5️⃣ Comprovacions

Gestió client web CUPS, introduir usuari i contrasenya del nostre usuari Ubuntu

```bash
https://192.168.56.101:631
```

### 6️⃣ Error al accedir des del client

Primer de tot haurem de instal·lar el client nfs al nostre client Ubunto Desktop / Zorin

```bash
sudo usermod -aG lpadmin usuari
```

### 7️⃣



### 8️⃣



### 9️⃣ 
