# Letterform Cartographer

Une carte du système d'un glyphe: la minuscule **a** en Clarendon LT Std roman.Onze cartes de noms — neuf vivants, un reste, un fantôme — chacune citant une gamme exacte du contour de la police réelle, pas une approximation redessinée de celui-ci.

## Démo en direct

`docs/index.html` — un diagramme survolé de la lettre. Chaque survol récupère et affiche la carte `.md` réelle à partir de `objects/`, en direct, directement à partir de ce dépôt. Rien dans le diagramme n'est une copie des cartes; c'est un visualiseur sur elles. Servez-le à partir de la racine du dépôt (GitHub Pages: source = `/ (root)`, pas `/docs`) de sorte que la récupération relative de ZQx0 à `../objects/*.md` se résout — Les pages restreintes à ZQ X5 seules donneraient 404 sur chaque carte.

## Pourquoi cela existe-t-il

« Bol », « compteur », « éperon » sont des noms qu’un humain dessine autour de plages de ces données — rien dans un fichier de police ne s’étiquette lui-même. Ce référentiel est cet étiquetage, fait une fois, cité à la fois par rapport au contour extrait réel (`fontTools`) et à une compétence de référence typographique chargée, de sorte que personne n’ait à le redériver à l’œil nu.

## Le seul fantôme, expliqué à l'avance

Clarendon est une serif de type slab — c'est la première et souvent la seule chose que tout le monde sait à son sujet, et cela crée une attente confiante et fausse : que chaque trait dans la face se termine par un pied de type slab entre parenthèses. Cette minuscule `a` ne le fait pas. Sa tige se termine par une épine incurvée, sa finition par un terminal sphérique, et il n'existe pas de pied de serif n'importe où sur la lettre. Ce n'est pas une simplification ou un choix artistique décrit vaguement — c’est un fait concernant le contour réel, vérifié par rapport à un deuxième [`objects/foot-serif.md`](objects/foot-serif.md) indépendant après que la première extraction ait été presque rejetée comme corrompue pour manquer du serif même que ce README vous a dit de ne pas attendre.

## Comment un inconnu — ou une session d’IA froide — utilise-t-il cela?

1. Lisez `identity.md` et `rules.md` une fois. Ils sont courts.
2. Ouvrez `examples.md`. C'est une table de catalogue des onze pièces plus trois courtes promenades travaillées.
3. Besoin d'une pièce? Ouvrez exactement sa carte dans `objects/`. Arrêtez-vous là.
4. Vous avez trouvé un nom qui n'est pas dans le catalogue ("arch", "tail")? Vérifiez d'abord `reference/naming-collisions.md`. Il y a très probablement déjà une réponse.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## Ce qui est ici

| Path | Job |
| --- | --- |
| `identity.md` | Qui est le cartographe, de quel territoire s’agit-il, qui est le lecteur ultérieur |
| `rules.md` | Ce qui compte comme un nom ici, comment Live/Leftover/Ghost sont décidés, la règle Hits/Does-not-hit |
| `examples.md` | Le tableau du catalogue + trois promenades travaillées, daté 2026-08-21 |
| `objects/` | Les onze cartes elles-mêmes — les étagères réelles |
| `reference/card-types.md` | Les trois formes de cartes utilisées par ce territoire |
| `reference/naming-collisions.md` | Quatre vrais pièges de vocabulaire, écrits une fois |
| `reference/decisions.md` | Décisions consignées (choix de police, corrections terminologiques, technique de rendu) avec justification |
| `docs/index.html` | Le diagramme en direct — un visualiseur sur `objects/`, pas une copie de celui-ci |

## Ce que ce n'est pas

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Territoire et approvisionnement

- Fonte: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), vérifiée par rapport à un deuxième Clarendon indépendant avant utilisation — voir `reference/decisions.md`.
- Terminologie : Compétence `typography-fundamentals` (glossaire, notes de contre-formule, référence de classification) Deux termes rédigés de mémoire avant cette vérification (« arc », « queue ») étaient incorrects et ont été remplacés par les termes réels de la compétence (« finial », « éperon »).
- Le diagramme décrit le glyphe et les onze mots de l'étiquette comme des chemins vectoriels plutôt que d'intégrer soit Clarendon ou Akzidenz-Grotesk comme polices web — les deux sont des logiciels de polices commerciaux ; seules les formes de lettres spécifiques utilisées comme illustrations de diagramme sont livrées, pas les polices elles-mêmes.Le texte du corps de la carte (qui est une prose sans limite, pas une liste fixe de mots) utilise une pile de polices CSS système — Helvetica Neue, en revenant à Helvetica, Arial et sans-serif — donc il n'envoie aucun fichier de police de toute façon.

Construit en suivant la sixième forme décrite dans Weekly Comp #11: The Cartographer — une carte système d'un corps de travail réel et en vigueur, utilisant les invariants de la compétence ICM Architect (github.com/RinDig/icm-architect) comme échafaudage.
