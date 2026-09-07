# Architecture --- References

Version 1.0.0 --- 3 septembre 2026

## 1. Vue d'ensemble

References est une application web légère fonctionnant principalement
côté navigateur. L'interface, les styles et la logique sont regroupés
dans `ref.html`. Le catalogue livré avec l'application est
volontairement séparé dans `data/references-default.json` afin de
pouvoir corriger ou enrichir les références proposées sans modifier le
moteur de l'application.

Aucun serveur applicatif ni base de données n'est requis.

## 2. Arborescence

``` text
/
├── ref.html
├── index.html
├── README.md
├── NOTICE.md
├── LICENSE.md
├── CHANGELOG.md
├── ARCHITECTURE.md
├── data/
│   └── references-default.json
├── favicon/
│   └── favref.png
└── docs/
    └── images/
        ├── references-desktop.png
        ├── references-mobile.png
        └── references-reglages.png
```

## 3. `ref.html`

Le fichier principal contient :

-   la structure HTML de l'interface ;
-   la feuille de style CSS ;
-   la logique JavaScript ;
-   les textes d'interface français et anglais ;
-   la gestion des tableaux, filtres et catégories ;
-   l'import/export JSON ;
-   la persistance locale ;
-   le chargement du catalogue par défaut.

Le JavaScript est organisé en sections fonctionnelles : données et état,
traductions, utilitaires, sauvegarde/chargement, rendu/filtres,
catégories, glisser-déposer, ajout/édition, import/export,
événements/démarrage.

## 4. État de l'application

L'état courant regroupe notamment :

-   les références ;
-   les catégories ;
-   les couleurs de catégories ;
-   les filtres actifs ;
-   le mode de tri ;
-   la langue ;
-   le nom du tableau ;
-   les informations temporaires d'édition et de glisser-déposer.

Le tri initial est **Catégorie**.

## 5. Stockage local

L'application utilise `localStorage` avec la clé `eba_references_v24`.

Le stockage local est prioritaire lors d'une ouverture normale afin de
préserver le tableau personnel de l'utilisateur. Les données ne sont pas
envoyées à un serveur par l'application.

Conséquence : une modification du catalogue officiel ne remplace pas
automatiquement une bibliothèque locale existante.

## 6. Catalogue par défaut

`data/references-default.json` contient :

-   la liste initiale des catégories ;
-   leurs couleurs ;
-   les fiches de références proposées.

Au premier lancement sans état local, le fichier est chargé par
`fetch()`.

La commande **Restaurer les références par défaut** recharge également
ce fichier et remplace la bibliothèque locale après confirmation.

Le fichier doit être servi par HTTP/HTTPS avec `ref.html`. Une ouverture
locale directe en `file://` peut empêcher le chargement par `fetch()`
selon le navigateur.

## 7. Modèle d'une référence

Une référence comprend principalement :

``` json
{
  "id": "identifiant",
  "title": "Titre",
  "url": "https://...",
  "domain": "example.org",
  "category": "Catégorie",
  "tags": ["mot-clé"],
  "description": "Description",
  "imageUrl": "https://...",
  "favorite": false,
  "createdAt": "date ISO",
  "updatedAt": "date ISO"
}
```

Les identifiants servent à distinguer les fiches. L'URL est également
utilisée lors de certaines opérations de fusion/import.

## 8. Import et export

L'export produit un fichier JSON contenant le nom du tableau, les
catégories, les couleurs et les références.

Le nom du fichier suit la forme :

`reference_nom_du_projet.json`

L'import peut :

-   fusionner les données avec la bibliothèque actuelle ;
-   remplacer entièrement la bibliothèque actuelle.

Le JSON constitue également la sauvegarde portable permettant de
transférer un tableau entre navigateurs ou appareils.

## 9. Vignettes

Les images ne sont pas stockées dans l'application. Chaque fiche
conserve une `imageUrl` externe.

Si une image distante disparaît ou bloque l'affichage, l'application
affiche un visuel de remplacement. Les URL de vignettes du catalogue par
défaut peuvent être corrigées directement dans
`references-default.json`.

## 10. Données et vie privée

References ne nécessite pas de compte utilisateur et n'héberge pas les
tableaux personnels.

Les données de travail restent dans le stockage local du navigateur,
sauf lorsque l'utilisateur choisit explicitement d'exporter un fichier
JSON.

L'utilisateur reste responsable de la conservation de ses sauvegardes
JSON.

## 11. Dépendances

Le programme ne dépend d'aucun framework JavaScript et n'utilise pas de
système de compilation.

Il s'appuie uniquement sur les API web du navigateur, notamment :

-   DOM ;
-   `localStorage` ;
-   `fetch` ;
-   `FileReader` ;
-   Blob / téléchargement de fichiers ;
-   événements souris et tactiles.

## 12. Déploiement

Pour un déploiement complet, conserver les chemins relatifs :

-   `ref.html`
-   `data/references-default.json`
-   `favicon/favref.png`

Le dépôt peut être publié avec GitHub Pages. `index.html` sert de page
de présentation et renvoie vers `ref.html`.

## 13. Maintenance

Pour ajouter ou corriger une référence proposée, modifier en priorité
`data/references-default.json`.

Pour modifier le comportement, l'interface ou la structure des données,
intervenir dans `ref.html` puis :

1.  vérifier la syntaxe JavaScript ;
2.  tester l'ouverture et la restauration du catalogue ;
3.  tester l'ajout, l'édition et la suppression ;
4.  tester les catégories, filtres et tris ;
5.  tester le glisser-déposer sur ordinateur et appareil tactile ;
6.  tester l'import en fusion et en remplacement ;
7.  tester l'export JSON et son nom de fichier ;
8.  vérifier français et anglais ;
9.  tester Safari/iPadOS et au moins un navigateur Chromium ;
10. mettre à jour `CHANGELOG.md` et le numéro de version si nécessaire.
