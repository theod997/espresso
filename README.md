# Espresso 1:2

Petite application web (PWA) pour noter ses shots d'espresso (Gaggia Classic Pro + Kingrinder K6) et recevoir des conseils pour viser un ratio **1:2 en 25–30 s**.

Tout est enregistré **uniquement sur le téléphone** (stockage local du navigateur) : pas de compte, pas de serveur. Au premier lancement, l'app importe automatiquement les 7 shots d'avant l'app (une seule fois).

Fichiers : `index.html` (toute l'app), `manifest.json`, `service-worker.js`, `icon-192.png`, `icon-512.png`. Il n'y a rien à compiler.

---

## 1. Activer GitHub Pages

1. Sur GitHub, ouvre le dépôt **theod997/espresso** → onglet **Settings** → menu **Pages**.
2. Dans **Source**, choisis **Deploy from a branch**.
3. Dans **Branch**, choisis **main** et le dossier **/ (root)**, puis **Save**.
4. Attends 1 à 2 minutes : l'app est en ligne sur **https://theod997.github.io/espresso/**.

> Les fichiers doivent être sur la branche `main`. S'ils sont sur une autre branche, fusionne d'abord la *pull request*.

---

## 2. Installer l'app sur Android (Pixel 8)

1. Ouvre **https://theod997.github.io/espresso/** dans **Chrome**.
2. Menu **⋮** (en haut à droite) → **Ajouter à l'écran d'accueil** → **Installer**.
3. L'icône tasse apparaît sur l'écran d'accueil ; l'app s'ouvre en plein écran et fonctionne sans réseau.

---

## 3. Sauvegarder ses données

Les shots vivent dans Chrome, sur le téléphone. Ils sont perdus si tu **désinstalles l'app**, **effaces les données de Chrome** ou changes de téléphone.

👉 De temps en temps, va dans **Historique → Exporter en CSV** et garde le fichier (Drive, mail…). Il s'ouvre dans Google Sheets ou Excel.

---

## Mettre à jour l'app

Modifie les fichiers sur GitHub (branche `main`). Si le téléphone affiche encore l'ancienne version, ferme puis rouvre l'app (deux fois au besoin). Pour forcer la mise à jour, augmente le numéro de `espresso-v2` dans `service-worker.js`. Tes shots ne sont pas touchés par une mise à jour.
