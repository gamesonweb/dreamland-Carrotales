# Documentation du jeu
Cette documentation présente, à un niveau global, les choix techniques et les fonctionnalités mises en place dans le jeu, sans entrer dans les détails de l’implémentation ou de la structure du code.

---

## 1. Vue d’Ensemble

Le jeu est construit autour d’un moteur 3D (Babylon.js) et d’un moteur de physique (Havok). L’architecture repose sur plusieurs modules, chacun responsable d’une fonctionnalité précise (gestion du personnage, des ennemis, des quêtes, des mini-jeux, etc.). Les interactions entre ces modules sont orchestrées par un fichier principal qui initialise la scène, charge les ressources et lance la boucle de jeu.

---

## 2. Personnalisation du Personnage

Le joueur peut choisir l’aspect visuel de son avatar en sélectionnant différents accessoires. Cette personnalisation est appliquée au modèle 3D du personnage dès le démarrage ou depuis un écran dédié dans l’interface.

---

## 3. Physique et Mouvement

  - Le personnage utilise un contrôleur physique qui gère la gravité, les collisions et la détection de terrain.  
  - Le joueur se déplace en toute fluidité dans l’environnement. Nous avons fais notre maximum pour que les déplacements soient "agréables".

---

## 4. Plateformes Mobiles

  - Des plateformes se déplacent le long de trajectoires prédéfinies (horizontales, verticales ou circulaires). Le déplacement se fait grâce à des animations couplées à la physique, garantissant que le personnage peut monter dessus et être transporté sans glisser.


---

## 5. Systèmes d’ennemis et PNJ

- **Abeilles** :  
  - Les adversaires patrouillent dans des zones définies, détectent le joueur à une certaine distance, puis passent en mode poursuite.  
  - Lorsque l’ennemi atteint le joueur ou est touché par une attaque, il réagit (anim réactif, projection via physique).  
  - Si l’ennemi perd le joueur de vue, il retourne à sa position de patrouille après un délai.

- **Moutons à corne** :  
  - Les moutons à cornes ont les memes comportements que les abeilles, exceptés qu'ils sont "bloqués" dans la grotte du niveau 3. Il ne peuvent pas en sortir.

- **PNJ** :  
  - Des personnages dotés d’un comportement limité : ils restent attachés à un lieu, proposent des dialogues et offrent des quêtes ou informations.  
  - Lorsqu’on interagit avec un NPC, une interface s’ouvre pour afficher des textes, des choix ou lancer une quête associée.

---


## 6. Système de Quêtes

- **Définition et Suivi** :  
  - Chaque quête possède un objectif principal (collecte, élimination d’ennemis, interaction avec un NPC, mini-jeu, etc.).  
  - Le suivi des objectifs se fait en temps réel (nombre d’objets collectés, ennemis vaincus), et l’interface affiche la progression.

- **Déclenchement et Récompenses** :  
  - Les quêtes démarrent après dialogue avec un NPC.  
  - Une fois l’objectif atteint, le joueur peut retourner chez le donneur de quête pour débloquer un des cadenas du 3e niveau.

- **Gestion des Étapes** :  
  - Certaines quêtes sont multi-étapes : débloquer un nouvel objectif après validation de la phase précédente.  

---

## 7. Collecte de Carottes et Objets

- **Carottes** :  
  - Dispersées dans le décor, elles servent de monnaie.
  - Plusieurs moyens d'en gagner (récolte, pêche, jeu de dés, coffres) 
  - Elles servent à débloquer des boost ou des nouvelles compétences

---

## 8. Mécaniques de Pêche

Inspiré du jeu Stardew Valley, nous avons ajouté une mécanique de pêche dans notre jeu.

- **Point de Pêche** :  
  - Des endroits spécifiques (lacs) sont identifiés comme zones de pêche.  
  - Lorsque le joueur lance sa ligne, une mini-interface apparaît pour pouvoir pécher.

- **Mini-Jeu de Pêche** :  
  - Basé sur une jauge qui se déplace verticalement. Le joueur doit maintenir la jauge dans une zone verte pendant une durée définie pour réussir à pêcher.  

- **Variété de loot** :  
  - Deux types de drop possibles : le drop basique (entre 1 et 5 carottes), et le "rare loot" qui donne 25 carottes.

---

## 9. Mini-Jeux 

- **Jeu de dés** :  
  - disponible aux niveau 1 et 2, on peut miser des carottes pour espérer en gagner plus.

- **Parcours** :  
  - Un mini jeu de parcours a été ajouté en tant que quête du niveau 3. Il faut réussir le parcours dans un temps imparti, avec deux chances. 

- **Piñata** :
  - Un mini jeu style "combat" a été ajoute en tant que quête pour le niveau 3. Il faut taper 3 fois la piñata pour la détruire, entre chaque coup elle explose et crée une zone autour d'elle qui tue le joueur s'il reste proche. 
---

## 10. Gestion des Ennemis et des Créatures (Managers)

  - Au démarrage d’une zone, un système parcourt une liste de positions prédéfinies pour instancier les ennemis et les moutons.  
  - Lorsqu’un ennemi est vaincu, il peut réapparaître après un délai ou rester définitivement disparu suivant la configuration de la zone.


---

## 11. Gestion Audio

- **Musique d’Ambiance** :  
  - Une musique de fond a été ajoutée. Il y a également une musique plus stressante qui se lance quand un ennemis nous course.

- **Effets Sonores** :  
  - Différents effets sonores ont été ajoutés

- **Volume et Paramètres** :  
  - Une interface permet de régler le volume de la musique et des effets séparément (touche V).  

---

## 12. Menu

  - Écran de démarrage (nouvelle partie, charger partie, options).  
  - Options : contrôles, possibilité d'activer un mode triche.  
  - Écran de sélection de personnage et de personnalisation.


---

## 13. Caméra et Contrôle de Vue

- **Caméra Troisième Personne** :  
  - Suivi du personnage 
  - La caméra se repositionne automatiquement pour éviter les collisions avec les décors (ajustement dynamique de l’angle et de la distance).

- **Zones Spéciales** :  
  - Dans certains espaces (intérieurs, mini-jeux), la caméra peut basculer en vue fixe ou en vue « coupée » pour mettre en valeur l’action ou simplifier la jouabilité.

- **Mouvements de Caméra lors des Événements** :  
  - Des cinématiques simplifiées (déplacements prédéfinis) sont déclenchées pour des moments clés (fin de quête).

---

## 14. Logique de Niveau et Chargement

- **Découpage en Zones** :  
  - Le monde est divisé en zones distinctes. Lorsqu’on progresse d’une zone à l’autre, le moteur charge les ressources nécessaires (textures, modèles, sons), et on nettoie tous les meshs entre les différents niveaux.

## 15. Boutiquie : Pouvoir activables et Boosts

- **Sort de gel** : permet de geler les ennemis pendant 5 secondes. Débloquable dans la boutique
- **Sort de speed** : permet de gagner un boost de vitesse pendant 10 secondes. Débloquable dans la boutique
- **Boost de range**  qui permet de récolter les carottes de plus loin
- **Carrot Lover** qui ajoute +1 à la valeur des carottes récupérables
- **Life Insurance** qui permet au joueur de réapparaître sans délai lorsqu'il meurt dans le vide pour la première fois pendant un niveau
- **Tip** : donne un pourboire de 10 carottes au marchand. Sert seulement à rendre le marchand plus heureux !
