# 📊 Analyse des zones de forte demande Uber à New York (2014-2015)

## 📌 Présentation du projet

Ce projet analyse les courses Uber à New York à partir de deux jeux de données couvrant avril à septembre 2014 et janvier à juin 2015.

L'objectif est d'identifier les zones géographiques où la demande est la plus importante et d'étudier les variations de l'activité selon les jours de la semaine et les heures de prise en charge.

Cette analyse vise à proposer des recommandations pour mieux répartir la disponibilité des chauffeurs et contribuer à réduire le temps d'attente des clients. L'objectif opérationnel est de limiter l'attente à moins de 7 minutes, seuil au-delà duquel les clients sont susceptibles d'annuler leur course. Cet objectif nécessiterait toutefois des données spécifiques sur les temps d'attente et les annulations pour être évalué directement.

Les deux jeux de données ne couvrant pas les mêmes périodes et ne contenant pas les mêmes variables, l'analyse de 2014 repose sur un clustering géographique, tandis que celle de 2015 s'appuie sur le volume de courses par zone. Les résultats sont ensuite comparés afin d'examiner les tendances générales de concentration de la demande.

## 🎯 Objectifs

- Analyser la répartition géographique des courses Uber
- Identifier les zones présentant une forte concentration de courses à l'aide de KMeans
- Étudier la demande selon les jours de la semaine et les heures de prise en charge
- Identifier les heures de pointe pour chaque jour et chaque zone ou cluster
- Comparer les tendances générales observées en 2014 et 2015
- Formuler des recommandations pour améliorer la disponibilité des chauffeurs dans les zones et aux périodes les plus demandées 

## 📊 Données

**Données de 2014**

Période étudiée : avril à septembre 2014

Le dataset contient 4 534 327 observations et 4 variables :

- Date/Time - Date et heure de la course
- Lat - Latitude du point de prise en charge
- Lon - Longitude du point de prise en charge
- Base - Identifiant de la base Uber associée

**Données de 2015**

Période étudiée : janvier à juin 2015

Le dataset contient 14 270 479 observations et 6 variables :

- Pickup_date - Date et heure de la course
- Dispatching_base_num - Identifiant de la base ayant distribué la demande
- Affiliated_base_num - Identifiant de la base affiliée
- LocationID - Identifiant de la zone de prise en charge
- Zone - Nom de la zone géographique
- Borough - District de New York auquel appartient la zone

## ⚙️ Méthodologie

1. **Analyse de 2014 : clustering géographique**

L'analyse de 2014 repose sur les coordonnées de latitude et de longitude des prises en charge. L'algorithme K-Means est utilisé pour regrouper les points géographiques en fonction de leur proximité spatiale. L'algorithme K-Means est utilisé pour regrouper les points géographiques en fonction de leur proximité spatiale.

La méthode du coude (Elbow Method) a permis d'examiner plusieurs nombres de clusters, avec une plage de solutions pertinentes comprise entre 4 et 10 clusters. Compte tenu de l'objectif d'identifier des zones opérationnelles suffisamment détaillées pour orienter la disponibilité des chauffeurs, 8 clusters ont été retenus. Ce choix a également été étayé par l'analyse du coefficient de silhouette, qui atteint 0,46 pour cette solution.

Les huit clusters sont ensuite analysés selon le jour de la semaine et l'heure de prise en charge afin d'identifier les périodes de forte demande dans chaque zone géographique.

2. **Analyse de 2015 : clustering selon le volume de courses**

Pour 2015, le nombre de courses est calculé pour chaque zone géographique à partir de son identifiant LocationID.

L'algorithme K-Means est ensuite appliqué au nombre de courses par zone afin de regrouper les zones présentant des volumes d'activité similaires.

L'analyse de l'inertie et le coefficient de silhouette ont été utilisés pour guider le choix du nombre de clusters. Trois clusters ont été retenus, avec un coefficient de silhouette de 0,77.

Les trois clusters sont ensuite étudiés selon leur répartition par borough, les volumes de courses et les variations de la demande selon le jour et l'heure.

Limite méthodologique : les clusters de 2014 correspondent à des regroupements géographiques, alors que ceux de 2015 regroupent des zones selon leur volume de courses. Les numéros de clusters ne sont donc pas directement comparables entre les deux années.

## 📈 Résultats des analyses

**Avril à septembre 2014**

