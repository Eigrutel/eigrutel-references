# References

Version 1.0.0 --- 3 septembre 2026

**References** est une application web bilingue permettant de
constituer, classer et sauvegarder des tableaux de références visuelles
à partir de liens web.

Le programme est conçu et développé par **Simon Léturgie** dans le cadre
d'**Eigrutel BD Academy** et d'**Eigrutel Lab --- Atelier d'outils
libres pour la bande dessinée**.

## Fonctionnalités

-   ajout et édition de références web ;
-   vignettes, descriptions, catégories et mots-clés ;
-   favoris ;
-   recherche et filtres ;
-   tri par catégorie par défaut ;
-   réorganisation manuelle par glisser-déposer ;
-   catégories et couleurs personnalisables ;
-   nom personnalisable du tableau ;
-   sauvegarde automatique locale ;
-   import et export JSON ;
-   restauration d'un catalogue de références proposé ;
-   interface français / anglais ;
-   utilisation sur ordinateur, tablette et téléphone.

## Utilisation

L'application publiée doit être servie avec son dossier `data`, car le
catalogue initial est chargé depuis `data/references-default.json`.

Ouvrir `ref.html` depuis un serveur web ou utiliser la version publiée
via GitHub Pages.

## Sauvegarde

Le travail courant est conservé dans le `localStorage` du navigateur. Il
n'est pas hébergé par l'application.

Pour conserver une sauvegarde indépendante du navigateur, utiliser
**Sauvegarder**. Le fichier exporté porte un nom de la forme
`reference_nom_du_projet.json`.

## Structure

-   `ref.html` : application ;
-   `data/references-default.json` : catalogue proposé ;
-   `index.html` : page de présentation ;
-   `ARCHITECTURE.md` : documentation technique ;
-   `docs/images/` : captures d'écran ;
-   `favicon/favref.png` : favicon.

## Auteur

Simon Léturgie\
Eigrutel BD Academy\
Eigrutel Lab --- Atelier d'outils libres pour la bande dessinée\
https://www.stripmee.com/

## Licences

Code : **GNU AGPL v3.0 ou version ultérieure**.\
Documentation et modèles : **CC BY-SA 4.0**, sauf mention contraire.\
Marques, logos et signes distinctifs Eigrutel / Eigrutel Lab / Eigrutel
BD Academy : **réservés**.

Les ressources externes référencées par l'application restent soumises
aux droits et licences de leurs propriétaires respectifs.

Voir `LICENSE.md` et `NOTICE.md`.
