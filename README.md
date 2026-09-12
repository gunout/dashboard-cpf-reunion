# 🏝️ Dashboard Cadastre & Immobilier – La Réunion

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?style=for-the-badge&logo=leaflet&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chart.js&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

> **Carte interactive du cadastre et des données immobilières (DVF) pour les 24 communes de La Réunion**

Application web monopage (SPA) permettant de visualiser les **parcelles cadastrales**, les **bâtiments** et les **transactions immobilières** (DVF) sur l'ensemble du territoire réunionnais, avec des indicateurs clés et des graphiques interactifs.

---

## 📋 Table des matières

- [Aperçu](#-aperçu)
- [Fonctionnalités](#-fonctionnalités)
- [Structure des données](#-structure-des-données)
- [Installation](#-installation)
- [Utilisation](#-utilisation)
- [Technologies](#-technologies)
- [Captures d'écran](#-captures-décran)
- [Contribuer](#-contribuer)
- [Licence](#-licence)

---

## 🎯 Aperçu

Ce dashboard cartographique offre une vision complète du marché immobilier et du cadastre à La Réunion. Il combine :

- 🗺️ **Fond de carte OpenStreetMap** centré sur l'île
- 📍 **Trois couches interactives** : parcelles, bâtiments, transactions DVF
- 📊 **KPIs dynamiques** : prix moyen/m², prix médian, surfaces, nombre de transactions
- 📈 **Graphique de répartition** des transactions par tranche de prix
- 🎛️ **Filtres par commune** parmi les 24 communes officielles
- 🌐 **Décompression automatique** des fichiers `.json.gz` (via `DecompressionStream` ou fallback `pako`)

---

## ✨ Fonctionnalités

### 🗺️ Carte interactive
- Clustering des marqueurs pour des performances optimales (Leaflet.markercluster)
- Popups détaillés pour chaque entité (section, numéro, surface, type, prix…)
- Contrôles d'affichage des couches (checkboxes : Parcelles / Bâtiments / Transactions)

### 📊 Indicateurs clés (KPI)
| Indicateur | Description |
|------------|-------------|
| 💰 Prix moyen / m² | Moyenne des prix au mètre carré |
| 🏠 Transactions | Nombre de transactions sur la commune |
| 📐 Surface moy. vente | Surface moyenne des biens vendus |
| 📈 Prix médian | Prix médian des transactions |
| 🗂️ Nb parcelles | Nombre total de parcelles cadastrales |

### 📈 Graphique Chart.js
- Répartition des transactions par tranche de prix (6 intervalles dynamiques)
- Mise à jour automatique selon la commune sélectionnée

### 🏘️ Couverture géographique
Les 24 communes de La Réunion sont supportées :

| Code INSEE | Commune | Code INSEE | Commune |
|------------|---------|------------|---------|
| 97401 | Les Avirons | 97413 | Sainte-Leu |
| 97402 | Bras-Panon | 97414 | Sainte-Louis |
| 97403 | Entre Deux | 97415 | Saint-Joseph |
| 97404 | Étang Salé | 97416 | Saint-Pierre |
| 97405 | Petite Île | 97417 | Saint-Philippe |
| 97406 | La Plaine des Palmistes | 97418 | Sainte-Marie |
| 97407 | Le Port | 97419 | Saint-Rose |
| 97408 | La Possession | 97420 | Saint-Suzanne |
| 97409 | Saint-André | 97421 | Salazie |
| 97410 | Saint-Benoît | 97422 | Tampon |
| 97411 | Saint-Denis | 97423 | Trois Bassins |
| 97412 | Saint-Joseph | 97424 | Cilaos |

---

## 📂 Structure des données

L'application charge dynamiquement des fichiers GeoJSON compressés (`.json.gz`) :


    📁 repository/
    ├── index.html
    ├── README.md
    └── 📁 data/
        ├── 📁 communes_974/
            │   ├── parcelles-97401.json.gz
            │   ├── parcelles-97402.json.gz
            │   └── ... (24 fichiers)
        └── 📁 communes_974_batiments/
             ├── batiments-97401.json.gz
             ├── batiments-97402.json.gz
             └── ... (24 fichiers)

Format attendu des GeoJSON

Parcelles (parcelles-{code}.json.gz) :

json

{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": { "type": "Polygon", "coordinates": [[[55.5, -21.1], ...]] },
      "properties": {
        "section_cadastrale": "AB",
        "num_lot": "123",
        "surface_cadastrale": 4500
      }
    }
  ]
}

Bâtiments (batiments-{code}.json.gz) :
json

{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": { "type": "Polygon", "coordinates": [[[55.5, -21.1], ...]] },
      "properties": {
        "type_batiment": "Résidentiel",
        "hauteur": 12,
        "surface_habitable": 95
      }
    }
  ]
}

    💡 Astuce : Les fichiers .gz sont automatiquement décompressés côté navigateur grâce à DecompressionStream (natif) ou pako (fallback).

🚀 Installation
Prérequis

    Un navigateur moderne (Chrome, Firefox, Edge, Safari)

    Un serveur HTTP local pour éviter les restrictions CORS sur fetch()

Étapes

    Cloner le dépôt
    bash

    git clone https://github.com/votre-utilisateur/dashboard-cadastre-reunion.git
    cd dashboard-cadastre-reunion

    Lancer un serveur local
    bash

    # Python 3
    python -m http.server 8000

    # Node.js (avec npx)
    npx serve .

    # PHP
    php -S localhost:8000

    Ouvrir dans le navigateur
    text

    http://localhost:8000

🎮 Utilisation

    Sélectionner une commune dans le menu déroulant en haut à droite

    Les données (parcelles, bâtiments, transactions) se chargent automatiquement

    Cocher/décocher les couches pour affiner l'affichage

    Cliquer sur un marqueur pour voir les détails

    Consulter les KPIs et le graphique en bas de l'écran

🛠️ Technologies
Technologie	Usage
Leaflet 1.9.4	Carte interactive
Leaflet.markercluster 1.5.3	Clustering des marqueurs
Chart.js	Graphiques statistiques
Pako 2.1.0	Décompression gzip (fallback)
OpenStreetMap	Fond de carte


🤝 Contribuer

Les contributions sont les bienvenues !

    Fork le projet

    Créer une branche (git checkout -b feature/amelioration)

    Commit les changements (git commit -m 'Ajout fonctionnalité X')

    Push (git push origin feature/amelioration)

    Ouvrir une Pull Request

Idées d'amélioration

    □

    Ajout de filtres par type de bien (appartement/maison)
    □

    Export CSV des transactions
    □

    Comparaison multi-communes
    □

    Intégration de données DVF réelles via API
    □

    Mode sombre

📄 Licence

Ce projet est distribué sous licence MIT. Voir le fichier LICENSE pour plus d'informations.
🙏 Remerciements

    IGN – Données cadastrales

    DVF – Données de valeurs foncières

    OpenStreetMap – Fond de carte

    Communauté Leaflet & Chart.js

### Liens WEBSITE :

    https://gunout.github.io/dashboard-cpf-reunion/

### EXAMPLE :

<img width="1807" height="761" alt="Screenshot 2026-09-04 at 13-26-15 🏝️ Dashboard Cadastre   Immobilier – La Réunion" src="https://github.com/user-attachments/assets/4243b70d-b611-4a8b-a682-f81be9c71ac6" />

---

<div align="center">

### 🇫🇷 Gunout · 2026

![Made in France](https://img.shields.io/badge/Made_in-France-002395?style=flat-square&labelColor=FFFFFF&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA5MDAgNjAwIj48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjYwMCIgZmlsbD0iIzAwMjM5NSIvPjxyZWN0IHdpZHRoPSI5MDAiIGhlaWdodD0iNDAwIiB5PSIxMDAiIGZpbGw9IiNmZmYiLz48cmVjdCB3aWR0aD0iOTAwIiBoZWlnaHQ9IjIwMCIgeT0iNDAwIiBmaWxsPSIjZWQyOTM5Ii8+PC9zdmc+)
![GitHub](https://img.shields.io/badge/GitHub-gunout-181717?style=flat-square&logo=github&logoColor=white)
![Year](https://img.shields.io/badge/2026-ED2939?style=flat-square&labelColor=FFFFFF)

<sub>© 2026 <strong>gunout</strong> — Tous droits réservés.</sub>

</div>
