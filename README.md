# Les Archives de la Composition — Institut expérimental de Shinji Sabaku

« Comprendre la matière avant de prétendre la transformer. »

Carnet scientifique interactif pour le RP de Shinji Sabaku (Sunagakure, Pays du Vent) :
Kōseijutsu, géologie, matrices, forge, expéditions, validation MJ. Même logique que
« Les Sciences du Ciel » de Kagura, mais tout est à l’identité de Shinji : vieux carnet,
manuscrits du désert, atelier de forge, ruines Sabaku.

## Lancer le projet

Aucune dépendance à installer pour construire : `tools/build-single.mjs` prend `esbuild` et React
déjà présents sur la machine (ou dans `node_modules` après `npm install`).

```bash
node tools/build-single.mjs       # → dist-single/index.html (site complet) et dist-single/page.html (page claude.ai)
npx tsc -p tsconfig.json          # vérification des types (stubs React dans tools/stubs si @types manquent)
python3 tests/test_site.py        # tests Playwright : local, page claude.ai, site hébergé, téléphone
```

Trois façons d’ouvrir le site :
- **claude.ai** : la page publiée contient les archives et se republie elle‑même (« Publier » dans le HUD) ;
- **ailleurs (GitHub Pages, Netlify…)** : `index.html` lit ses données dans `donnees/*.json` posés à côté ;
- **fichier seul** : `dist-single/index.html` s’ouvre d’un double‑clic, tout reste dans le navigateur.

## Le Laboratoire des Dunes

La scène d’accueil (SVG 1600 × 900, poussière dans la lumière, braises, parallaxe). Chaque objet
ouvre un lieu des archives :

| Objet | Lieu |
|---|---|
| Carnet ouvert | **Carnet de Shinji** — double page, deux écritures (avant l’accident : manuscrite, de travers, gribouillis ; après la Noèse : tapée, froide, alignée), 11 catégories, tags, humeurs, personnages, notes de marge, croquis, chronologie |
| Dossiers | **Dossiers de recherche** — la fiche complète (numéro, domaine, difficulté, statut, lieu, durée, date RP, matériaux, matrice, origine → application, résultat, validation MJ) |
| Étagère de pierres | **Matériaux** — 24 fiches livrées, six niveaux de compréhension (I Identification → VI Recomposition maîtrisée) avec la justification de chaque niveau |
| Grande matrice | **Kōseijutsu** — Lecture → Décomposition → Recomposition, échange équivalent, stabilisation, Retour de Résonance, les six domaines |
| Matrices au mur | **Bibliothèque des matrices** — diagrammes générés (anneaux, symétrie, nœuds, motif), difficulté, matériaux, chakra, préparation, risques, maîtrise ; les avancées sont scellées par paliers |
| Bras mécanique | **Kōsei no Ude** — schéma technique par couches, fonctions classées, versions V0 → V7 |
| Forge | **Forge & Inventions** — 8 inventions sur plan avec croquis, usure, versions |
| Bibliothèque | **Théories** — rayons par domaine, dont « Conséquences mentales » (Ancien / Nouveau Shinji) et la Matrice de Noèse |
| Carte | **Expéditions** — carte du Pays du Vent, épingles posées d’un clic |
| Coffre rouge | **Les Portes Interdites** — dix tabous, la conscience déjà franchie ; Pierre Philosophale (ANOMALIA) et Khepri scellés |
| Mur de plans | **Projets** — étapes à cocher, liens, plans retournés contre le mur tant que les Éclats manquent |
| Chronomètre | **Chronologie RP** — ligne verticale, avant / après l’accident |
| Lettre scellée | **Validation MJ** — validation fondatrice (7 conditions), dossiers côté MJ, **rapport MJ** (imprimable, PDF, .md, dépôt en attente) |
| Jarre de sable d’or | **Éclats de Compréhension** — d’où ils viennent, paliers, ce qu’ils ouvrent |
| Instruments | **Simulations** — Analyse de roche, Composition, Construction de matrice, Résonance, Forge, Diagnostic du bras ; chaque séance écrit une page au carnet |

