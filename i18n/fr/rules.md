## Ce qui compte comme un nom

Un **anatomical part**: une plage nommée du contour du glyphe, ou une ligne de référence nommée de la largeur de la police par rapport à laquelle le contour est mesuré.Onze existent dans ce territoire - neuf vivants, un reste, un fantôme.

Deux sortes de noms:

- **Stroke parts** (tige, cuvette, bout, extrémité sphérique, éperon) — un tronçon contigu du contour extérieur.
- **Derived shapes** (contre, ouverture) — espace blanc délimité par des parties de trait, sans contour propre.
- **Metrics** (x-height, baseline, overshoot) — lignes de référence horizontales des propres tables de la police, pas du tout le contour du glyphe.

## Ce qui compte comme mouvement

L'édition d'une partie de trait modifie la plage de contour qu'elle nomme, et tout ce que la plage borde structurellement. Une tige partageant un bord avec le compteur signifie que l'élargissement de la tige rétrécit le compteur - c'est un vrai succès, citez-le.Une tige ne partageant rien avec la hauteur x signifie que changer la tige ne la touche jamais - c'était un vrai échec, citez aussi.

Les métriques se déplacent différemment : elles touchent *tous les glyphes de la police*, jamais seulement celui-ci. Cette asymétrie — un changement de trait d'un glyphe reste local, un changement de métrique à l'échelle de la police devient global — est la chose la plus importante qu'une carte dans ce territoire puisse faire correctement.

## Live / Restover / Ghost, défini pour ce territoire

- **Live** — La partie correspond à une plage réelle du contour réel, cité par index de point et coordonnée.
- **Leftover** — La pièce est réelle et présente, mais sa raison d'être est une correction d'une tradition de conception antérieure, pas une caractéristique de ce glyphe en soi.Le dépassement: fait toujours son travail, vaut toujours la peine d'être expliqué, pas quelque chose à "réparer".
- **Ghost** — Le fantôme de ce territoire, le foot serif, existe précisément parce que la catégorie propre de la police (slab serif) établit une attente à laquelle cette lettre ne répond pas, et qu'il n'y a rien derrière lui dans ce glyphe spécifique.

## Hits / Ne frappe pas

Chaque carte se termine par exactement deux lignes. **Hits** nomme le vrai voisin structurel, **Does not hit** nomme le mauvais voisin que le lecteur devinera d'abord — généralement la partie qui semble adjacente dans la forme de lettre rendue mais qui ne partage aucune limite réelle dans les données de contour.

## Refus

- Pas besoin de coller les données brutes du chemin du glyphe dans une carte comme si c'était une explication — citez les plages de points et les limites, même discipline que de citer un chemin de fichier au lieu de coller un script.
- Pas de traitement d'une forme dérivée (compteur, ouverture) comme si elle avait une géométrie indépendante à modifier.
- Une partie qui n'existe pas reçoit une carte qui le dit, et non le silence.

## Comment une carte est construite

Avant d'écrire n'importe quelle carte: extrayez le contour réel (`fontTools`, pas une image rendue, pas une mémoire de ce à quoi Clarendon "devrait" ressembler), identifiez la plage de points que la partie occupe, et vérifiez-la par rapport à une deuxième source indépendante de la même police avant de faire confiance à tout ce qui semble surprenant.Cette carte fantôme du territoire existe parce que cette vérification était nécessaire - le premier regard sur le contour semblait faux précisément là où il était en fait correct.
