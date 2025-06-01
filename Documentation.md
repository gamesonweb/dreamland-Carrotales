# Documentation Technique du Jeu

Cette documentation présente, à un niveau global, les choix techniques et les fonctionnalités mises en place dans le jeu, sans entrer dans les détails de l’implémentation ou de la structure du code.

---

## 1. Vue d’Ensemble

Le jeu est construit autour d’un moteur 3D (Babylon.js) et d’un moteur de physique (Havok). L’architecture repose sur plusieurs modules, chacun responsable d’une fonctionnalité précise (gestion du personnage, des ennemis, des quêtes, des mini-jeux, etc.). Les interactions entre ces modules sont orchestrées par un fichier principal qui initialise la scène, charge les ressources et lance la boucle de jeu.

---

## 2. Personnalisation du Personnage

- **Apparence et Équipement** : Le joueur peut choisir l’aspect visuel de son avatar en sélectionnant différentes couleurs, tenues ou accessoires. Cette personnalisation est appliquée au modèle 3D du personnage dès le démarrage ou depuis un écran dédié dans l’interface.
- **Chargement Dynamique** : Les éléments visuels (corps, vêtements, accessoires) sont chargés au lancement du jeu ou lors de changements en cours de partie, afin de permettre une mise à jour immédiate sans recharger la scène.
- **Sauvegarde des Choix** : Les préférences de personnalisation sont mémorisées pour être restaurées automatiquement lors des sessions suivantes.

---

## 3. Physique et Mouvement

- **Intégration de la Physique Havok** :  
  - Le personnage utilise un contrôleur physique qui gère la gravité, les collisions et la détection de terrain.  
  - Les objets interactifs (coffres, plates-formes, barils, etc.) bénéficient de la physique pour rebondir, glisser ou basculer de manière réaliste.  
  - Les détections de contact (au sol, avec les murs) sont utilisées pour autoriser les sauts, les glissades ou les chutes.

- **Contrôles de Déplacement** :  
  - Le joueur se déplace en toute fluidité dans l’environnement 3D, avec prise en compte de l’inertie, de la friction et de la réponse aux pentes.  
  - Les sauts et la détection du sol sont gérés par la physique pour éviter les « sautillages » ou les traversées de sol involontaires.

---

## 4. Plateformes Mobiles et Environnement

- **Plateformes Animées** :  
  - Des plateformes se déplacent le long de trajectoires prédéfinies (horizontales, verticales ou circulaires). Le déplacement se fait grâce à des animations couplées à la physique, garantissant que le personnage peut monter dessus et être transporté sans glisser.
  - Le système gère les phases d’arrêt et de redémarrage pour offrir des chemins dynamiques.

- **Éléments Interactifs** :  
  - Des leviers, interrupteurs ou boutons déclenchent des mouvements (ouverture de ponts, montée de plateformes).  
  - Certains objets du décor ont des réactions physiques (bascules, chutes) lorsque le joueur agit ou passe à proximité.

- **Collision et Limites du Niveau** :  
  - L’ensemble du décor utilise des volumes de collision (murs invisibles, zones de déclenchement) pour empêcher le joueur de sortir de la zone de jeu ou pour déclencher des événements (chutes dans le vide, déclenchement de pièges).

---

## 5. Systèmes d’IA

- **Ennemis** :  
  - Les adversaires patrouillent dans des zones définies, détectent le joueur à une certaine distance, puis passent en mode poursuite.  
  - Lorsque l’ennemi atteint le joueur ou est touché par une attaque, il réagit (anim réactif, projection via physique).  
  - Si l’ennemi perd le joueur de vue, il retourne à sa position de patrouille après un délai.

- **Moutons (Créatures Passe-partout)** :  
  - Les moutons se déplacent de façon erratique dans un périmètre restreint, sans attaquer le joueur.  
  - Ils peuvent réagir à la présence du joueur (fuite sur une courte distance) et reviennent ensuite à leur comportement aléatoire.  
  - Ils servent principalement à peupler le décor et peuvent être « récompenses » visuelles ou des objectifs de quêtes.

- **NPC (Personnages Non-Joueurs)** :  
  - Des personnages dotés d’un comportement limité : ils restent attachés à un lieu, proposent des dialogues et offrent des quêtes ou informations.  
  - Lorsqu’on interagit avec un NPC, une interface s’ouvre pour afficher des textes, des choix ou lancer une quête associée.

---

## 6. Système de Quêtes

- **Définition et Suivi** :  
  - Chaque quête possède un objectif principal (collecte, élimination d’ennemis, interaction avec un NPC, mini-jeu, etc.).  
  - Le suivi des objectifs se fait en temps réel (nombre d’objets collectés, ennemis vaincus), et l’interface affiche la progression.

