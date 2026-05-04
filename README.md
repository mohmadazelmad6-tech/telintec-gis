# 🛰️ Telintec NMS - Gestion d'Infrastructure Khénifra

Une plateforme moderne de gestion d'infrastructure réseau (NMS) permettant la visualisation géospatiale, l'importation de fichiers KMZ et la gestion fine de la capacité des ports.

![Status](https://img.shields.io/badge/Status-Ready_for_Deployment-success?style=for-the-badge)
![Tech](https://img.shields.io/badge/Stack-Laravel_9_%2B_React_18-blue?style=for-the-badge)
![Cloud](https://img.shields.io/badge/Deploy-Railway-6e17e6?style=for-the-badge&logo=railway)

---

## 🚀 Fonctionnalités Clés

- **🗺️ Cartographie Interactive** : Visualisation en temps réel des équipements (NRO, SR, PCO) via Leaflet.
- **📥 Importation KMZ Intelligente** : Parsing automatique des fichiers KML/KMZ avec gestion des zones et correction des typos de parenté (ex: `0` vs `O`).
- **📊 Dashboard de Planification** : Statistiques détaillées sur l'occupation des ports et l'état du réseau.
- **🔌 Gestion des Ports** : Suivi précis des abonnés et de la saturation des équipements.

---

## 🚢 Guide de Déploiement Railway (Exact)

Pour obtenir le même résultat qu'en local, suivez ces étapes précises :

### 1️⃣ Étape 1 : Créer la Base de Données
1. Sur [Railway](https://railway.app/), cliquez sur **+ New** -> **Database** -> **Add MySQL**.
2. Une fois prête, ne touchez à rien, les variables seront liées automatiquement.

### 2️⃣ Étape 2 : Déployer le Backend (API)
1. **+ New** -> **GitHub Repo** -> Sélectionnez votre dépôt.
2. Cliquez sur le service et allez dans **Settings** :
   - **Root Directory** : `backend`
   - **Start Command** : `php artisan serve --host=0.0.0.0 --port=$PORT`
3. Allez dans **Variables** et ajoutez ces valeurs exactes :
   - `APP_KEY` : *(Votre clé de .env local)*
   - `JWT_SECRET` : *(Votre secret JWT de .env local)*
   - `DB_CONNECTION` : `mysql`
   - `DB_HOST` : `${{MySQL.MYSQLHOST}}`
   - `DB_PORT` : `${{MySQL.MYSQLPORT}}`
   - `DB_DATABASE` : `${{MySQL.MYSQLDATABASE}}`
   - `DB_USERNAME` : `${{MySQL.MYSQLUSER}}`
   - `DB_PASSWORD` : `${{MySQL.MYSQLPASSWORD}}`
4. Dans **Settings** -> **Public Networking**, cliquez sur **Generate Domain** et copiez-le (ex: `https://backend-production.up.railway.app`).

### 3️⃣ Étape 3 : Déployer le Frontend (Client)
1. **+ New** -> **GitHub Repo** -> Sélectionnez encore le même dépôt.
2. Cliquez sur le service et allez dans **Settings** :
   - **Root Directory** : `frontend`
   - **Build Command** : `npm run build`
   - **Install Command** : `npm install`
3. Allez dans **Variables** et ajoutez :
   - `VITE_API_URL` : *(Collez l'URL générée à l'étape 2 en ajoutant /api à la fin)*.  
     Exemple : `https://backend-production.up.railway.app/api`
4. Dans **Settings** -> **Public Networking**, générez un domaine. **C'est votre lien final !**

### 4️⃣ Étape 4 : Initialiser la Database Online
1. Allez dans le service **Backend** sur Railway.
2. Cliquez sur l'onglet **View Logs** puis sur le bouton **Terminal**.
3. Tapez la commande suivante pour créer les tables et les comptes :
   ```bash
   php setup_db.php
   ```

---

## 🛠️ Stack Technique

- **Backend** : Laravel 9 (PHP 8.1), JWT Auth, MySQL.
- **Frontend** : React 18, Vite, React-Leaflet, Lucide Icons.
- **Optimisation** : Eager loading des relations et calculs de ports côté serveur pour une vitesse maximale.

---

## 👤 Identifiants par défaut
- **Admin** : `admin@test.com` / `password`
- **Technicien** : `technicien@test.com` / `password`

---

## 📝 Licence
Propriété de **Telintec S.A.** - Projet de gestion d'infrastructure Khénifra.
