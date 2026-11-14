## Carte travaillée — Clarendon minuscule `a`

Territoire: un glyphe, `ClarendonLTStd.otf`, cité le 2026-08-21. Onze cartes vivent dans [`objects/`](objects/) — ce fichier est le catalogue, pas une copie d'entre elles. La terminologie a été vérifiée par rapport au glossaire des compétences de `typography-fundamentals`; deux termes rédigés de mémoire (« arche », « queue ») étaient incorrects et ont été remplacés — voir [`reference/decisions.md`](reference/decisions.md).

### Catalogue

| Partie | Type | Statut | Carte |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Stem | accident vasculaire cérébral | Live | [`objects/stem.md`](objects/stem.md)                      |
| Bowl | accident vasculaire cérébral | Live | [`objects/bowl.md`](objects/bowl.md)                      |
| Finial | accident vasculaire cérébral | Live | [`objects/finial.md`](objects/finial.md)                  |
| Borne à bille | stroke ending | Live | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Trace | stroke ending | Live | [`objects/spur.md`](objects/spur.md)                      |
| Compteur | Espace négatif | Live, dérivé | [`objects/counter.md`](objects/counter.md)                |
| Ouverture | Espace négatif | Live, dérivé | [`objects/aperture.md`](objects/aperture.md)              |
| x-hauteur | Unités métriques | Live | [`objects/x-height.md`](objects/x-height.md)              |
| Niveau de référence | Unités métriques | Live | [`objects/baseline.md`](objects/baseline.md)              |
| Overshoot | correction | Restes | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot serif | accident vasculaire cérébral | 👻 fantôme | [`objects/foot-serif.md`](objects/foot-serif.md)          |

Un lecteur à froid s'arrête ici à moins qu'une partie ait besoin d'être ouverte.

### Une promenade, en entier

*Question: "Je veux donner à ce Clarendon `a` un pied de plaque plus lourd pour correspondre au reste du visage. Qu'est-ce que cela touche?"*

1. Ouvrez le catalogue ci-dessus. “Foot serif” est la porte évidente.
2. Open `objects/foot-serif.md`. It says, in the first line of body text: there is no foot serif on this glyph. Status: **ghost**.
3. La prémisse de la question est erronée — il n'existe pas de pied-sérif à rendre plus lourd. La carte nomme également les deux vrais traits qu'un lecteur aurait pu vouloir dire à la place : [`spur`](objects/spur.md) et [`ball-terminal`](objects/ball-terminal.md), et explique, avec une marche coordonnée citée, pourquoi aucun n'est un serif.

Aucune autre carte n'a dû être ouverte pour répondre à cette question, c'est le but du catalogue.

### Une deuxième promenade, plus courte

**Question:** "Qu'est-ce que le comptoir, et puis-je le rendre plus grand par lui-même?"

1. Ouvrez `objects/counter.md`.
2. **Hits**: Rien directement — il est dérivé de `bowl` et `stem`.
3. **Does not hit**: L'ouverture, une forme blanche séparée que les gens veulent généralement dire à la place.
4. Réponse: non, pas seul. Editez `bowl` ou `stem`; le compteur suit. Stop.

### Une troisième promenade, sur le vocabulaire lui-même

**Question:** "Comment s'appelle l'arche sur ce a?"

1. Il n'y a pas de `arch.md`. Le catalogue n'a pas de ligne nommée "Arch".
2. `reference/naming-collisions.md` nomme cette question exacte et pointe vers [`objects/finial.md`](objects/finial.md) — le terme basé sur la compétence pour cette lettre, avec la raison pour laquelle « arche » ne s'applique pas ici (elle ne revient jamais à la ligne de base, donc ce n'est pas une).
3. Arrêtez, avec le vocabulaire corrigé, pas seulement la géométrie située.