- **Déclenchement et Récompenses** :  
  - Les quêtes démarrent soit automatiquement à l’accès d’une zone, soit après dialogue avec un NPC.  
  - Une fois l’objectif atteint, le joueur peut retourner chez le donneur de quête pour obtenir une récompense (expérience, orbes, objet spécial).

- **Gestion des Étapes** :  
  - Certaines quêtes sont multi-étapes : débloquer un nouvel objectif après validation de la phase précédente.  
  - Les quêtes liées aux NPC peuvent également débloquer des dialogues supplémentaires ou des fonctionnalités (ouvrir une porte, activer un mécanisme).

---

## 7. Collecte d’Orbes et Objets

- **Orbes Lumineuses** :  
  - Dispersées dans le décor, elles sont visualisées par un effet lumineux distinct.  
  - Lorsqu’on les approche, une animation de ramassage se déclenche et l’orbe est ajoutée au compteur global.  
  - Les orbes servent à débloquer de nouveaux contenus (espaces, compétences, événements).

- **Objets Divers** :  
  - Coffres : contiennent parfois des orbes, des pièces ou des objets de quête.  
  - Ressources : certaines zones contiennent des éléments à collecter pour la fabrication ou l’échange auprès de NPC.

---

## 8. Mécaniques de Pêche

- **Point de Pêche** :  
  - Des endroits spécifiques (bords de l’eau, quais) sont identifiés comme zones de pêche.  
  - Lorsque le joueur lance sa ligne, une mini-interface apparaît pour indiquer la tension ou la probabilité d’attraper un poisson.

- **Mini-Jeu de Pêche** :  
  - Basé sur une jauge qui se déplace verticalement. Le joueur doit maintenir la jauge dans une zone verte pendant une durée aléatoire pour attraper le poisson.  
  - Les poissons ont différentes raretés et permettent d’obtenir des récompenses variées (orbes, objets de collection, améliorations).

- **Variété de Poissons** :  
  - Plusieurs espèces, définies par leur fréquence d’apparition et la difficulté du mini-jeu.  
  - Certains poissons rares n’apparaissent qu’à des heures spécifiques ou sous conditions météo (gérées dans l’environnement).

---

## 9. Mini-Jeux Additionnels

- **Catalogue de Mini-Jeux** :  
  - Au-delà de la pêche, d’autres mini-jeux (ex. : jeu de rapidité, puzzle) peuvent être déclenchés via NPC ou objets spéciaux.  
  - Chaque mini-jeu a sa propre interface et ses propres règles (simple clique, glisser-déposer, mini-plateformes, etc.).

- **Récompenses Liées** :  
  - Réussir un mini-jeu rapporte des points spéciaux, des orbes ou des objets utilitaires.  
  - Certains mini-jeux débloquent des zones cachées ou offrent des indices pour la quête principale.

---

## 10. Gestion des Ennemis et des Créatures (Managers)

- **Chargement et Instanciation** :  
  - Au démarrage d’une zone, un système parcourt une liste de positions prédéfinies pour instancier les ennemis et les moutons.  
  - Lorsqu’un ennemi est vaincu, il peut réapparaître après un délai ou rester définitivement disparu suivant la configuration de la zone.

- **Optimisation** :  
  - Pour éviter de trop charger la scène, les créatures trop éloignées du joueur peuvent être mises en pause (leur IA s’arrête) ou supprimées temporairement.  
  - Lorsqu’elles se rapprochent, elles sont réactivées et retrouvent leur comportement normal.

---

## 11. Gestion Audio

- **Musique d’Ambiance** :  
  - Plusieurs pistes de musique sont associées à différentes zones. Lorsqu’on change de zone, un fondu (cross-fade) garantit une transition en douceur.  
  - Les variations de la musique (plus intense en combat, plus calme en exploration) sont gérées dynamiquement selon le contexte (présence d’ennemis, état de quête, etc.).

- **Effets Sonores** :  
  - Effets de pas, sauts, atterrissages, collisions, bruits de cueillettes, gargouillis d’eau, etc.  
  - Chaque action déclenche l’effet correspondant, avec possibilité de spatialisation (son plus fort si l’action est proche du joueur).

- **Volume et Paramètres** :  
  - Une interface permet de régler le volume de la musique et des effets séparément.  
  - Les préférences audio sont sauvegardées pour être restaurées lors des lancements suivants.

---

## 12. Interfaces Utilisateur (UI)

- **Menus Principaux** :  
  - Écran de démarrage (nouvelle partie, charger partie, options).  
  - Options : réglages graphiques, audio, contrôle.  
  - Écran de sélection de personnage et de personnalisation.

