# Demandes à adresser aux établissements

Ces demandes servent à compléter le recensement. Elles portent sur 7 documents introuvables en ligne et sur 2 établissements pour lesquels aucun texte n'a été trouvé. À envoyer au service indiqué ou, à défaut, à la direction de la communication ou au service juridique.

## Modèle de message

**Objet : demande de document, usage de l'intelligence artificielle**

Madame, Monsieur,

Dans le cadre d'un travail de recherche sur l'encadrement de l'intelligence artificielle générative dans les universités françaises, et en particulier en doctorat, je recense les chartes, recommandations et guides publiés depuis 2023.

[Variante A, document identifié] Votre établissement a publié le document suivant : « TITRE » (DATE). Le lien public n'est plus accessible. Pourriez-vous m'en transmettre une copie ou m'indiquer où le consulter ?

[Variante B, aucun document trouvé] Je n'ai trouvé aucun texte de votre établissement sur ce sujet. Pourriez-vous me dire si une charte, des recommandations, une clause du règlement des études ou un texte d'école doctorale existe, adopté ou en préparation, et le cas échéant me le transmettre ?

Ces documents seront cités avec leur source et utilisés uniquement à des fins de recherche.

Avec mes remerciements,

[Nom, fonction, établissement]

## Liste des demandes

| ID | Établissement | Document demandé | Variante | Service à contacter |
|---|---|---|---|---|
| U010 | Université Paris Cité | Charte d'usage des systèmes d'IA générative (16/06/2026) | A | Mission IA ou comité d'éthique et d'intégrité scientifique |
| U057 | Université de Caen Normandie | Livre blanc « Enseigner avec l'intelligence artificielle générative à l'université » | A | Centre d'enseignement multimédia universitaire (CEMU) |
| U071 | Université Toulouse Capitole | Guide « Enseigner dans le supérieur à l'ère de l'IA générative » | A | Service d'appui à la pédagogie |
| U082 | Université Claude Bernard Lyon 1 | Fiche repère étudiants sur l'IA (ISTR, masso-kinésithérapie, février 2025) | A | Département de masso-kinésithérapie de l'ISTR |
| U084 | Université Grenoble Alpes | Délibération cadrage IA (CFVU du 16/10/2025, CA du 23/10/2025) | A | Direction des affaires juridiques ou secrétariat des conseils |
| U090 | INU Champollion (Albi) | Charte des pratiques de l'intelligence artificielle (V1, septembre 2025) | A | Service numérique |
| U099 | Le Mans Université | Charte sur l'utilisation de l'intelligence artificielle (CA du 25/09/2025) | A | Secrétariat des conseils |
| | Université de Guyane | Tout texte sur l'IA, y compris de l'école doctorale 587 | B | Vice-présidence formation ou école doctorale |
| | Università di Corsica | Tout texte sur l'IA, y compris de l'école doctorale 377 | B | Vice-présidence formation ou école doctorale |

Une fois un document reçu, l'enregistrer dans `documents/` sous le nom `<ID>_<etablissement>.pdf`, puis lancer `python3 scripts/construire.py` pour mettre à jour le tableau.
