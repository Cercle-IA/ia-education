# Chartes, recommandations et guides IA des universités françaises (2023 à 2026)

Recensement des textes publiés depuis janvier 2023 par les universités françaises sur l'usage de l'IA (surtout générative), avec un repérage spécifique des textes qui portent sur le doctorat. État au 11 novembre 2026.

## Contenu du dossier

| Fichier | Rôle |
|---|---|
| `TABLEAU.md` | Tableau lisible : d'abord les documents liés au doctorat, puis l'ensemble |
| `recensement.xlsx` | Tableau complet avec filtres, onglets Doctorat, Universités, Cadres nationaux, Sources de recensement, Légende |
| `recensement.csv` | Même contenu au format CSV (UTF-8) |
| `domaines.txt` | Domaines à autoriser pour télécharger les documents |
| `scripts/donnees.txt` | Source unique des données (une ligne par document) |
| `scripts/construire.py` | Régénère le CSV, le XLSX et `TABLEAU.md` à partir de `donnees.txt` |
| `scripts/telecharger.py` | Télécharge tous les documents dans `documents/` avec un journal (statut, taille, SHA-256) |

## Chiffres clés

- 141 documents : 123 émanant de 66 universités ou établissements universitaires (établissement, composante ou école doctorale), 6 d'autres établissements d'enseignement supérieur, 12 cadres nationaux.
- Doctorat : 14 documents propres au doctorat, 19 qui le couvrent en partie (volet recherche, relais par une école doctorale), 15 à confirmer.
- 107 documents ont une URL de PDF directe.
- Répartition par année : 2023 (5), 2024 (10), 2025 (63), 2026 (46), non datés (17).

## Ce qu'il faut retenir sur le doctorat

- Aucun texte national dédié à l'IA en doctorat n'a été trouvé (ni MESR, ni RNCD, ni Ofis). La fiche de l'Ofis « Systèmes d'intelligence artificielle générative : quelques points de vigilance » est le texte national le plus proche.
- Les règles doctorales viennent surtout des écoles doctorales et des chartes du doctorat : charte du doctorat PSL (section 2.7, 2026), charte du doctorat de l'ED 286 de l'EHESS (2026), recommandation IA de l'ED de droit de la Sorbonne (Paris 1), formulaire de déclaration de l'ED 441 (Paris 1), règlements intérieurs des ED VAAME et Végétal (Pays de la Loire, décembre 2025), supports doctorat de l'Université Paris-Saclay (2026).
- Les chartes d'établissement couvrent souvent la recherche sans viser les doctorants en tant que tels (Toulouse, Clermont Auvergne, La Réunion, Le Mans, Rouen, Orléans, Paris 8).

## Méthode et limites

1. Recherche par moteur de recherche, université par université (liste des universités publiques françaises, métropole et outre-mer), puis recherches ciblées sur le doctorat et sur les recensements existants (DINUM, observatoire IA formation d'Aix-Marseille, bibliographie de Paris 8, CCN de Strasbourg).
2. **Les documents n'ont pas pu être ouverts ni téléchargés** depuis l'environnement de travail : sa politique réseau bloque les sites universitaires. Chaque ligne indique donc son niveau de vérification :
   - `Extrait` : titre, URL et date vus dans les résultats du moteur de recherche.
   - `Cité` : document seulement mentionné par une source secondaire.
3. Une date déduite du dossier de mise en ligne d'un fichier peut différer de la date d'adoption.
4. L'absence d'une université ne prouve pas l'absence de texte. Établissements sans document propre trouvé : Paris Nanterre, Sorbonne Paris Nord, UTC Compiègne, Artois, Littoral Côte d'Opale, Haute-Alsace, Antilles, Guyane, Corse, Nouvelle-Calédonie, Polynésie française. Pau et Toulouse Jean Jaurès ont seulement des clauses dans leurs règles d'examen, avec une charte annoncée.

## Télécharger les documents

Depuis une machine qui a accès au web (Python 3.8 ou plus, sans dépendance) :

```bash
cd chartes-ia-universites
python3 scripts/telecharger.py              # tous les documents
python3 scripts/telecharger.py --doctorat   # seulement doctorat (oui ou partiel)
```

Les fichiers arrivent dans `documents/` sous le nom `<ID>_<établissement>.pdf` (ou `.html` quand seule une page existe). Le journal `documents/_journal.csv` donne l'empreinte SHA-256 de chaque fichier.

Pour le faire dans une session Claude Code cloud, ajoutez les domaines de `domaines.txt` aux domaines autorisés de l'environnement (Network access), voir https://code.claude.com/docs/en/cloud-environments#network-access.

## Mettre à jour

Ajoutez ou corrigez une ligne dans `scripts/donnees.txt`, puis lancez `python3 scripts/construire.py`.
