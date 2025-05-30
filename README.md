![Logo](carotales.png)

Jeu hébergé sur : https://shanto0o.github.io/3D-Game-Project-Carotales/

GitHub du projet : https://github.com/Shanto0o/3D-Game-Project-Carotales

Vidéo de présentation du gameplay : https://www.youtube.com/watch?v=PiP7ZgeqVu0

## Groupe
- **Florent Belot**
- **Shanti Noel**
- **Alexis Dubarry**

## Description
Carotales est un jeu de plateforme 3D dans lequel vous incarnez un lapin aventurier ; collectez un maximum de carottes, franchissez les niveaux dans le temps imparti et, enfin, accédez à la Carotte Sacrée.

## Niveaux
1. **Niveau 1** : île flottante avec une montagne. Deux chemins (facile / difficile) et deux mini-jeux : pêche et dés.
2. **Niveau 2** : apparition des ennemis (abeilles). Objectif : collecter des carottes et atteindre la fin avant la montre.
3. **Niveau 3** : la Carotte Sacrée est derrière un portail protégé par **4 cadenas**. Pour les ouvrir, 4 quêtes :
   - **Quête de pêche** : repêcher l’objet perdu du PNJ dans l’étang.
   - **Parcours chronométré** : finir un parcours en moins de 90 s.
   - **Récupération de clé** : explorer une grotte et rapporter la clé au PNJ.
   - **Combat de boss** : affronter une pinata, subir son explosion, ramasser les bonbons et les déposer pour terminer la quête.
   Une fois les 4 cadenas déverrouillés, le portail disparaît et vous accédez à la Carotte Sacrée.

## Fonctionnalités principales
- **Moteur physique Havok** avec particules et animations.
- **Ombres en temps réel** et collision caméra empêchant la traversée des murs.
- **Synchronisation** du personnage avec les plateformes mouvantes.
- **Boutique entre les niveaux** : compétences actives (freeze, speedboost) et améliorations passives.
- **Mini-jeux** : pêche, dés.
- **Système de quêtes** avec gestion du journal de quêtes (touche P).
- **Boss final** avec système de loot (bonbons).


## Modèles et animations 
- **Fait main!** : Nous avons réalisés nous-même presque tous les modèles de notre jeu (lapin, accessoires, mouton, Map de tous les niveaux), et toutes les animations ! 

## Personnalisation
Avant de démarrer la partie, vous pouvez personnaliser l’apparence de votre lapin en lui attribuant divers accessoires.

- **Bouton Personnaliser** : dans le menu principal, cliquez sur « Customize » pour ouvrir le panneau de personnalisation.
- **Sélection** : cochez la case de l’accessoire souhaité dans chaque catégorie.
- **Appliquer / Fermer** : cliquez sur « Appliquer » pour enregistrer vos choix, ou « Fermer » pour annuler.
- Les accessoires sélectionnés sont chargés au démarrage du jeu via la variable `accessoriesConfig` et affichés sur votre lapin.

## Commandes
- **Z / Q / S / D** : déplacement. (jouable en qwerty)
- **Espace** : sauter.
- **E** : interagir.
- **Q** : compétence Freeze (cooldown : 60 s).
- **R** : Speedboost (cooldown : 60 s).
- **G** : parler aux PNJ.
- **P** : ouvrir/fermer le livre de quêtes.
