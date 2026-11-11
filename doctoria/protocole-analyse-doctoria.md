# Protocole d'analyse de l'enquête DoctorIA, sur le modèle de l'étude Anthropic

Version 0.1, 11 novembre 2026. Document de travail, à valider par l'équipe DoctorIA avant toute analyse confirmatoire.

## 1. Objet et sources

Ce document propose une méthode pour analyser les réponses à l'enquête DoctorIA en reprenant, autant que les données le permettent, la logique de l'étude d'Anthropic sur l'usage de Claude par les chercheurs.

Deux sources ont été lues :

- **[Anthropic 2026]** Hermle, Jones, Althoff et al., *AI for scientific discovery: how researchers use Claude*, The Anthropic Institute, 5 novembre 2026. https://www.anthropic.com/research/how-researchers-use-claude. Tous les chiffres attribués à l'étude ci-dessous viennent de ce rapport. Son annexe (détail du modèle, des classifieurs et des pondérations) n'a pas été consultée.
- **[DoctorIA, export]** Fichier `doctoria-responses_1.csv`, 297 lignes, 43 colonnes, réponses du 12 juin au 10 novembre 2026. Tous les chiffres DoctorIA ci-dessous sont calculés sur ce fichier.

Limite à signaler : le site https://doctoria.fr/ n'était pas accessible depuis l'environnement de travail (domaine hors de la liste réseau autorisée). Le libellé exact des questions, les échelles et le cadre de diffusion sont donc déduits de l'export. Les points à confirmer avec le questionnaire d'origine sont marqués **[à confirmer]**.

## 2. Ce que fait l'étude Anthropic