`Ctrl + K` : recherche globale (tout est fouillé, des dossiers aux Portes).

## Classification

Rien n’est présenté comme acquis. Chaque élément porte un mot : **CONNU** (maîtrisé),
**EXPÉRIMENTAL** (en test), **THÉORIQUE** (pensé possible), **INTERDIT** (refusé), **FUTUR**
(prochain dossier MJ). Le niveau autorisé par les MJ est affiché sur la page Kōseijutsu et dans
le rapport.

## Éclats de Compréhension

Pas un niveau de combat. Ils se gagnent en terminant des recherches (3), en notant des observations (2),
en comprenant un matériau au‑delà de l’identification (1 par niveau, +2 au niveau IV), en stabilisant
des matrices (3), en analysant un échec (2), en menant des expéditions (3), en obtenant une validation
MJ (4), en écrivant des pages (1), en rendant une invention fonctionnelle (3), en réalisant une version
du bras (1), en menant des simulations (1, 25 au plus).

Paliers : 0 Apprenti des dunes · 30 Lecteur de grains (lumière du soir, Matrice Métallurgique) ·
45 Traceur (Matrice Cristalline, matrices du mur allumées) · 60 Compositeur (Grande Matrice
Territoriale, forge plus vive) · 80 Chercheur du désert (Khepri, nuit sur les ruines) · 100 Gardien des
Portes (Pierre Philosophale) · 140 Maître de Composition (sceau doré). Le site livré part à 24.

## Sauvegarde

- **Automatique** dans le navigateur (`localStorage` pour les données, IndexedDB pour les images et
  les copies de secours). Un visiteur d’une page publiée ne laisse rien dans son navigateur.
- **Export / import** : un fichier `.json` complet (images comprises), fusion ou remplacement ;
  copies de secours horodatées ; « tout effacer » prend une copie avant.
- **Fusion sans perte** : chaque élément porte sa date de modification, les suppressions laissent une
  trace (`meta.tomb`) ; deux appareils se fusionnent sans se marcher dessus.
- **Page claude.ai** : `user.canEdit()` décide auteur / visiteur ; l’auteur republie la page avec l’état
  intégré (`#ac-public`), automatiquement après deux minutes de calme ou en quittant la page.
- **Site hébergé** : `donnees/site.json` (sommaire, révision, images) + `donnees/archives.json`.
  `?auteur` rend le site modifiable sur l’appareil de l’auteur ; « Télécharger les données (.zip) »
  ou « Relier un dépôt GitHub » (jeton fine‑grained, Contents : Read and write — il reste dans le
  navigateur et ne part que vers api.github.com) publie en un seul commit.

## Structure

```
src/
  App.tsx                 scènes, démarrage (mode, rôle, publication), ambiances
  state/model.ts          types et réparation des données
  state/seed.ts           tout le contenu livré (matériaux, matrices, dossiers 003/004, théories, carnet…)
  state/store.ts          magasin, fusion, tombes, persistance
  state/derive.ts         domaines, classifications, tabous, Éclats et paliers
  state/rapport.ts        rapport MJ (texte, PDF)
  public/                 rôle (local / artifact / hosted), publication claude.ai, site hébergé, zip
  components/             cadre, HUD, panneaux, recherche, diagrammes de matrice, particules, croquis
  scenes/                 les 17 lieux
  audio/                  sons de synthèse, musique « Les Dunes au crépuscule », fichier perso
tools/build-single.mjs    construction en un fichier
tests/test_site.py        tests d’interaction
```

Polices : Cormorant Garamond, Marcellus, EB Garamond, Nanum Pen Script (avant l’accident),
Architects Daughter, Special Elite (après), Cutive Mono — chargées depuis Google Fonts, avec
repli sur les polices du système.
