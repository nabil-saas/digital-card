# Visuels de la maquette

Tout ce qui est image vit ici. Dans la quasi-totalité des cas, **remplacer un
fichier en gardant son nom suffit** : il n'y a rien à modifier dans le code.

```
assets/
├── marque/          le logo de votre entreprise
├── commerces/       les photos de la section « Pour quels commerces »
└── logos-clients/   les logos de la bande « Ils nous font confiance »
```

---

## 1. Votre logo — `marque/`

| Fichier | Où il apparaît |
| --- | --- |
| `logo.svg` | barre de navigation de la landing (fond clair) |
| `logo-sombre.svg` | pied de page de la landing, bandeau du compte démo (fond foncé) |

**Pour le remplacer :** déposez vos deux fichiers sous ces noms exacts. Ils
s'afficheront partout, dans `index.html` comme dans `demo.html`.

- Format conseillé : **SVG**. Sinon PNG à deux fois la taille d'affichage
  (le logo est rendu à 34 px de haut dans la nav, 40 px dans le pied de page).
- Prévoyez bien **deux versions** : la version sombre doit rester lisible sur
  le fond noir du pied de page.
- Le fichier peut contenir le symbole seul ou le symbole + le nom, au choix :
  il remplace l'ensemble du bloc logo.

**Si les fichiers sont absents ou illisibles**, la maquette revient d'elle-même
au carré jaune avec une lettre — rien ne casse. Vous pouvez aussi forcer ce
repli en vidant les champs `logo` et `logoDark` en haut du script des deux
fichiers HTML.

---

## 2. Photos des commerces — `commerces/`

Huit photos, une par type d'activité du carrousel :

```
restaurant.jpg          maquis.jpg            salon-de-coiffure.jpg
institut-de-beaute.jpg  boulangerie.jpg       pressing.jpg
boutique.jpg            lavage-auto.jpg
```

**Pour en changer une :** écrasez le fichier en gardant son nom.

- Cadrage : **4/3 paysage**, environ **1000 px de large**.
- Les photos sont recadrées automatiquement et recouvertes d'un dégradé sombre
  en bas (le nom de l'activité s'y inscrit). Évitez donc les visuels dont le
  sujet est collé au bord inférieur.
- Poids : visez **moins de 250 Ko** par image.

Les photos livrées proviennent d'Unsplash (licence libre, usage commercial
autorisé, sans attribution obligatoire). Ce sont des illustrations
temporaires : remplacez-les par vos propres commerces dès que possible,
c'est ce qui rendra la page crédible.

**Pour ajouter ou retirer une activité**, modifiez la liste `BIZ` dans
`index.html` (recherchez `const BIZ`). Chaque entrée indique son nom de
fichier, son icône, son ticket moyen et sa récompense.

---

## 3. Logos partenaires — `logos-clients/`

Six logos défilent en boucle dans la bande « Ils nous font confiance ».

```
01-salon-eclat.svg      02-le-petit-maquis.svg   03-boutique-soleil.svg
04-pain-et-cie.svg      05-studio-teranga.svg    06-auto-net.svg
```

Ceux livrés sont des **filigranes de remplacement**, pas de vraies marques.

**Pour mettre vos partenaires :** déposez leurs SVG dans ce dossier, puis
ouvrez `index.html` et mettez à jour la liste `TRUST` (recherchez
`const TRUST`) avec les noms et les noms de fichiers.

- Format : **SVG monochrome**. Si le SVG utilise `fill="currentColor"`, il
  prend automatiquement le gris de la bande et s'éclaircit au survol.
  Un SVG avec des couleurs figées s'affichera tel quel, ce qui est acceptable
  mais moins homogène.
- Hauteur de rendu : **30 px**, largeur libre.
- Un PNG fonctionne aussi, mais il n'héritera pas de la teinte grise.

Si un fichier manque, la maquette affiche simplement le nom du partenaire en
toutes lettres — la bande reste présentable.

---

## Attention au chargement local

Les logos partenaires sont lus par le navigateur via `fetch`. Si vous ouvrez
`index.html` par un double-clic (adresse `file://`), le navigateur bloque ces
lectures et vous verrez les noms en texte au lieu des logos. **Les photos et
votre logo, eux, s'affichent normalement.**

Pour tout voir correctement en local, servez le dossier par HTTP. Depuis le
dossier du projet :

```
python3 -m http.server 4173
```

puis ouvrez `http://localhost:4173/`. Une fois le site en ligne sur un vrai
hébergement, la question ne se pose plus.
