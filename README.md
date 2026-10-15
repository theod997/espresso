# Espresso 1:2

Petite application web (PWA) pour noter ses shots d'espresso (Gaggia Classic Pro + Kingrinder K6) et recevoir des conseils pour viser un ratio **1:2 en 25–30 s**. Les données sont enregistrées dans la feuille Google Sheets « Espresso Shots ».

Fichiers : `index.html` (toute l'app), `manifest.json`, `service-worker.js`, `icon-192.png`, `icon-512.png`. Il n'y a rien à compiler.

---

## 1. Activer GitHub Pages

1. Sur GitHub, ouvre le dépôt **theod997/espresso** → onglet **Settings** → menu **Pages**.
2. Dans **Source**, choisis **Deploy from a branch**.
3. Dans **Branch**, choisis **main** et le dossier **/ (root)**, puis **Save**.
4. Attends 1 à 2 minutes : l'app est en ligne sur **https://theod997.github.io/espresso/**.

> Les fichiers doivent être sur la branche `main`. S'ils sont sur une autre branche, fusionne d'abord la *pull request*.

---

## 2. Créer CLIENT_ID et API_KEY (Google Cloud Console)

Tout se fait sur <https://console.cloud.google.com>, connecté avec **theophile.delepouve00@gmail.com**.

### a) Créer un projet
1. En haut de la page, clique sur le sélecteur de projet → **Nouveau projet**.
2. Nom : `Espresso` → **Créer**, puis sélectionne ce projet.

### b) Activer les API
Menu ☰ → **API et services** → **Bibliothèque**. Recherche et clique sur **Activer** pour chacune :
- **Google Sheets API**
- **Google Drive API**
- **Google Picker API**

### c) Écran de consentement (mode test)
Menu ☰ → **API et services** → **Écran de consentement OAuth** (ou **Google Auth Platform**).
1. **Commencer** / **Configurer** : nom de l'application `Espresso 1:2`, e-mail d'assistance = ton adresse.
2. Type d'utilisateurs / Audience : **Externe**.
3. Coordonnées du développeur : ton adresse → termine l'assistant.
4. Dans **Audience** : laisse le statut sur **En test** et, sous **Utilisateurs test**, clique **Add users** et ajoute **theophile.delepouve00@gmail.com**.
5. Dans **Accès aux données** (Data access) : **Ajouter ou supprimer des champs d'application** → coche `.../auth/drive.file` → **Mettre à jour** → **Enregistrer**.

### d) Créer le CLIENT_ID
Menu ☰ → **API et services** → **Identifiants** (ou **Google Auth Platform → Clients**).
1. **Créer des identifiants** → **ID client OAuth**.
2. Type d'application : **Application Web**. Nom : `Espresso web`.
3. **Origines JavaScript autorisées** → **Ajouter un URI** : `https://theod997.github.io` (sans `/espresso` ni `/` final).
4. **Créer**. Copie l'**ID client** (il ressemble à `123456789012-xxxx.apps.googleusercontent.com`).

### e) Créer l'API_KEY
1. Toujours dans **Identifiants** → **Créer des identifiants** → **Clé API**. Copie la clé (`AIzaSy...`).
2. Clique sur la clé pour la **restreindre** (conseillé, car elle est visible dans le code) :
   - Restrictions d'application : **Sites Web** → ajoute `https://theod997.github.io/*`.
   - Restrictions d'API : **Restreindre la clé** → coche **Google Picker API**.
   - **Enregistrer**.

### f) Mettre les deux valeurs dans le code
1. Sur GitHub, ouvre `index.html` → icône crayon ✏️ (**Edit this file**).
2. Cherche (en haut du script) :
   ```js
   const CLIENT_ID = '';
   const API_KEY   = '';
   ```
   et colle tes valeurs entre les apostrophes.
3. **Commit changes…** → **Commit changes**. Au bout d'une minute, GitHub Pages est à jour.

> Les modifications de la console Google peuvent mettre quelques minutes à s'appliquer.

---

## 3. Premier lancement

1. Ouvre **https://theod997.github.io/espresso/** dans Chrome sur ton Pixel.
2. Touche **Se connecter à Google** → choisis ton compte. Google affiche « Google n'a pas validé cette application » (normal en mode test) → **Continuer**.
3. Dans la fenêtre de choix, sélectionne la feuille **Espresso Shots** (dossier *Claude*).
4. L'app crée l'onglet **cafes** s'il n'existe pas, puis charge tes shots.

Ensuite :
- Chaque shot enregistré ajoute une ligne dans la feuille. Sans réseau, il reste en attente (⏳) et part tout seul au retour du réseau.
- La connexion Google dure environ 1 h ; ensuite l'app la redemande d'un simple tap (pastille en haut, ou au prochain enregistrement).
- Le menu **⋯** permet de synchroniser, de changer de feuille ou de se déconnecter.

---

## 4. Installer l'app sur Android (Pixel 8)

1. Ouvre **https://theod997.github.io/espresso/** dans **Chrome**.
2. Menu **⋮** (en haut à droite) → **Ajouter à l'écran d'accueil** → **Installer**.
3. L'icône tasse apparaît sur l'écran d'accueil ; l'app s'ouvre en plein écran, comme une vraie application.

---

## Mettre à jour l'app

Modifie les fichiers sur GitHub (branche `main`). Si le téléphone affiche encore l'ancienne version, ferme puis rouvre l'app (deux fois au besoin). Pour forcer la mise à jour, change `espresso-v1` en `espresso-v2` dans `service-worker.js`.
