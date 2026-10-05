# Sëtal AAAS — version alpha

Plateforme de vidange et de curage à la demande de l'**Association des Acteurs de l'Assainissement du Sénégal**,
sur le modèle Yango / Uber. Toutes les données de cette alpha sont **fictives**.

## Ce que fait l'alpha

| Espace | Contenu |
|---|---|
| **Client** | Vidange, curage ou débouchage ; maintenant ou programmé. Adresse précise, repère, téléphone, contact sur place. Recherche des camions connectés, attribution au chauffeur qui a le plus de points, fiche chauffeur (photo, téléphone, camion, plaque), prix estimé puis ajusté par le chauffeur (±15 %), validation, paiement, suivi GPS, dépotage en STBV, notification finale, enquête, reçu. |
| **Vidangeur** | Réception des demandes, ajustement du prix avec motif, navigation, code client, photos et anomalies, scan de la station, points. Formules Basique (25 000 F/mois) et Premium (10 %). |
| **Chef de garage** | Mandat digital de 5 %, saisie de commandes pour les clients sans smartphone, camions rattachés. |
| **Pilotage AAAS** | Demandes et classement des chauffeurs en direct, enrôlement, effacement des données de test, flotte, cotisations, formations. |
| **Modèle et lancement** | Grille tarifaire, offres, navigation, points de vigilance, feuille de route. |

Stations de dépotage : STBV de Cambérène, Pikine, Rufisque et Tivaouane Peulh (STEP de l'ONAS), choisies selon le quartier.

## Trois façons de l'ouvrir

1. **Sur un seul téléphone (simulation)** — dès la publication GitHub, sans rien configurer.
   Les chauffeurs sont simulés : ils répondent tout seuls, le camion roule sur la carte.
2. **Sur plusieurs téléphones (test réel)** — un téléphone « client », un ou plusieurs téléphones « chauffeur »,
   un ordinateur « bureau AAAS ». Il faut brancher la base Firebase du projet `assainissement-pro` (étape 2 ci-dessous).
3. **Lien claude.ai** — même application, déjà reliée à une base partagée, sans configuration.

## Étape 1 — Publier sur GitHub et installer sur le téléphone

1. Double-cliquer sur `publier-sur-github.command` (macOS). Le script crée le dépôt public `setal-aaas`,
   pousse le code et active GitHub Pages (outil `gh` requis : `brew install gh`).
2. Lien : **https://magnfall1992-design.github.io/setal-aaas/**
3. Sur le téléphone :
   - **Android (Chrome)** : ouvrir le lien › menu ⋮ › *Ajouter à l'écran d'accueil* / *Installer l'application*.
   - **iPhone (Safari)** : ouvrir le lien › bouton Partager › *Sur l'écran d'accueil*.
   L'icône AAAS apparaît comme une application.

## Étape 2 — Brancher la base Firebase (test sur plusieurs téléphones)

1. https://console.firebase.google.com › projet **assainissement-pro**.
2. *Build › Firestore Database* : créer la base si elle n'existe pas (emplacement `eur3` ou le plus proche).
3. Onglet *Règles* : coller le contenu de `firestore.rules`, puis *Publier*.
   Ces règles ouvrent seulement les collections `demandes` et `chauffeurs`, jusqu'au 31/12/2026. Elles servent au test.
4. *Paramètres du projet* (roue dentée) › *Vos applications* › icône Web `</>` › nom « Sëtal » ›
   copier l'objet `firebaseConfig`.
5. Coller les valeurs dans `firebase-config.js` (apiKey, messagingSenderId, appId…), enregistrer,
   puis relancer `publier-sur-github.command`.
6. En haut de l'application, le badge passe à **« Test réel · base partagée (Firebase) »**.
7. Onglet *Pilotage AAAS* › *Charger 6 chauffeurs de test* (une seule fois).

Les fonctions Cloud déjà présentes dans `assainissement-firebase/functions` utilisent les collections `missions`,
`camions`, `depotages`. L'alpha écrit dans `demandes` et `chauffeurs` : pas de conflit. Le rapprochement des deux
modèles est l'étape suivante.

## Structure

```
index.html              application complète (un seul fichier)
firebase-config.js      configuration Firebase (à compléter pour le test à plusieurs)
firestore.rules         règles Firestore de test
manifest.webmanifest    installation sur l'écran d'accueil
sw.js                   ouverture même avec un réseau faible
icon-192.png, icon-512.png   icônes AAAS
GUIDE_DE_TEST.md        scénarios à faire jouer aux testeurs
```