- **Interface en Jeu** :  
  - Barre de vie/énergie, compteur d’orbes et d’objets clés, mini-carte (si activée).  
  - Fenêtre de dialogue pour les interactions avec les NPC : affiche le texte, les choix de réponse et les informations de quête.  
  - Fenêtre de quêtes : liste des quêtes actives, objectifs en cours, progression visuelle.  
  - Fenêtre de personnalisation : permet de modifier en temps réel l’apparence du personnage.  
  - Fenêtres contextuelles pour la pêche, pour les mini-jeux, ou pour l’achat/vente auprès d’un marchand.

- **Transitions et Animations** :  
  - Les fenêtres s’ouvrent et se ferment avec des animations (fondu, glissement) pour garder une cohérence visuelle.  
  - Les notifications (nouvelle quête, objet trouvé) apparaissent en bas de l’écran pendant quelques secondes.

---

## 13. Caméra et Contrôle de Vue

- **Caméra Troisième Personne** :  
  - Suivi du personnage avec un léger retard pour plus de fluidité.  
  - La caméra se repositionne automatiquement pour éviter les collisions avec les décors (ajustement dynamique de l’angle et de la distance).

- **Zones Spéciales** :  
  - Dans certains espaces (intérieurs, mini-jeux), la caméra peut basculer en vue fixe ou en vue « coupée » pour mettre en valeur l’action ou simplifier la jouabilité.

- **Mouvements de Caméra lors des Événements** :  
  - Des cinématiques simplifiées (déplacements prédéfinis) sont déclenchées pour des moments clés (fin de quête, découverte d’un boss).

---

## 14. Logique de Niveau et Chargement

- **Découpage en Zones** :  
  - Le monde est divisé en zones distinctes. Lorsqu’on progresse d’une zone à l’autre, le moteur charge les ressources nécessaires (textures, modèles, sons) et libère celles de la zone précédente pour optimiser la mémoire.

- **Points de Respawn et Checkpoints** :  
  - Des emplacements de sauvegarde automatique ou manuelle : si le joueur meurt, il revient au dernier checkpoint sans devoir tout recommencer.  
  - Les checkpoints sont souvent placés avant les zones à fort risque ou après la validation de quêtes critiques.

- **Transitions Fluides** :  
  - Les chargements sont masqués par un effet de fondu ou un écran de chargement minimaliste pour éviter de casser l’immersion.

---

## 15. Gestion des Ressources et Optimisation

- **Textures et Modèles** :  
  - Utilisation de formats compressés (ex. : `.gz`, `.basis`) pour réduire la taille de téléchargement et la mémoire GPU.  
  - LOD (Niveaux de détail) : les objets éloignés utilisent des modèles simplifiés pour alléger le rendu.

- **Scripts et Modules** :  
  - Chaque fonctionnalité est isolée dans un module, facilitant le débogage et l’extension.  
  - Les modules communiquent via des événements et des échanges de messages, plutôt que de dépendre directement les uns des autres.

- **Gestion de la Mémoire** :  
  - Libération des ressources des zones inactives (textures, géométries, sons).  
  - Réutilisation d’objets (pooling) pour les projectiles ou les particules, afin d’éviter des allocations/désallocations trop fréquentes.

- **Performances** :  
  - Le framerate vise 60 FPS sur configuration moyenne. Les évaluations en temps réel détectent les goulets d’étranglement (nombre d’entités à l’écran, surfaces transparentes).  
  - Les ombres et effets de post-processing sont activés ou désactivés selon la puissance matérielle détectée dans les options.

---

## 16. Gestion des Sauvegardes

- **Progression Globale** :  
  - Les informations de l’état du personnage (position, personnalisation, inventaire, quêtes terminées, orbes collectées) sont sérialisées dans un fichier local ou via un système de stockage web selon la plateforme ciblée.
- **Restoration au Démarrage** :  
  - Lorsqu’on relance le jeu, la dernière sauvegarde est chargée automatiquement pour restaurer l’état exact du monde (quêtes en cours, progrès dans les zones, etc.).
- **Sauvegarde Manuelle** :  
  - Le joueur peut sauver à tout moment via un menu, déclenchant l’écriture de l’état actuel.

---

## 17. Conclusion

Ce document résume, sans plonger dans le détail des variables ou de la structure interne de chaque classe, l’ensemble des choix techniques et des fonctionnalités clés implémentées dans le jeu. L’architecture modulaire, l’usage du moteur de physique Havok, la diversité des systèmes (IA, quêtes, mini-jeux, etc.) ainsi que l’optimisation des ressources contribuent à offrir une expérience fluide et immersive.

Pour toute précision supplémentaire concernant un aspect particulier (logique d’un module, algorithme d’IA, configuration d’un shader, etc.), il est possible de consulter directement le code source ou de demander des éclaircissements sur un point spécifique.
