## Types de cartes (jeu fermé)

Trois types de cartes existent sur ce territoire.

### Course / fin de course

Champs obligatoires : ce qu'il s'agit (une ligne, nommant le terme défini par la compétence), statut avec plage de points citée, hits, ne touche pas.

### Espace négatif (dérivé)

Une forme délimitée par des traits sans contour propre — le compteur, l’ouverture. Les champs requis sont les mêmes, mais les « coups » pour ceux-ci sont presque toujours « rien de direct ». Une forme dérivée n’a pas de géométrie à modifier, seulement des traits qui la délimitent.

### Métrique

Une ligne de référence de la largeur de la police, qui ne fait pas partie du contour propre du glyphe — x-height, baseline, overshoot.Ces derniers citent les propres tables de la police (`OS/2`, `hhea`) plutôt que le contour, et leur ligne « hit » nomme chaque glyphe dans la police, pas seulement celui-ci — le seul endroit dans ce territoire où le rayon de détonation d'une carte quitte la lettre.

## Le fantôme n'est pas un quatrième type

`foot-serif.md` utilise le modèle Stroke avec `status: ghost`.Un fantôme ne prend pas sa propre forme — il prend la forme attendue par le lecteur, rempli de la découverte que rien n'est là.

## Si une douzième partie apparaît

Seulement si le contour lui-même change (une épaisseur différente, un glyphe redessiné) — une nouvelle carte suit l'un des trois modèles ci-dessus et est ajoutée à la table du catalogue dans `examples.md`.`examples.md` reste un instantané daté sinon.
