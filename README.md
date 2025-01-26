# Projet de digitalisation des commerces parisiens - Documentation

## Structure du projet
```
Digitalisation_Commerces_Parisiens/
├── BCOM2023.ipynb                           # Code du projet sous Jupyter
├── data/                                    # Dossier contenant les fichiers de données CSV
│   ├── BDCOM_2023(in).csv                   # Fichier de données initial
│   ├── export_for_search.csv                # Fichier préparé pour le géocodage
│   ├── result_geocoded.csv                  # Résultats du géocodage
│   ├── BCOM2023_enriched.csv                # Fichier enrichi avec les coordonnées GPS
│   └── BCOM2023_avec_site_et_livraison.csv  # Fichier final enrichi
├── README.md                                # Documentation du projet
```

## Étape 1 : Chargement et exploration des données

Dans cette étape, nous avons chargé le fichier CSV contenant les données des commerces parisiens dans un notebook Jupyter. L'objectif était d'explorer les colonnes disponibles afin d'identifier celles utiles pour la recherche des coordonnées géographiques, telles que l'adresse, le code postal et l'arrondissement. Nous avons également vérifié la qualité des données en identifiant les valeurs manquantes et les incohérences.

Fichier utilisé : `data/BDCOM_2023(in).csv`

Une fois l'exploration terminée, une colonne 'adresse' a été construite en concaténant les informations de l'adresse (numéro, lettre, type de voie, libellé de voie et arrondissement) pour préparer les données au géocodage.

## Étape 2 : Géocodage des adresses

Pour enrichir le dataset avec des coordonnées GPS, nous avons utilisé l'API de géocodage du gouvernement français. La liste des adresses a été exportée dans un fichier CSV, puis soumise à l'API via une requête HTTP POST. Les résultats obtenus (latitude et longitude) ont été enregistrés dans un nouveau fichier et intégrés dans le dataset initial.

Fichiers utilisés : `data/export_for_search.csv`, `data/result_geocoded.csv`

En cas de succès, le fichier enrichi avec les coordonnées a été sauvegardé, permettant ainsi d'améliorer les analyses spatiales des commerces.

## Étape 3 : Recherche des sites web des commerces

L'étape suivante a consisté à rechercher les sites web des commerces à l'aide de l'outil Selenium et de la bibliothèque BeautifulSoup. L'idée était de scrapper les informations à partir de Google Maps en utilisant les adresses des commerces et leurs coordonnées géographiques.

Fichier utilisé : `data/BCOM2023_enriched.csv`

Nous avons mis en place un script qui génère dynamiquement des URLs de recherche Google Maps en combinant les informations d'adresse et de géolocalisation. Le navigateur automatisé a ensuite parcouru ces pages et extrait les liens des sites web ainsi que des indices de disponibilité de service de livraison.

Des pauses ont été introduites entre chaque requête pour éviter un blocage par Google. Enfin, les résultats ont été ajoutés au dataset principal.

Fichier produit : `data/BDCOM_2023_avec_site_et_livraison_test.csv`

## Étape 4 : Intégration des nouvelles données

Après avoir enrichi les données avec les coordonnées GPS et les sites web des commerces, nous avons fusionné ces informations dans le dataset initial. La base de données finale contient désormais des colonnes supplémentaires pour les liens des sites web et l'indication de la disponibilité d'un service de livraison.

Fichier final : `data/BCOM2023_avec_site_et_livraison.csv`

Le fichier final a été sauvegardé sous un format compatible pour d'éventuelles analyses ultérieures.

## Étape 5 : Défis rencontrés

Plusieurs défis ont été rencontrés tout au long du projet, notamment :
- Gestion des valeurs manquantes et incohérences dans les données initiales.
- Limitation des requêtes aux APIs (quotas et délais d'attente).
- Adaptation du scraping pour extraire efficacement les informations.
- Respect des bonnes pratiques en matière de collecte automatisée de données.

## Conclusion

Ce projet a permis d'enrichir une base de données de commerces parisiens en y ajoutant des informations géographiques et numériques cruciales pour une meilleure digitalisation. Les résultats obtenus sont exploitables pour des analyses plus poussées dans le cadre de la transformation numérique des commerces locaux.
