# Rando-fds-orga
Dossier contenant le fichier public html mais pas les données 
https://rando-pelu-fds.github.io/Rando-fds-orga/
# Fil des Saisons - Randos

Carnet de randonnées partagé pour un groupe : proposer des randos, s'inscrire, discuter, consulter le calendrier et les traces GPX, le tout dans **un seul fichier HTML** hébergé gratuitement sur GitHub Pages.

Les données (randos, inscrits, messages) sont stockées dans un fichier `randos.json` du dépôt, lu et écrit directement par l'application via l'API GitHub. Il n'y a pas de serveur.

---

## Sommaire

1. [Contenu du dépôt](#1-contenu-du-dépôt)
2. [Installation initiale](#2-installation-initiale)
3. [Utiliser l'application](#3-utiliser-lapplication)
4. [Mettre à jour le code](#4-mettre-à-jour-le-code)
5. [Sécurité et bonnes pratiques](#5-sécurité-et-bonnes-pratiques)
6. [Limites connues](#6-limites-connues)
7. [Dépannage](#7-dépannage)

---

## 1. Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | L'application complète (HTML + CSS + JavaScript). C'est le seul fichier de code. |
| `randos.json` | Les données du groupe. Créé automatiquement à la première publication. **Ne pas le supprimer.** |
| `README.md` | Ce fichier. |

L'application charge deux bibliothèques/ressources externes : Google Fonts et [Leaflet](https://leafletjs.com/) (cartes), ainsi que les fonds de carte OpenTopoMap, IGN et OpenStreetMap. Une connexion internet est donc nécessaire.

---

## 2. Installation initiale

### 2.1 Créer le dépôt

1. Sur GitHub, créer un dépôt **public** (par exemple `randos-groupe`).
2. Y déposer le fichier `index.html` (le nom doit être exactement `index.html`).

> Le dépôt doit être public pour que tous les participants puissent lire les données sans jeton.

### 2.2 Activer GitHub Pages

1. Dans le dépôt : **Settings → Pages**.
2. *Source* : `Deploy from a branch`.
3. *Branch* : `main`, dossier `/ (root)`, puis **Save**.
4. Après une à deux minutes, le site est disponible à l'adresse :
   `https://<votre-compte>.github.io/<nom-du-depot>/`

### 2.3 Créer un jeton d'accès (pour publier des modifications)

Seules les personnes qui doivent **écrire** dans le fichier de données ont besoin d'un jeton. Sans jeton, l'application fonctionne en **lecture seule** (les inscriptions ne sont alors enregistrées que localement et disparaissent).

1. GitHub → photo de profil → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. *Repository access* : **Only select repositories** → choisir le dépôt des randos.
3. *Permissions → Repository permissions* : **Contents : Read and write**.
4. Choisir une durée d'expiration, puis générer et **copier le jeton** (`github_pat_…`). Il ne sera plus affiché.

### 2.4 Configurer l'application

1. Ouvrir le site, cliquer sur la roue crantée **⚙** (en haut à droite), confirmer le message « réservé aux administrateurs ».
2. Renseigner :
   - **Propriétaire / organisation** : votre compte GitHub
   - **Dépôt** : le nom du dépôt
   - **Branche** : `main`
   - **Chemin du fichier JSON** : `randos.json`
   - **Jeton** : le jeton créé ci-dessus
3. Cliquer sur **Enregistrer les paramètres**. Le voyant en haut passe au vert (« Publié / Synchronisé »).

### 2.5 Partager l'application au groupe

Dans **⚙ → Lien à partager au groupe**, cliquer sur **Générer et copier le lien**, puis l'envoyer au groupe. Ce lien ouvre l'application déjà connectée au bon dépôt.

---

## 3. Utiliser l'application

### Pour tous les participants

- **Calendrier** (affiché par défaut) : navigation de mois en mois. Cliquer sur une rando ouvre sa fiche.
- **Liste** : randos à venir, avec une case pour afficher les randos passées.
- **Statistiques** : nombre de randos, distance et dénivelé cumulés, nombre de participants différents et d'inscriptions, moyennes par rando (distance, dénivelé, participants), randos par mois, organisateurs et participants les plus actifs.
- **Fiche d'une rando** : toutes les infos (date, heures et lieux de RdV et de départ de marche, parcours, distance, dénivelé, durée, difficulté, téléphone de l'organisateur cliquable sur mobile).
  - **Carte et trace GPX** (section repliable) : carte topographique par défaut, avec choix du Plan IGN ou d'OpenStreetMap, et téléchargement du fichier `.gpx` (nom du fichier affiché) et bouton plein écran sur la carte (⛶, retour avec ✕ ou Échap).
  - **Participants** : liste des inscrits (section repliable).
  - **S'inscrire** : prénom, NOM, et lieu de rencontre (point de RdV ou lieu de départ, avec les heures).
  - **Discussion** : messages du groupe (section repliable, avec le nombre de messages).
- **Lien d'inscription** reçu par e-mail : ouvre directement une fenêtre d'inscription à la rando concernée, avec la discussion et un bouton **Calendrier Rando**.

### Pour proposer une rando

- Bouton **+ Proposer une rando**, ou **clic sur un jour vide du calendrier** (la date est préremplie).
- Renseigner titre, date, organisateur et téléphone, difficulté, distance, dénivelé, durée, lieu et heure de RdV, lieu et heure de départ de marche, boucle ou non, description.
- Section **Carte et trace GPX** : importer un fichier `.gpx` (300 Ko maximum), le visualiser, le retirer ou le télécharger.

### Zone organisateur

Sur la fiche d'une rando, le bouton **🔒 Gérer la randonnée (réservé à l'organisateur)** affiche les actions d'administration. Chacune demande une confirmation :

- **Lien d'inscription** : génère un lien direct (contient le jeton si vous en avez configuré un).
- **Générer le texte d'e-mail** : produit un texte mis en forme à partir des infos de la rando, à copier puis coller dans votre messagerie.
- **Modifier** la rando.
- **Dupliquer la rando** : ouvre un formulaire prérempli, sans les participants ni la discussion.
- **Annuler / Rétablir** la rando (avec une raison affichée sur la page principale).
- **Supprimer** définitivement.

> Ce verrouillage est une aide visuelle contre les fausses manipulations, pas une vraie protection : voir [Sécurité](#5-sécurité-et-bonnes-pratiques).

### Paramètres (administrateurs)

Via la roue crantée **⚙** :

- **Dépôt GitHub et jeton.**
- **Lien à partager au groupe.**
- **Valeurs par défaut d'une nouvelle rando** (partagées avec tous, enregistrées dans `randos.json`) : organisateur, téléphone, lieu et heure de RdV, lieu et heure de départ de marche, difficulté, durée. Elles préremplissent la création, mais restent modifiables.
- **Modèle du texte d'e-mail** (partagé, enregistré dans `randos.json`) : éditeur avec gras, italique, souligné, liste, taille, couleur et liens avec texte personnalisé. Le menu « Insérer un champ » ajoute des champs remplacés automatiquement (`{titre}`, `{date}`, `{heure_rdv}`, `{rdv}`, `{heure_depart}`, `{depart}`, `{parcours}`, `{orga}`, `{tel}`, `{km}`, `{deniv}`, `{duree}`, `{difficulte}`, `{description}`, `{participants}`, `{lien_inscription}`).
  Pour afficher « Inscription » au lieu d'une longue adresse, utiliser le bouton **🔗 Lien**, saisir `{lien_inscription}` comme adresse, puis « Inscription » comme texte affiché.
- **Données** : actualiser depuis GitHub, exporter et importer un fichier JSON (sauvegarde).

Cliquer sur **Enregistrer les paramètres** pour valider (dépôt, valeurs par défaut et modèle d'e-mail).

---

## 4. Mettre à jour le code

Quand vous recevez une nouvelle version de `index.html`, **il suffit de remplacer l'ancien fichier**. Les données du groupe ne sont pas touchées, car elles sont dans `randos.json`.

### Ce qui est conservé

- Toutes les randos, inscriptions et messages (`randos.json`).
- Les paramètres de chaque navigateur (dépôt et jeton), tant que l'adresse du site ne change pas.
- Les valeurs par défaut et le modèle d'e-mail, partagés dans `randos.json`.

### Méthode A : depuis le site GitHub (la plus simple)

1. Ouvrir le dépôt, cliquer sur le fichier `index.html`.
2. Cliquer sur le **crayon** (Edit this file), ou sur **Add file → Upload files** pour envoyer le nouveau fichier.
   - Avec le crayon : tout sélectionner (`Ctrl+A`), coller le contenu du nouveau fichier.
   - Avec l'envoi : glisser le nouveau `index.html` (même nom) pour remplacer l'ancien.
3. Cliquer sur **Commit changes**, avec un message du type « Mise à jour de l'application ».
4. Attendre une à deux minutes (onglet **Actions** du dépôt : le déploiement Pages doit passer au vert).

### Méthode B : avec Git en ligne de commande

```bash
git clone https://github.com/<votre-compte>/<nom-du-depot>.git   # une seule fois
cd <nom-du-depot>
git pull                                  # récupérer l'état actuel
# remplacer index.html par la nouvelle version, puis :
git add index.html
git commit -m "Mise à jour de l'application"
git push
```

> `git pull` avant de modifier est important : l'application écrit elle-même dans `randos.json`, donc le dépôt évolue entre deux de vos mises à jour. Ne touchez pas à `randos.json` pendant une mise à jour de code.

### Vérifier que la mise à jour est bien en ligne

1. Ouvrir le site et forcer le rechargement : `Ctrl+Shift+R` (Windows/Linux), `Cmd+Shift+R` (Mac). Sur mobile : vider le cache du navigateur ou ouvrir le site en navigation privée.
2. Vérifier le **numéro de version** en bas de page (par exemple `v2026.11.14-c`). Il change à chaque nouvelle version.

### En cas de problème après une mise à jour

- Dans le dépôt, ouvrir l'historique de `index.html` (**History**), repérer la version précédente, puis **⋯ → View file** et recopier son contenu, ou utiliser `git revert <commit>`.
- Les données ne sont pas affectées : elles sont restaurables via l'historique de `randos.json` ou via un export JSON fait depuis **⚙ → Données**.

---

## 5. Sécurité et bonnes pratiques

- **Le dépôt est public.** Tout ce qui est saisi (noms, prénoms, numéros de téléphone des organisateurs, messages) est lisible par n'importe qui qui connaît ou trouve l'adresse du dépôt, y compris dans l'historique GitHub. Ne saisissez rien de sensible.
- **Le jeton donne un accès en écriture** au dépôt. Il est stocké en clair dans le navigateur de la personne qui l'a saisi. Utilisez toujours un jeton *fine-grained* limité à ce seul dépôt et à la permission *Contents : Read and write*, avec une date d'expiration.
- **Le lien d'inscription généré par l'organisateur (et celui inséré dans l'e-mail) contient le jeton.** Quiconque reçoit ce lien peut écrire dans `randos.json`. C'est ce qui permet aux participants de s'inscrire sans compte GitHub. À réserver à un groupe de confiance. Si le jeton fuit, le **révoquer** sur GitHub (Settings → Developer settings) et en créer un nouveau, puis régénérer les liens.
- **Il n'y a pas d'authentification réelle** : le bouton « Gérer la randonnée » et les confirmations évitent les erreurs, mais ne bloquent pas quelqu'un qui détient le jeton.
- **Faites des sauvegardes** : **⚙ → Données → Exporter en JSON** de temps en temps.

---

## 6. Limites connues

- **Écritures simultanées** : si deux personnes s'inscrivent exactement au même moment, la seconde publication peut échouer (message d'erreur dans le voyant d'état). Il suffit de réessayer.
- **Quota GitHub** : sans jeton, l'API est limitée à 60 requêtes par heure et par adresse IP. L'application se rafraîchit toutes les minutes, ce qui peut atteindre cette limite. Avec un jeton, la limite est bien plus haute.
- **Taille des données** : les traces GPX sont stockées dans `randos.json` (300 Ko maximum par trace). Un fichier JSON dépassant environ 1 Mo ne peut plus être lu par l'application. Évitez d'importer beaucoup de traces lourdes et supprimez celles des randos anciennes si besoin.
- **Paramètres propres à chaque navigateur** : le dépôt configuré et le jeton ne sont pas partagés entre appareils. Les valeurs par défaut et le modèle d'e-mail, eux, sont partagés (stockés dans `randos.json`) ; les enregistrer demande un jeton.
- **Inscription sans jeton** : un participant qui ouvre le site sans jeton (ni lien contenant le jeton) ne peut pas enregistrer son inscription sur GitHub.

---

## 7. Dépannage

| Symptôme | Cause probable et solution |
|---|---|
| Voyant rouge « Impossible de joindre GitHub » | Dépôt, branche ou nom de fichier mal saisis, ou dépôt privé, ou quota atteint. Vérifier **⚙**. |
| « Enregistré localement seulement » | Aucun jeton configuré : l'inscription n'est pas publiée. Utiliser le lien d'inscription fourni par l'organisateur. |
| Erreur 401 ou 403 à la publication | Jeton expiré, révoqué, ou sans la permission *Contents : Read and write* sur ce dépôt. |
| Erreur 409 | Publication simultanée : réessayer. |
| Une inscription disparaît après quelques secondes | La publication a échoué, et l'actualisation automatique a remis l'état de GitHub. Vérifier le voyant d'état et le jeton. |
| La carte reste grise ou vide | Connexion internet ou bloqueur de contenu qui bloque Leaflet ou les tuiles. Essayer un autre fond de carte via le sélecteur en haut à droite de la carte. |
| Le site n'affiche pas la nouvelle version | Cache du navigateur : rechargement forcé (`Ctrl+Shift+R`), puis vérifier le numéro de version en bas de page. |
| Page blanche ou erreur 404 sur le site | GitHub Pages non activé, ou fichier pas nommé exactement `index.html`. Vérifier **Settings → Pages**. |