| Bloc | Méthode | Résultat principal cité |
|---|---|---|
| A. Mesure | Un classifieur LLM lit chaque session et lui attribue des étiquettes fermées (discipline, sous-discipline, tâche) selon la taxonomie SciNet (34 disciplines, 318 sous-disciplines, 7 262 tâches). Seules les étiquettes sont conservées. Résultats agrégés, cellules sous un seuil minimal de comptes masquées. | 207 049 sessions, du 2 août au 30 septembre 2026 |
| B. Usage par discipline | Part des sessions d'une discipline comparée à sa part dans la population mondiale de chercheurs | Usage relatif élevé en sciences formelles, faible en santé et sciences de laboratoire. Corrélation log-log 0,79 (Claude), 0,62 (Claude Code) |
| C. Usage par tâche | Part des sessions par catégorie de tâche (8 catégories) comparée à la part du temps de recherche consacrée à cette catégorie (estimation SciNet). Le rapport des deux est le « ratio d'usage ». | Analyse de données 33,7 % des sessions pour 27,6 % du temps. Écriture 32,0 % pour 16,0 %. Recueil de données 11,5 % pour 28,6 %. Idéation 4,2 % pour 7,1 % |
| D. Enquête | 528 chercheurs, surtout sciences de la vie et santé, utilisateurs actifs. Niveau d'usage en 5 paliers (aucun, assistif, partagé, délégué, autonome) et importance de chaque catégorie (100 points à répartir) | Les tâches jugées les plus importantes (idéation, recueil de données) sont les moins confiées à l'IA |
| E. Outils spécialisés | Comparaison Claude Science, Claude, Claude Code sur durée, niveau doctoral, autonomie | Idéation à 8 % des sessions sur Claude Science, environ le double de Claude |
| F. Productions | Part des sessions produisant un artefact écrit ou technique, par discipline | Écrit dominant en SHS, technique dominant en sciences formelles et naturelles |
| G. Capacité théorique de l'IA | Comparaisons par paires faites par un LLM, agrégées par un modèle de Bradley-Terry, puis moyenne par tâche. Mise en relation avec le ratio d'usage et avec des caractéristiques de tâche (adéquation à l'apprentissage par renforcement, caractère cognitif, physique, interpersonnel, contraintes réglementaires) | Les 20 % de tâches les mieux notées reçoivent 2 à 4 fois l'usage attendu. Corrélations avec le score de capacité : 0,78 (indice RL), 0,69 (cognitif), −0,57 (physique), −0,31 (interpersonnel), −0,38 (réglementaire) |
| H. Autonomie | Score d'autonomie moyen par sous-discipline, corrélé à la capacité théorique | L'usage est plus autonome là où la capacité théorique est plus élevée |
| I. Scénarios | « Part IA » du temps de recherche, puis « accélération » via une fonction de production d'idées (Jones 2026), avec un coût IA de 30 $/h contre 95 $/h pour un chercheur | Scénario actuel : 27 à 52 % du temps, accélération de 1,35x à 2,02x. Scénarios d'automatisation : jusqu'à 15 à 16x sans goulot physique, 3 à 4x en sciences de paillasse |
| J. Anticipations | Horizon auquel l'IA égalerait les meilleurs chercheurs, par catégorie de tâche | Environ 40 % attendent des projets de recherche complets menés par l'IA d'ici 2030 |

L'étude précise elle-même que ses scénarios sont illustratifs et non des prévisions, et que son enquête porte sur des répondants plus utilisateurs que la moyenne.

## 3. Ce que contient l'export DoctorIA

### 3.1 Structure

| Bloc | Variables | Type |
|---|---|---|
| Profil | `q2_discipline` (section CNU, 46 modalités), `q3_ecole_doctorate` (8 écoles doctorales), `q4_annee_inscription`, `q5_financement`, `q6_temps_these` | Choix unique |
| Rapport à l'IA | `q7_usage_avant`, `q8_comprehension`, `q8_evaluation`, `q8_limites` (1 à 4), `q9_inspirations`, `q10_formations` | Mixte |
| Usage | `q11_utilisateur_actuel`, `q12_frequence`, `q12bis_non_usage` | Filtre |
| Étapes, tâches, outils | `q14_etapes` (6 étapes de la thèse), `q15_taches` (12 tâches, intensité 0 à 4), `q16_outils` (10 familles d'outils, 0 à 4), `q17_roles` | Multi-réponses et grilles |
| Vérification et données | `q18_verification`, `q18_type_verification`, `q19_verification_utile`, `q20_donnees_sensibles` | Mixte |
| Perceptions | `q21_avantages` (6 items, 0 à 4), `q22_risques` (6 items, 0 à 4) | Grilles |
| Cadre institutionnel | `q13_amenagements`, `q23_mention_these`, `q24_cadre_reglementaire`, `q25_encadrement_usage`, `q26_discute_csi` | Mixte |
| Formation | `q27_ressources`, `q28_interet_formation`, `q28_themes_souhaites`, `q29_formats` | Multi-réponses |
| Texte libre | `q30_verbatim` (53 réponses, médiane 416 caractères), 4 colonnes `*_autre_libelles` | Texte |

### 3.2 Points de qualité relevés dans le fichier

1. **Lignes de test.** Les identifiants 3, 4 et 5 portent des verbatims du type « Test de soumission automatisée ». Après exclusion : **294 répondants, dont 253 utilisateurs et 41 non-utilisateurs**.
2. **Deux schémas de clés** pour `q15`, `q16`, `q21`, `q22` : libellés français (juin à début septembre, environ 174 lignes) puis codes (`writing`, `time_saved`, à partir de septembre, environ 123 lignes, dont les 15 réponses en anglais). Une table de correspondance est nécessaire, et un effet de version doit être testé.
3. **Variante de libellé.** Le libellé « intégrité scientifique » apparaît à côté de « intégrité académique ». Vérifier si le libellé a changé entre versions **[à confirmer]**.
4. **Colonnes vides.** `q1_genre` et `q1_tranche_age` ne contiennent aucune valeur. `q29_formats` n'a que 2 réponses.
5. **Réponses « Autre » mêlées aux modalités fermées**, dans les listes (`q9`, `q13`, `q14`, `q17`, `q18_type`, `q27`, `q28_themes`) et comme clés supplémentaires dans les grilles.
6. **Doublon de modalité** : « 70 Sciences de l'education » et « 70 Sciences de l'éducation ».
7. **Incohérence de filtre** : le filtre entre `q12` (utilisateurs) et `q12bis` (non-utilisateurs) n'est pas toujours respecté. Prévoir une règle de traitement.
8. **Modalités à clarifier** : `q24` contient 221 « Peut-être » ; `q25` contient une modalité « Encouragé » isolée à côté de « Recommandé » et « Suggéré » ; les étiquettes de l'échelle 0 à 4 ne figurent pas dans l'export **[à confirmer]**.
9. **Deux vagues de collecte** : juillet (132 réponses) et septembre (136). À traiter comme variable de contrôle.
10. **Effectifs par section CNU faibles** : sur 46 sections, 2 seulement dépassent 20 répondants et la majorité en compte moins de 6.

### 3.3 Aperçu descriptif provisoire

Calculé sur les 253 utilisateurs, clés harmonisées, sans pondération. Ces chiffres servent à vérifier la faisabilité du protocole, pas à conclure.

| Tâche (`q15`) | Intensité moyenne (0 à 4) | Part à 3 ou 4 |
|---|---|---|
| Reformulation, correction | 2,25 | 45 % |
| Traduction | 2,17 | 48 % |
| Revue de littérature | 1,69 | 25 % |
| Résumés, synthèses | 1,67 | 30 % |
| Traitement de données | 1,34 | 22 % |
| Rédaction | 1,31 | 16 % |
| Brainstorming | 1,25 | 15 % |
| Plans, brouillons, formatage | 1,21 | 22 % |
| Visualisations | 0,98 | 15 % |
| Supports de présentation | 0,86 | 9 % |
| Cartographie conceptuelle | 0,64 | 7 % |
| Conception d'enquête | 0,44 | 4 % |

Avantage le mieux noté : gain de temps (3,25, 79 % à 3 ou 4). Risque le mieux noté : dépendance technologique (2,86, 68 % à 3 ou 4), devant la sécurité des données (2,33) et les erreurs ou hallucinations (2,16).

Lecture prudente : le haut du classement (écriture, traduction) et le bas (conception d'enquête, soit le recueil de données) vont dans le même sens que le bloc C d'Anthropic. Le traitement de données, premier chez Anthropic, n'est ici qu'en milieu de tableau. Cet écart est une hypothèse à tester (section 6, H2), pas un résultat.

## 4. Ce qui est transposable et ce qui ne l'est pas

| Bloc Anthropic | Équivalent DoctorIA | Faisabilité | Donnée manquante |
|---|---|---|---|
| A. Mesure par classifieur | Codage fermé des verbatims et des réponses « Autre » | Oui | Aucune |
| B. Usage par discipline | Taux et intensité d'usage par école doctorale, rapportés aux inscrits | Oui, avec données externes | Effectifs de doctorants inscrits par école doctorale |
| C. Usage par tâche et temps | Part d'intensité par tâche (`q15`) et par étape (`q14`), rapportée au temps de thèse | Partielle | Répartition du temps de thèse par étape |
| D. Niveaux d'usage et importance | `q15` (fréquence) et `q17` (rôles) | Partielle | Importance perçue de chaque étape, niveau de délégation |
| E. Outils spécialisés | `q16` : agents généralistes contre outils spécialisés (bibliographie, codage, local) | Oui | Aucune |
| F. Productions | Profil « écrit » contre « technique » des tâches `q15`, par domaine | Oui | Aucune |
| G. Capacité théorique | Score de capacité sur les 12 tâches, par domaine | Oui, à construire | Scores à produire, ou scores SciNet si disponibles |
| H. Autonomie | Indice d'autonomie tiré de `q17` et `q18` | Partielle | Définition exacte des rôles **[à confirmer]** |
| I. Scénarios | « Part IA » du temps de thèse | Partielle, illustrative | Temps par étape. Paramètres du modèle en annexe Anthropic |
| J. Anticipations | Aucun | Non | Question absente du questionnaire |

DoctorIA couvre en revanche trois thèmes que l'étude Anthropic ne mesure pas et ne traite qu'en discussion : la vérification des sorties (`q18`, `q19`), les données sensibles (`q20`) et le cadre institutionnel (`q13`, `q23` à `q27`). Le protocole leur réserve un volet propre (section 5.8).

Différence de nature à garder en tête dans toute comparaison : Anthropic observe des sessions réelles sur un seul produit, à l'échelle mondiale. DoctorIA recueille des déclarations de doctorants, tous outils confondus, dans 8 écoles doctorales dont les libellés renvoient à Lille et aux Hauts-de-France. Les deux sources ne mesurent pas la même grandeur.

## 5. Protocole proposé

### 5.1 Étape 0 : gel du plan et gouvernance des données

- Rédiger et dater un plan d'analyse (ce document, complété) avant de produire les résultats confirmatoires. Séparer explicitement analyses confirmatoires (hypothèses de la section 6) et exploratoires.
- Reprendre le principe de confidentialité d'Anthropic : seules des étiquettes fermées sortent du texte libre, et les résultats ne sont publiés qu'en agrégat.
- **Seuil de diffusion : aucune cellule de moins de 10 répondants.** Conséquence : pas de résultat par section CNU, seulement par école doctorale ou par domaine.
- Les verbatims peuvent identifier leur auteur (discipline rare, sujet de thèse). Pas de citation sans paraphrase ou accord. Le fichier brut n'est pas versionné dans ce dépôt.
- **Traitement déjà réalisé, à régulariser.** Les chiffres descriptifs de la section 3 ont été calculés sur l'export dans une session Claude Code hébergée, donc par un LLM hébergé, avant que ce point soit vérifié. L'équipe DoctorIA doit confirmer que ce traitement est couvert par la base légale et par l'information donnée aux répondants, ou décider des suites (information des répondants, suppression des copies de travail). Aucun autre traitement de ce type tant que ce n'est pas tranché.
- Le seuil de diffusion vaut aussi pour ce document, versionné dans un dépôt public : il ne décrit aucune ligne individuelle, et la mention du périmètre géographique (section 4) est à valider par l'équipe avant fusion.
- Vérifier la base légale et l'information donnée aux répondants avant tout nouveau traitement par un LLM hébergé. Plusieurs répondants expriment eux-mêmes des réserves sur la confidentialité des outils en ligne : un modèle local, ou un service couvert par un accord de traitement de données, est cohérent avec ce qu'ils ont déclaré.

### 5.2 Étape 1 : préparation des données

1. Exclure les lignes de test (ids 3, 4, 5) et documenter la règle.
2. Harmoniser les clés des grilles vers un jeu de codes unique (table de correspondance libellé français vers code, à versionner).
3. Créer `version_questionnaire` (libellés ou codes), `vague` (juillet, septembre, autre) et `langue`.
4. Séparer modalités fermées et réponses « Autre » dans les multi-réponses. Les « Autre » passent à l'étape 6 (section 5.7).
5. Regrouper `q2_discipline` en domaines. Proposition, proche des regroupements d'Anthropic : sciences formelles (sections 25 à 27, 61), sciences physiques et ingénierie (28 à 37, 60, 62, 63), sciences de la vie et santé (42 à 58, 64 à 69, 74, 85 à 87, 90 à 92), sciences sociales (01 à 06, 16, 19, 20, 23, 24, 70, 71), arts et humanités (07 à 15, 17, 18, 21, 22, 72, 73, 76, 77). Toute modalité de l'export absente de cette liste est affectée explicitement et consignée dans le journal des décisions. À valider par l'équipe.
6. Construire les variables dérivées : ancienneté en thèse (en années universitaires, calculée à partir de `q4` et de la date de réponse, car la collecte chevauche les années 2025-2026 et 2026-2027), score de littératie (`q8`, après vérification de la cohérence interne par alpha de Cronbach ou oméga), nombre de tâches utilisées, nombre d'outils utilisés.
7. Produire un dictionnaire de données et un journal des décisions.

### 5.3 Étape 2 : représentativité et pondération

Équivalent du dénominateur « nombre de chercheurs par discipline » d'Anthropic.

- Obtenir auprès des écoles doctorales ou du collège doctoral les effectifs inscrits par école doctorale, année d'inscription et financement.
- Calculer le taux de réponse par école doctorale.
- Pondérer par calage sur marges (école doctorale, ancienneté, financement). Présenter tous les résultats en version brute et pondérée.
- Discuter l'auto-sélection : la part d'utilisateurs parmi les répondants (253 sur 294) ne peut pas être lue comme un taux d'adoption de la population. Anthropic fait la même réserve sur son enquête.

### 5.4 Étape 3 : usage par discipline (blocs B et F)

- Indicateurs par école doctorale et par domaine : part d'utilisateurs, fréquence (`q12`), intensité totale (somme des 12 items de `q15`), étendue (nombre de tâches à 1 ou plus).
- **Ratio d'usage disciplinaire** = part de l'école doctorale dans l'intensité totale déclarée, divisée par sa part dans les inscrits. Un ratio de 1 signifie un usage proportionnel à la taille.
- Profil des productions : indice « écrit » (rédaction, reformulation, traduction, résumés, supports) contre indice « technique » (traitement de données, visualisations, formatage LaTeX), par domaine, pour reproduire la figure 7 d'Anthropic.
- Intervalles de confiance par bootstrap (2 000 tirages). Avec 8 écoles doctorales, la corrélation taille contre usage est descriptive seulement.

### 5.5 Étape 4 : usage par tâche (blocs C et D)

**Correspondance avec les 8 catégories d'Anthropic** (proposition à valider) :

| Catégorie Anthropic | Tâches `q15` | Étape `q14` |
|---|---|---|
| Analyse de données | Traitement de données, visualisations | Analyse données |
| Écriture et communication | Rédaction, reformulation, traduction, formatage, supports de présentation | Rédaction, valorisation |
| Recueil de données | Conception d'enquête | Recueil données |
| Lecture et acquisition de connaissances | Revue de littérature, résumés | Exploration, cadre théorique |
| Analyse théorique | Cartographie conceptuelle | Cadre théorique |
| Idéation et hypothèses | Brainstorming | Exploration |
| Conception et développement | Non couvert (voir `q16`, assistants de codage) | Non couvert |
| Autre | Réponses « Autre » recodées | Réponses « Autre » recodées |

**Indicateurs.** L'échelle 0 à 4 est une fréquence déclarée, pas une part de sessions. Deux mesures complémentaires :

- Prévalence : part des utilisateurs à 3 ou 4 sur la tâche.
- Part d'intensité : somme des scores de la tâche divisée par la somme des scores de toutes les tâches. C'est l'analogue le plus proche d'une part de sessions.

**Ratio d'usage par catégorie** = part d'intensité de la catégorie, divisée par la part du temps de thèse consacrée à cette catégorie.

Le dénominateur n'existe pas dans DoctorIA. Deux options, à mener en parallèle :

- Option 1, immédiate : utiliser les parts de temps par catégorie de SciNet (https://www.anatomyofscience.com/), par discipline, après correspondance entre sections CNU et disciplines SciNet. Sous réserve que ces estimations soient accessibles et réutilisables. Elles portent sur des chercheurs, pas sur des doctorants.
- Option 2, à privilégier : un module complémentaire court adressé aux répondants ou à un nouvel échantillon (section 7).

Si aucune des deux n'est disponible, s'en tenir aux parts d'intensité et à leur comparaison qualitative avec la figure 3 d'Anthropic, sans calculer de ratio.

### 5.6 Étape 5 : capacité théorique et caractéristiques des tâches (blocs G et H)

Reproduction à échelle réduite de la mesure d'Anthropic.

1. **Unités à noter.** Les 12 tâches de `q15`, déclinées par domaine (5 domaines), soit 60 unités, chacune décrite en 2 à 4 étapes concrètes rédigées avec un doctorant du domaine. Exemple : « conception d'enquête en sciences de la vie » ne recouvre pas les mêmes gestes qu'en sociologie.
2. **Comparaisons par paires.** Un LLM reçoit deux unités et indique laquelle une IA actuelle réalise le mieux. Tirage aléatoire des paires, chaque unité vue au moins 30 fois, ordre de présentation inversé une fois sur deux, 3 passages indépendants.
3. **Agrégation** par modèle de Bradley-Terry, score converti en percentile.
4. **Caractéristiques notées séparément**, comme chez Anthropic : caractère cognitif, physique, interpersonnel ; facilité de vérification du résultat ; contraintes réglementaires (données personnelles, données de santé, secret).
5. **Validation humaine.** Deux évaluateurs notent indépendamment un sous-échantillon de 100 paires. Accord inter-juges (kappa) et accord avec le LLM (tau de Kendall) rapportés. En dessous d'un tau de 0,6, le score n'est pas utilisé en confirmatoire.
6. **Analyses.** Ratio d'usage ou part d'intensité par tercile de capacité (les quintiles d'Anthropic demandent plus d'unités) ; corrélation de Spearman entre score de capacité et intensité moyenne, sur les 60 unités ; même analyse avec chaque caractéristique de tâche.
7. **Autonomie.** Construire un indice ordinal à partir de `q17` (du rôle le plus encadré au plus délégué, ordre à fixer avec les définitions du questionnaire **[à confirmer]**) et le croiser avec la capacité moyenne des tâches utilisées, par domaine.

Un contrôle utile, absent chez Anthropic : comparer le score de capacité théorique à la littératie déclarée (`q8`) et à la formation reçue (`q10`), pour séparer ce qui tient à la tâche de ce qui tient à l'utilisateur.

### 5.7 Étape 6 : texte libre (bloc A)

- Corpus : 53 verbatims `q30` et les réponses « Autre ».
- Élaborer une grille fermée de 10 à 15 thèmes à partir d'une lecture humaine de 20 verbatims (codage inductif), puis la figer.
- Codage multi-étiquettes par un LLM, avec la consigne de ne produire que des étiquettes de la grille. Double codage humain sur l'ensemble du corpus, faisable vu sa taille. Accord rapporté par thème.
- Seuls les comptages par thème sont diffusés.

### 5.8 Étape 7 : vérification, données et cadre institutionnel (volet propre à DoctorIA)

- Vérification : distribution de `q18` et `q19`, types de vérification par domaine. Dans l'export, plus de 9 utilisateurs sur 10 déclarent vérifier « toujours » ou « le plus souvent » (ordre de grandeur provisoire, non pondéré, chiffre exact à reporter en section 3.3 après harmonisation), ce qui appelle une réserve de désirabilité sociale. Croiser avec `q8_limites` et avec le risque « erreurs ou hallucinations ».
- Données sensibles : `q20` par domaine et par école doctorale, croisé avec `q13` (demande d'accès sécurisé) et `q16` (outils locaux).
- Cadre : `q24`, `q25`, `q26` par école doctorale. Tester si un cadre connu ou une discussion en comité de suivi est associé à l'intensité d'usage et aux pratiques de vérification.
- Non-utilisateurs (41) : motifs `q12bis`, profil, attentes de formation. Effectif trop faible pour des croisements fins.
- Besoins de formation : `q27`, `q28` par domaine et par niveau de littératie.

### 5.9 Étape 8 : scénarios (bloc I)

- **Part IA du temps de thèse.** Reprendre la construction d'Anthropic : associer chaque niveau d'usage à une fraction de temps prise en charge, puis agréger par étape et par domaine en pondérant par le temps. Dans DoctorIA, l'échelle 0 à 4 mesure une fréquence et non un niveau de délégation, donc la conversion 0, 25, 50, 75, 100 % d'Anthropic ne s'applique pas telle quelle. Présenter le résultat comme une borne, avec deux conversions alternatives en analyse de sensibilité.
- **Accélération.** Le modèle d'Anthropic repose sur des paramètres propres à son contexte (coûts horaires en dollars, calibration sur Ahmadpoor et Jones 2019) et sur une annexe non consultée. Recommandation : ne pas publier de facteur d'accélération pour la thèse. Si l'équipe y tient, le reléguer en annexe, avec les hypothèses affichées et une analyse de sensibilité.
- Ne pas transposer les anticipations (bloc J) : la question n'a pas été posée.

### 5.10 Méthodes statistiques

- Proportions : intervalles de Wilson. Moyennes et ratios : bootstrap.
- Comparaisons entre domaines : Kruskal-Wallis ou khi-deux, taille d'effet rapportée (V de Cramér, epsilon carré), correction de Benjamini-Hochberg sur l'ensemble des tests confirmatoires.
- Modèles : régression logistique ordinale de l'intensité par tâche sur domaine, ancienneté, financement, littératie, formation, avec `version_questionnaire` et `vague` en contrôle.
- Typologie exploratoire des profils d'usage (classes latentes ou classification hiérarchique sur les 12 items de `q15`).
- Avec 294 répondants, les analyses à plus de deux variables croisées sont réservées au niveau domaine.
- Code versionné, graine aléatoire fixée, prompts et version du modèle archivés pour toute étape utilisant un LLM.

### 5.11 Lecture par le cadre des 4D (AI Fluency)

Source : Dakan et Feller, *Framework for AI Fluency, practical overview document*, version 1.1 du 13 janvier 2025 selon le document fourni (le nom du fichier indique 1.5), https://ringling.libguides.com/ai/framework, licence CC BY-NC-ND 4.0. Le cadre définit quatre compétences (Delegation, Description, Discernment, Diligence) et trois modalités d'interaction (Automation, Augmentation, Agency).

L'étude Anthropic mesure où l'IA est utilisée. Le cadre des 4D décrit ce que l'utilisateur doit savoir faire. Les deux se complètent : le premier structure les étapes 3 à 6, le second structure l'étape 7 et les recommandations de formation.

**Correspondance avec les variables DoctorIA** (proposition à valider) :

| Compétence | Sous-catégories du cadre | Variables DoctorIA | Couverture |
|---|---|---|---|
| Delegation | Goal and task awareness, platform awareness, task delegation | `q14`, `q15` (quelles tâches), `q16` (quels outils), `q17` (rôles), `q12bis` (non-usage par choix), `q8_comprehension` | Bonne |
| Description | Product, process, performance description | Aucune mesure directe. Indirectement : thème « Prompt » demandé en formation (`q28_themes`), `q10` | Très faible |
| Discernment | Product, process, performance discernment | `q8_evaluation`, `q8_limites`, `q18`, `q19` (utilité de la vérification), risque « erreurs ou hallucinations » (`q22`) | Bonne |
| Diligence | Creation, transparency, deployment diligence | `q20` (données sensibles), `q22` (intégrité, sécurité des données), `q23` (mention dans la thèse), `q24` à `q26` (cadre, comité de suivi), `q18_type` (vérification des sources) | Bonne |

**Usages proposés.**

1. **Indices par compétence.** Construire un indice pour Delegation, Discernment et Diligence, vérifier leur cohérence interne, et les décrire par domaine. Pas d'indice Description, faute d'items.
2. **Croisement usage et compétences.** Tester si une intensité d'usage élevée s'accompagne d'un discernement et d'une diligence élevés. Repérer le profil « usage intense, diligence faible », qui est la cible prioritaire d'une formation.
3. **Qualité de la délégation.** L'analyse capacité contre usage (étape 5) mesure, à l'échelle d'un domaine, si les doctorants délèguent là où l'IA est jugée capable. C'est une lecture agrégée de la compétence Delegation.
4. **Modalités.** Rapprocher les rôles de `q17` et les 5 paliers d'Anthropic des trois modalités : assistif et partagé relèvent de l'Augmentation, délégué de l'Automation, autonome de l'Agency. Correspondance approximative, à présenter comme telle.
5. **Grille de codage des verbatims.** Utiliser les 4 compétences et leurs 12 sous-catégories comme taxonomie fermée pour l'étape 6, à côté de la grille thématique inductive.
6. **Besoins de formation.** Classer les thèmes de `q28_themes` par compétence (Outils vers Delegation, Prompt vers Description, Intégrité et Données vers Diligence) pour formuler les recommandations dans un vocabulaire partagé.
7. **Module complémentaire.** Ajouter 3 items sur Description (formulation de la demande, itération, consignes durables), seule compétence non couverte. Ils figurent dans le module de la section 7.
8. **Déclaration de diligence.** Joindre au rapport une déclaration d'usage de l'IA sur le modèle de celle qui clôt le document de Dakan et Feller, puisque l'analyse elle-même mobilise un LLM.

**Réserves.**

- Le cadre est un outil pratique d'orientation, pas une échelle de mesure validée. Les indices sont descriptifs.
- Les items DoctorIA n'ont pas été conçus à partir du cadre. La vérification (`q18`) relève à la fois de Discernment (évaluer la sortie) et de Deployment diligence (se porter garant). Fixer une règle d'affectation avant analyse.
- Une compétence déclarée n'est pas une compétence observée.
- La modalité Agency est presque absente du questionnaire.
- La licence interdit de diffuser une version modifiée du cadre. Le citer et s'y référer, sans en republier une adaptation.

## 6. Hypothèses

Tirées des résultats d'Anthropic, formulées pour la population DoctorIA. H1, H3, H4 et H6 sont confirmatoires. H2 ne le devient que si le module complémentaire (section 7) fournit les parts de temps. H5 est exploratoire.

- **H1.** L'intensité d'usage est plus élevée en sciences formelles qu'en sciences de la vie et santé et qu'en sciences physiques et ingénierie (domaines définis en section 5.2).
- **H2 (conditionnelle).** Les tâches d'écriture et de traitement de données ont une part d'intensité supérieure à leur part de temps ; le recueil de données et l'idéation ont une part inférieure. Le dénominateur (part de temps) n'existe pas dans l'export : sans le module complémentaire, H2 est traitée en exploratoire, par comparaison qualitative (section 5.5).
- **H3.** L'intensité d'usage d'une tâche croît avec son score de capacité théorique.
- **H4.** L'intensité est plus faible pour les tâches à composante physique, interpersonnelle ou soumises à des contraintes réglementaires.
- **H5 (exploratoire).** Les domaines dont les tâches ont un score de capacité moyen plus élevé déclarent des rôles plus délégués (`q17`). Avec 5 domaines, donc 5 points, aucun test n'est possible : description seulement.
- **H6.** Les utilisateurs d'outils spécialisés (`q16` : bibliographie, codage, local) déclarent une intensité plus élevée sur les tâches d'idéation et d'analyse que les utilisateurs des seuls agents généralistes.

Chaque hypothèse confirmatoire est assortie d'un test, d'une taille d'effet et d'un seuil fixés avant analyse.

## 7. Module complémentaire recommandé

Quatre questions suffiraient à combler les écarts de la section 4. Elles reprennent le format de l'enquête d'Anthropic, ce qui rend la comparaison directe. Un cinquième bloc couvre la compétence Description (section 5.11).

1. Répartition du temps de thèse sur les 6 étapes de `q14` (100 points à répartir).
2. Importance de chaque étape pour la qualité de la thèse (100 points à répartir).
3. Niveau d'usage de l'IA par étape, sur les 5 paliers d'Anthropic : aucun, assistif, partagé, délégué, autonome.
4. Horizon auquel l'IA pourrait réaliser seule chaque étape au niveau d'un bon chercheur du domaine (déjà le cas, d'ici 2027, 2030, 2035, plus tard, jamais). Il s'agit d'une collecte nouvelle : le bloc J reste non transposable à partir de l'export actuel (section 5.9).
5. Trois items sur Description : formulation de la demande, itération sur les réponses, consignes durables (même échelle de fréquence que `q15`).

À ajouter aussi : le genre et la tranche d'âge, prévus dans le questionnaire mais vides dans l'export.

## 8. Livrables et calendrier indicatif

| Phase | Contenu | Durée |
|---|---|---|
| 0 | Validation du plan, points **[à confirmer]**, cadre de confidentialité | 1 semaine |
| 1 | Nettoyage, harmonisation, dictionnaire de données | 1 semaine |
| 2 | Effectifs de référence, pondération | 1 à 2 semaines selon accès aux données |
| 3 | Analyses descriptives par domaine, tâche, outil (étapes 3, 4, 7) | 2 semaines |
| 4 | Score de capacité, validation humaine, codage des verbatims | 2 semaines |
| 5 | Tests des hypothèses, scénario « part IA », sensibilité | 1 semaine |
| 6 | Rapport, figures, annexe méthodologique | 2 semaines |

Figures cibles, en miroir d'Anthropic : usage par école doctorale contre effectifs (fig. 1), part d'intensité par catégorie contre temps (fig. 3), profil écrit ou technique par domaine (fig. 7), usage par tercile de capacité (fig. 8), usage par caractéristique de tâche (fig. 10), part IA par domaine (fig. 13). S'y ajoutent trois figures propres à DoctorIA : vérification, données sensibles, cadre institutionnel.

## 9. Limites

- Données déclaratives, sur une échelle de fréquence. Anthropic mesure des sessions observées.
- Auto-sélection probable des répondants intéressés par le sujet.
- Périmètre limité à 8 écoles doctorales. Pas de généralisation nationale.
- Population de doctorants : le temps consacré à chaque tâche diffère vraisemblablement de celui de chercheurs en poste, ce qui fragilise l'option 1 de la section 5.5.
- Changement de version du questionnaire en cours de collecte.
- Douze tâches contre 7 262 dans SciNet : la relation entre capacité et usage sera estimée sur peu de points, d'où la déclinaison par domaine.
- Le score de capacité est produit par un LLM. Il mesure un jugement sur ce que l'IA sait faire, pas une performance mesurée. Anthropic le qualifie de « théorique » pour la même raison.

## 10. Questions ouvertes pour l'équipe DoctorIA

1. Étiquettes exactes de l'échelle 0 à 4 de `q15`, `q16`, `q21`, `q22`.
2. Définitions données aux répondants pour les rôles de `q17`.
3. Sens de « Peut-être » dans `q24` et différence entre « Suggéré », « Recommandé » et « Encouragé » dans `q25`.
4. Nature du changement de version de septembre : technique seulement, ou libellés modifiés.
5. Mode de diffusion et population cible, pour calculer un taux de réponse.
6. Accès possible aux effectifs inscrits par école doctorale.
7. Possibilité de recontacter les répondants pour le module complémentaire.