L'analyse met en évidence huit clusters géographiques de prises en charge. Les zones de forte demande se concentrent principalement à Manhattan et à Brooklyn, notamment dans les clusters 0, 1 et 6, suivis de secteurs de Queens représentés notamment dans les clusters 2 et 5.

Les heures de pointe varient selon les zones et les jours de la semaine, avec une concentration générale de la demande en fin de journée.

Voici les zones identifiées et les recommandations :

| Cluster | Principales zones observées | Jour de plus forte demande | Recommandations 
|---|---|---|---|
| 0 | Manhattan, Midtown | Jeudi | Renforcer la disponibilité tous les jours en fin d'après-midi entre 16h et 18h
| 1 | Manhattan, lower Village | Vendredi | Renforcer la disponibilité vers 17h en début de semaine et à partir de 21h en fin de semaine, notament le vendredi et le samedi
| 2 | Sud de Queens et Long Island | Dimanche | Renforcer la disponibilité vers 14h du lundi au samedi, 19h le dimanche
| 3 | Ouest de Manhattan, new Jersey | Lundi | Prévoir une couverture régulière l'après-midi, l'heure de pointe est à 15h
| 4 | Sud de Brooklyn | Samedi | Prévoir une couverture régulière à 7h en semaine et vers 20h à 21h du vendredi au dimanche
| 5 | Nord de Queens | Jeudi | Renforcer la disponibilité en soirée tout au long de la semaine, à 17h le samedi
| 6 | Nord de Brooklyn | Samedi | Prévoir une couverture tardive du mardi au dimanche, à partir de 21h
| 7 | Manhattan (Washington Heights) | Samedi | Renforcer la disponibilité entre 20h et 21h du mardi au samedi et entre 14h et 15h le lundi et le dimanche

**Janvier à juin 2015**

L'analyse de 2015 met en évidence trois clusters de zones présentant des volumes de courses différents. Manhattan, Brooklyn et Queens occupent une place importante dans la répartition de la demande.

L'activité est particulièrement soutenue en fin d'après-midi et en soirée, mais les profils varient selon les clusters.

Voici les zones identifiées et les recommandations :

| Cluster | Principales zones observées | Jour de plus forte demande | Recommandations 
|---|---|---|---|
| 0 | Queens, Brooklyn; Bronx | Samedi | enforcer la disponibilité le vendredi et le samedi, notamment vers 22 h et 23 h, et vers 8h du lundi au jeudi
| 1 | Manhattan | Vendredi | Prévoir une couverture tardive, avec des pics hebdomadaires entre 18 h et 23 h.
| 2 | Manhattan, Brooklyn | Samedi | Renforcer la disponibilité autour de 18 h et 19 h, du mardi au samedi, et vers 8h le lundi


## 🔎 Conclusion - Comparaison des tendances entre 2014 et 2015

Les résultats de 2015 renforcent la tendance générale observée en 2014 car les deux analyses mettent en évidence une forte concentration de la demande à Manhattan et Brooklyn avec les heures de pointe en fin d'après-midi et en soirée.

L'analyse de 2014 permet de distinguer huit zones géographiques et d'étudier leurs profils temporels. Celle de 2015 regroupe les zones selon leur volume de courses et confirme l'importance de plusieurs boroughs dans la répartition de la demande.

Les résultats suggèrent que la disponibilité des chauffeurs pourrait être adaptée en fonction des zones et des heures de pointe. Cependant, ces analyses portent sur les courses enregistrées et ne permettent pas de mesurer directement le temps d'attente des clients ni de démontrer que les recommandations réduiraient les annulations.

Pour confirmer plus rigoureusement la stabilité des zones à forte demande, il serait pertinent de rattacher les coordonnées de 2014 aux zones géographiques officielles utilisées en 2015, puis de comparer les mêmes unités géographiques sur des périodes équivalentes.

Enfin, l'accès à des données détaillées sur les demandes, les temps d'attente, les annulations et la disponibilité des chauffeurs permettrait d'évaluer concrètement l'effet d'une meilleure répartition des véhicules sur l'objectif d'un temps d'attente inférieur à 7 minutes.

## 🚀 Perspectives d'amélioration

- Harmoniser les unités géographiques utilisées pour 2014 et 2015.
- Comparer les deux années sur des périodes équivalentes afin de mieux prendre en compte la saisonnalité.
- Développer un tableau de bord interactif permettant de filtrer les résultats par zone, cluster, jour et heure.
- Évaluer les recommandations à partir de données sur les temps d'attente, les annulations et la disponibilité des chauffeurs.