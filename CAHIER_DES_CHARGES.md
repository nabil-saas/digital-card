# Cahier des charges — Landing page et démo SaaS fidélité

Version du 22 octobre 2026 — à lire en entier avant de commencer.

## 1. Contexte et consignes

Tu dois produire la maquette HTML cliquable d'un SaaS de cartes de fidélité digitales : une landing page de présentation et un compte démo commerçant navigable, sans backend.

**Le produit en une phrase.** Les commerces de proximité d'Afrique de l'Ouest (Sénégal, Côte d'Ivoire en priorité) créent une carte de fidélité que leurs clients ajoutent dans Google Wallet, Apple Wallet ou en carte web, sans installer d'application. Le staff scanne la carte en caisse pour attribuer un tampon ou des points.

**Périmètre fonctionnel du produit (à respecter dans tous les textes) :**

- Deux types de cartes : tampons (1 passage = 1 tampon) et points (selon le montant dépensé, dans la devise de l'établissement).
- Récompenses par paliers, définies par le commerçant.
- Trois supports côté client : Google Wallet (prioritaire), Apple Wallet, carte web (PWA) pour les téléphones sans Wallet.
- Inscription du client par QR code ou puce NFC sur une carte physique posée au comptoir.
- Campagnes de notifications push et relances automatiques.
- Plusieurs établissements sur un même compte (multi-gérants, petites chaînes).
- **Aucun paiement** dans le produit : ni encaissement, ni lien vers Wave ou Orange Money. Ne jamais en montrer.

**Consignes de production :**

1. Langue : français. Devise : le produit est multi-devise (chaque établissement choisit la sienne : EUR, XOF, MAD…), mais la maquette affiche l'euro partout pour l'instant. Formate tous les montants avec Intl.NumberFormat à partir d'une seule configuration (devise: 'EUR', locale: 'fr-FR'), pour qu'un changement de devise se fasse en un seul endroit (exemple : 12 500 €).
2. Nom et logo : pas encore définis. Utilise le placeholder `[NOM]` dans les textes et un logo provisoire (un carré arrondi jaune avec une lettre). Centralise le nom dans une seule variable JS pour le remplacer facilement.
3. Livrer deux fichiers autonomes : `index.html` (landing) et `demo.html` (compte démo). CSS et JS inline, aucune dépendance obligatoire hors polices et icônes en CDN.
4. Le bouton « Essayer la démo » de la landing ouvre `demo.html` directement, sans formulaire de connexion.
5. Toutes les données sont fictives et codées en dur dans un objet JS (voir section 6). Les actions (envoi de campagne, scan, création de carte) simulent un succès avec un toast.

## 2. Direction artistique

Style épuré et professionnel à la Apple, avec la rigueur de [Lodgify](https://www.lodgify.com/) : beaucoup de blanc, de grands titres, des captures produit mises en scène, et un jaune franc utilisé avec parcimonie pour attirer l'œil.

**Couleurs (à déclarer en variables CSS) :**

| Rôle | Valeur | Usage |
| --- | --- | --- |
| Jaune principal | #FFF75C, soit rgb(255, 247, 92) | Boutons principaux, surlignages, badges actifs, accents d'illustration |
| Jaune clair | #FFFCD6 | Fonds de sections alternées, états survolés |
| Texte principal | #1D1D1F | Titres et texte courant |
| Texte secondaire | #6E6E73 | Sous-titres, légendes |
| Fond page | #FFFFFF | Fond général |
| Fond gris | #F5F5F7 | Cartes, sections alternées, fond du back-office |
| Bordures | #E5E5EA | Séparateurs fins (1 px) |
| Succès / alerte / erreur | #34C759 / #FF9F0A / #FF3B30 | Statuts uniquement |

**Règle d'accessibilité impérative :** le jaune #FFF75C est très clair. Il ne sert jamais de couleur de texte sur fond blanc ou gris clair (illisible). Il s'utilise en fond, toujours avec un texte #1D1D1F dessus. Sur fond blanc, un bouton jaune garde un contour de 1 px #1D1D1F pour rester visible. Le jaune peut en revanche servir de couleur de texte ou d'accent sur les sections à fond foncé #1D1D1F (hero alterné, appel final, pied de page), où il ressort fortement.

**Typographie :** `-apple-system, BlinkMacSystemFont, "Inter", sans-serif` (Inter via Google Fonts en secours). Titres hero 56–64 px graisse 700, interlignage serré ; titres de section 40 px ; texte courant 17 px ; légendes 13–14 px. Sur mobile, hero à 36–40 px.

**Composants :**

- Boutons : hauteur 48 px, rayon 980 px (pilule). Primaire = fond jaune et texte foncé. Secondaire = contour 1 px foncé, fond transparent.
- Cartes : fond blanc ou #F5F5F7, rayon 20 px, aucune ombre lourde (au plus une ombre très diffuse sur les maquettes de téléphone).
- Espacement : sections de 120 px de hauteur de marge en desktop, 72 px en mobile ; largeur de contenu max 1200 px.
- Icônes : un seul jeu en trait fin (Lucide ou Tabler via CDN), 20–24 px.
- Animations : apparition douce au scroll (fondu + 16 px de translation, 400 ms), aucune animation clignotante.
- Responsive obligatoire : 375 px (mobile), 768 px (tablette), 1280 px et plus (desktop).

## 3. Landing page (index.html)

Une page unique en 12 sections, inspirée de la clarté pédagogique de [Waly](https://waly.fr/) et de la démonstration produit de [Fidelix](https://fidelix.ma/), adaptée au marché ouest-africain.

1. **Barre de navigation** fixe, fond blanc translucide avec flou au scroll. Logo à gauche ; liens « Fonctionnalités », « Comment ça marche », « Calculateur », « Tarifs » ; à droite « Se connecter » (lien texte) et « Essayer la démo » (bouton jaune). Menu burger en mobile.
2. **Hero.** Titre : « La carte de fidélité digitale qui fait revenir vos clients ». Sous-titre : vos clients l'ajoutent en un scan dans leur téléphone, sans application ; vous les récompensez à chaque passage. Deux boutons : « Essayer la démo » (jaune) et « Voir les tarifs » (secondaire). Trois mentions à cocher : sans application, prête en 5 minutes, sans engagement. À droite (dessous en mobile) : un téléphone contenant une pile de 3 cartes Wallet de commerces fictifs qui défilent doucement (un salon de coiffure à tampons, un restaurant à points, une boutique à points).
3. **Bande de confiance** : « Ils nous font confiance » avec 6 logos fictifs en gris qui défilent en boucle.
4. **Avant / après.** Deux colonnes : « Sans \[NOM\] » (offres identiques pour tous, clients oubliés après une visite, aucune idée de qui revient) et « Avec \[NOM\] » (meilleurs clients reconnus, relances automatiques, fréquence de visite visible).
5. **Comment ça marche** en 4 étapes numérotées, avec une mini-illustration chacune : créez votre carte ; vos clients scannent le QR code ou approchent leur téléphone de la carte NFC ; vous scannez en caisse ; ils reviennent chercher leur récompense.
6. **Fonctionnalités** en onglets (style Lodgify : un texte à gauche, une capture produit à droite) regroupés en trois familles :
   - Pour vos clients : carte dans Google Wallet, Apple Wallet ou en carte web ; carte à vos couleurs ; menu de récompenses par paliers ; notification à proximité (iPhone).
   - Au comptoir : scan en caisse illimité même sans internet ; accès employés limités et révocables ; formation de vos équipes ; plusieurs établissements sur un même compte.
   - Pour qu'ils reviennent : relances automatiques ; campagnes de notifications ; parrainage ; demande d'avis Google après une visite ; statistiques en temps réel ; conseiller IA.
7. **Pour quels commerces** : grille de 8 cartes cliquables (restaurant, maquis, salon de coiffure, institut de beauté, boulangerie-pâtisserie, pressing, boutique, lavage auto). Au clic, un encart montre un exemple chiffré en euros : ticket moyen, récompense, coût de la récompense.
8. **Calculateur** interactif à curseurs : clients par jour (30), panier moyen (15 €), jours d'ouverture par mois (26), gain de fréquentation (10 %). Résultat en grand : chiffre d'affaires additionnel par mois et par an, en euros. Mention « estimation indicative ».
9. **Chiffres clés** : 4 statistiques sur la rétention (fidéliser coûte 5 fois moins cher que conquérir, etc.), chacune avec sa source en petit.
10. **Témoignages** : carrousel de 3 cartes. Texte et nom en placeholders clairement marqués `[Témoignage à remplacer]` — ne jamais inventer de vrais avis.
11. **Tarifs** : interrupteur mensuel / annuel (−20 %). Deux offres : « Découverte » (gratuit jusqu'à 30 clients) et « Pro » (prix `[À DÉFINIR]` € par mois et par établissement, tout inclus : clients illimités, notifications illimitées, toutes les fonctionnalités). Encart à part : carte NFC + QR code pour le comptoir, prix `[À DÉFINIR]`, paiement unique.
12. **FAQ en accordéon** (6 questions : faut-il une application, compatible avec tous les téléphones, comment le client ajoute la carte, et sans internet, combien d'établissements, mes données) puis **appel final** sur fond jaune clair et **pied de page** (liens, mentions légales, réseaux sociaux, sélecteur de langue FR / EN et sélecteur de devise EUR / XOF / MAD, réglé sur EUR par défaut).

## 4. Compte démo : structure et navigation (demo.html)

Une application monopage : chaque section s'affiche sans rechargement (routage par ancre `#dashboard`, `#clients`, etc.), et tout l'écran se recalcule quand on change d'établissement.

**Bandeau démo** fin et permanent en haut : « Vous êtes sur le compte de démonstration · Données fictives » avec un bouton « Créer mon compte » (jaune).

**Desktop (≥ 1024 px) : barre latérale gauche de 260 px**, fond #F5F5F7 :

- En haut : le **sélecteur d'établissement** (voir ci-dessous).
- Navigation : Tableau de bord, Clients, Campagnes, Automatisations, Mes cartes. Élément actif sur fond blanc avec une pastille jaune à gauche.
- En bas : Paramètres (inactif dans la démo, toast « Bientôt disponible »), profil du gérant fictif (avatar, nom, rôle « Propriétaire »).

**Mobile et tablette (< 1024 px) :** la barre latérale disparaît.

- En haut : le sélecteur d'établissement en version compacte (nom + chevron).
- En bas : une barre d'onglets fixe à 5 positions : Accueil, Clients, **Scanner** (au centre, bouton rond jaune de 64 px qui dépasse de la barre), Campagnes, Cartes. Automatisations est accessible depuis Campagnes.
- Le bouton **Scanner** n'existe qu'à ces tailles d'écran. En desktop, il est masqué (`display:none` au-dessus de 1024 px) ; à la place, un encart discret du tableau de bord indique « Le scan se fait depuis votre téléphone ou votre tablette » avec un QR code vers la démo.

**Sélecteur d'établissement (fonction clé, multi-gérants) :**

- Un bouton affiche le logo, le nom et la ville de l'établissement actif. Au clic : une liste déroulante (une feuille qui monte du bas en mobile) avec un champ de recherche, la liste des établissements (logo, nom, ville, nombre de clients), une option « Tous les établissements » (vue consolidée) et un lien « + Ajouter un établissement ».
- Changer d'établissement met à jour **toutes** les vues : chiffres, clients, campagnes, cartes. Courte transition en fondu et toast « Vous êtes sur \[nom\] ».
- En vue « Tous les établissements », le tableau de bord additionne les chiffres, et une colonne « Établissement » apparaît dans la liste des clients et des campagnes.
- Le dernier établissement choisi est mémorisé (localStorage, avec try/catch).

## 5. Écrans du compte démo

Cinq écrans, tous filtrés par l'établissement actif ; chaque action simule un succès sans backend.

### 5.1 Tableau de bord

- **4 indicateurs** en haut, avec variation sur le mois précédent : clients inscrits, passages ce mois, récompenses distribuées, taux de retour à 30 jours.
- **Graphique des passages** sur 30 jours (courbe, Chart.js via CDN), avec un sélecteur 7 j / 30 j / 90 j.
- **Répartition des supports** : Google Wallet, Apple Wallet, carte web (barres horizontales ou anneau).
- **Derniers passages** : les 6 derniers scans (client, heure, + tampon ou + points, employé).
- **Clients à relancer** : absents depuis plus de 30 jours, avec un bouton « Relancer » qui ouvre une campagne pré-remplie.
- **Conseiller IA** : une carte avec 3 suggestions de la semaine (exemple : « 42 clients sont à 1 tampon de leur récompense : envoyez-leur un rappel »), chacune avec un bouton d'action.

### 5.2 Clients (base de données)

- **Tableau** de toutes les cartes créées : nom, téléphone, type de carte, support (icône Google / Apple / Web), solde (tampons ou points), dernier passage, date d'inscription, statut (actif, inactif, récompense disponible).
- **Recherche** par nom ou téléphone, **filtres** (type de carte, support, statut, période d'inscription), **tri** sur chaque colonne, pagination de 20 lignes.
- Bouton **« Exporter en CSV »** (génère réellement un fichier CSV des données fictives).
- **Fiche client** au clic sur une ligne (panneau latéral en desktop, plein écran en mobile) : coordonnées, consentement marketing, solde et progression vers le prochain palier, historique des transactions (date, type, quantité, employé), actions « Ajuster le solde », « Envoyer un message », « Désactiver la carte ».
- En mobile, le tableau devient une liste de cartes empilées.

### 5.3 Scanner (mobile et tablette uniquement)

1. Ouverture plein écran sur fond noir, faux flux caméra avec un cadre de visée animé et une ligne de scan qui balaie.
2. Bouton « Simuler un scan » (pour la démo) : choisit un client fictif au hasard et affiche sa fiche courte (nom, solde, prochaine récompense).
3. Selon le type de carte :
   - **Tampons** : un gros bouton « + 1 tampon ».
   - **Points** : un pavé numérique pour saisir le montant dans la devise de l'établissement (euros dans la démo) ; les points calculés s'affichent en direct avant validation.
4. Si une récompense est disponible : bannière jaune « Récompense disponible » et bouton « Utiliser la récompense ».
5. Confirmation : coche animée, nouveau solde, retour automatique au scanner après 2 secondes.
6. Secours : lien « Rechercher par téléphone » en bas de l'écran.
7. Interrupteur « Mode hors ligne » pour la démo : les scans s'empilent avec un badge « 3 en attente de synchronisation », puis se synchronisent quand on le désactive.

### 5.4 Campagnes et automatisations

**Campagnes** (notifications push) :

- Liste des campagnes envoyées et programmées : titre, date, audience, nombre de destinataires, statut (programmée, envoyée, brouillon).
- Bouton **« Nouvelle campagne »** qui ouvre un assistant en 4 étapes :
  1. Message (titre court + texte, compteur de caractères).
  2. Audience : tous les clients, inactifs depuis 30 jours, proches d'une récompense, nouveaux clients, ou sélection manuelle ; estimation du nombre de destinataires.
  3. Canal : notification Wallet (par défaut), WhatsApp, SMS.
  4. Envoi immédiat ou programmé (date et heure).
- **Aperçu en direct** à droite : la notification sur un écran verrouillé de téléphone, avec un bouton pour basculer entre Android et iPhone.
- Mention discrète : « 1 campagne par jour maximum pour préserver vos clients ».

**Automatisations** : une liste de règles avec un interrupteur chacune, et un message modifiable :

- Bienvenue à l'inscription.
- Relance d'un client absent depuis X jours (X réglable : 15, 30, 60).
- Récompense disponible et non utilisée depuis 7 jours.
- Anniversaire du client.
- Demande d'avis Google après la 3e visite, **sans contrepartie** (les politiques de Google interdisent de récompenser un avis).
- Points bientôt expirés.

Chaque règle affiche ses résultats sur 30 jours (envois, clients revenus).

### 5.5 Mes cartes

- **Grille des programmes** de tous les établissements du compte : aperçu de la carte, nom de l'établissement, type (tampons ou points), nombre de cartes actives, statut. Le programme de l'établissement actif apparaît en premier.
- Bouton **« Créer une carte »** : un éditeur en 2 colonnes, avec les réglages à gauche et l'aperçu en direct à droite (onglets Google Wallet / Apple Wallet / carte web).
  - Le détail de l'éditeur (personnalisation et paliers de récompenses selon le type de carte) est décrit juste après cette liste.
- **Supports physiques** : liste des cartes NFC et QR (code, emplacement, établissement, nombre de scans, statut non activée / active / désactivée), bouton « Activer une carte » (saisie du code imprimé) et bouton « Télécharger le QR code » (SVG).
- Bouton **« + Ajouter un établissement »** : formulaire simple (nom, activité, ville, adresse, devise, logo, gérant) qui l'ajoute au sélecteur.

#### Éditeur de carte : déroulé

L'éditeur s'ouvre en plein écran avec 5 étapes en haut (cliquables dans le désordre une fois la première validée) et l'aperçu en direct à droite, qui reste visible à chaque étape.

1. **Type** : deux grandes tuiles au choix, « Carte à tampons » et « Carte à points », chacune avec une mini-illustration et une phrase d'explication. Ce choix conditionne les étapes Design et Récompenses.
2. **Design** : la personnalisation visuelle.
3. **Récompenses** : les paliers, différents selon le type.
4. **Informations** : ce qui figure au dos de la carte.
5. **Publication** : récapitulatif, puis bouton « Publier la carte » (toast de succès et retour à la grille).

Un bouton « Enregistrer en brouillon » reste disponible à toutes les étapes.

#### Éditeur de carte : personnalisation

- **Modèles de départ** par activité (coiffure, restaurant, boulangerie, boutique, beauté, pressing) qui pré-remplissent couleurs, icône et paliers. Option « Partir de zéro ».
- **Identité** : nom de l'établissement affiché sur la carte, nom du programme (exemple : « Club Belle Allure »), logo (téléversement avec recadrage carré).
- **Couleurs** : fond de la carte, texte, libellés, avec un sélecteur et 8 couleurs suggérées. Alerte en orange si le contraste texte / fond est insuffisant.
- **Image de bannière** (facultative) : affichée sous le logo, au format conseillé indiqué.
- **Spécifique aux tampons** : icône du tampon choisie dans une bibliothèque de 12 icônes (café, ciseaux, croissant, étoile, cœur, goutte, etc.) ou téléversée ; style de la case vide (contour, pointillés) et de la case remplie.
- **Spécifique aux points** : nom de l'unité (« points » par défaut, personnalisable : « étoiles », « cauris »…), affichage d'une barre de progression vers la prochaine récompense (oui / non).
- **Code client** : QR code (par défaut) ou code-barres.
- **Aperçu** : onglets Google Wallet / Apple Wallet / carte web, interrupteur recto / verso, et un curseur « Simuler un client » qui fait varier le solde (de 0 au dernier palier) pour voir la carte se remplir.

#### Éditeur de carte : paliers de récompenses selon le type

L'étape Récompenses affiche une interface différente selon le type choisi à l'étape 1.

| Réglage | Carte à tampons | Carte à points |
| --- | --- | --- |
| Règle de gain | 1 tampon par passage | X points par euro dépensé, arrondi à l'inférieur, avec un montant minimum d'achat |
| Structure | Une carte de N cases (5 à 20), les paliers sont placés sur des cases précises | Un catalogue de récompenses, chacune avec son coût en points |
| Exemple | Case 5 : −10 % ; case 10 : 1 brushing offert | 500 pts : boisson offerte ; 1 500 pts : dessert offert ; 3 000 pts : repas offert |
| Interface | Un rail visuel des N cases ; on clique sur une case pour y poser une récompense | Une liste de récompenses triée par coût, avec « + Ajouter une récompense » |
| Après utilisation | La carte repart à zéro après le dernier palier, l'excédent est reporté | Les points sont déduits, le reste du solde est conservé |
| Options | Tampon de bienvenue offert ; 1 tampon maximum par période (1 h, 1 jour) | Points de bienvenue ; points bonus d'anniversaire ; expiration des points (aucune, 6 ou 12 mois) |

**Chaque récompense se définit par :** un libellé, un type (produit offert, remise en %, remise en montant), une durée de validité après déblocage (7, 30, 90 jours ou illimitée) et, pour les points uniquement, une limite facultative (« 1 fois par client »).

**Contrôles de saisie :**

- Au moins une récompense est obligatoire pour publier.
- Tampons : deux récompenses ne peuvent pas être sur la même case ; le dernier palier doit être sur la dernière case.
- Points : deux récompenses ne peuvent pas avoir le même coût ; les coûts sont des nombres entiers positifs.
- Erreurs affichées sous le champ concerné, en rouge, en une phrase.

**Modifier une carte existante :** même éditeur, avec un bandeau d'avertissement « Les modifications s'appliquent aux 60 cartes déjà distribuées. Les soldes de vos clients sont conservés. » Changer le type de carte est impossible une fois publiée : le bouton est grisé avec une info-bulle qui explique pourquoi.

## 6. Données fictives, contraintes techniques et livrables

La démo doit sembler vivante dès l'ouverture : trois établissements réalistes, environ 150 clients et 90 jours d'historique, générés une fois dans un objet JS.

**Compte démo :** gérante fictive « Aïssatou Ndiaye », rôle Propriétaire, qui gère 3 établissements.

| Établissement | Activité | Ville | Type de carte | Règle | Clients |
| --- | --- | --- | --- | --- | --- |
| Salon Belle Allure | Salon de coiffure | Dakar | Tampons | 8 passages = 1 brushing offert | 60 |
| Chez Tantie Rose | Restaurant | Abidjan | Points | 1 point par euro ; paliers à 500, 1 500 et 3 000 points | 55 |
| Pâtisserie Le Baobab | Boulangerie-pâtisserie | Dakar | Tampons | 10 passages = 1 gâteau offert | 35 |

**Clients :** prénoms et noms variés de la région, téléphones au format local fictif (+221 77 000 00 00, +225 07 00 00 00 00), répartition des supports d'environ 65 % Google Wallet, 20 % carte web, 15 % Apple Wallet. Environ 20 % d'inactifs depuis plus de 30 jours, et quelques clients avec une récompense disponible.

**Historique :** transactions sur 90 jours avec un pic le week-end, 4 employés fictifs, 5 campagnes passées, 1 programmée, 4 automatisations actives sur 6.

**Contraintes techniques :**

- HTML, CSS et JavaScript natifs, sans framework ni étape de compilation.
- CDN autorisés : Chart.js, un jeu d'icônes en trait fin (Lucide ou Tabler), Google Fonts (Inter).
- Aucun appel réseau autre que ces CDN ; aucune vraie donnée personnelle.
- Les images de produit (téléphones, cartes Wallet) sont dessinées en HTML et CSS, pas en images importées.
- Accessibilité : contrastes conformes WCAG AA, navigation au clavier, attributs `aria` sur les boutons-icônes.
- Chargement rapide : chaque fichier reste sous 500 Ko.

**Livrables et critères d'acceptation :**

- [ ] `index.html` : les 12 sections de la landing, responsive à 375, 768 et 1280 px.
- [ ] `demo.html` : les 5 écrans fonctionnels, navigation latérale en desktop et barre d'onglets en mobile.
- [ ] Le sélecteur d'établissement met à jour tous les écrans, y compris la vue « Tous les établissements ».
- [ ] Le bouton Scanner n'apparaît qu'en dessous de 1024 px.
- [ ] L'export CSV de la base clients produit un vrai fichier.
- [ ] Les éditeurs (campagne, carte) affichent un aperçu qui suit la saisie en direct.
- [ ] Le nom `[NOM]` et le logo provisoire sont centralisés et remplaçables en un seul endroit.
- [ ] Aucune mention de paiement, d'encaissement ou de mobile money nulle part, et tous les montants passent par la configuration de devise (euro par défaut).
