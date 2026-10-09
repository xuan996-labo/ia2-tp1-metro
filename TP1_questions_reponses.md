# TP1 — Résumé des questions et des réponses d’aide à l’apprentissage
## À partir de Q5.2

> Ce document résume les principales questions posées et les réponses reçues pendant les échanges. Il ne reproduit pas l’énoncé du TP ni le contenu des fichiers de données. Il s’agit d’un résumé, pas d’une transcription intégrale. La déclaration finale doit refléter honnêtement l’aide réellement utilisée et respecter les consignes de l’enseignant.

## 1. Caractéristiques calculées à partir des repères — Q6.1

**Question posée :**  
Les caractéristiques BFS et Dijkstra ajoutées avec `caracteristiques.extend([nb_arrets, nb_minutes])` ne représentent-elles que deux caractéristiques fixes, alors que l’énoncé en présente cinq ?

**Réponse reçue :**  
Les trois premières caractéristiques sont fixes : nombre de voisins, durée moyenne des tronçons et durée du tronçon le plus long. Pour chaque repère, deux caractéristiques supplémentaires sont ajoutées : le nombre d’arrêts calculé par BFS et la durée en minutes calculée par Dijkstra. Le nombre total est donc de 5 caractéristiques avec un repère, 7 avec deux repères et 9 avec trois repères. La boucle ajoute deux valeurs pour chaque repère sélectionné.

## 2. Interprétation des résultats — Q7.1

**Question posée :**  
Que signifient les résultats de 93,48 % sur les stations apprises et de 25 % sur les stations jamais vues, sachant que la précision de référence est de 43,94 % ?

**Réponse reçue :**  
Le modèle classe très bien les stations d’entraînement, mais obtient de mauvais résultats sur les stations de test. L’écart de 68,48 points de pourcentage suggère un risque de surapprentissage et une capacité de généralisation insuffisante. La précision de test est aussi inférieure à la référence de 43,94 %. Un seul repère pourrait ne pas fournir suffisamment d’informations pour distinguer les lignes. Il faut toutefois comparer la référence et le modèle sur le même ensemble de test pour une comparaison stricte.

## 3. Comparaison d’un, deux et trois repères — Q7.2

**Question posée :**  
Que montrent les résultats obtenus en utilisant un, deux puis trois repères ?

**Résultats communiqués :**
- 1 repère, 5 caractéristiques : 93,48 % à l’entraînement et 25 % au test.
- 2 repères, 7 caractéristiques : 100 % à l’entraînement et 35 % au test.
- 3 repères, 9 caractéristiques : 100 % à l’entraînement et 60 % au test.

**Réponse reçue :**  
La précision de test augmente avec le nombre de repères dans cette expérience. Avec trois repères, elle atteint 60 %, soit plus que la référence globale de 43,94 %. La précision d’entraînement reste à 100 % avec deux et trois repères, alors que la précision de test progresse. L’écart entre entraînement et test diminue de 65 à 40 points entre deux et trois repères, ce qui suggère que la généralisation s’améliore et que les signes de surapprentissage s’atténuent. Cependant, l’écart reste important et le test est petit : avec environ 20 stations de test, une station représente approximativement 5 points de pourcentage. Les résultats doivent donc être interprétés avec prudence.

## 4. Variation des résultats selon `random_state` — Q7.3

**Question posée :**  
Les cinq scores d’un arbre de décision et d’une forêt aléatoire devraient-ils varier de manière linéaire ?

**Réponse reçue :**  
Non. `random_state` est une graine qui contrôle certains aspects aléatoires du modèle; ce n’est ni un niveau de progression ni une valeur qui doit faire augmenter ou diminuer la précision. Les scores peuvent monter, baisser ou rester identiques. Avec environ 20 stations de test, une seule station peut modifier le score d’environ 5 points de pourcentage.

**Question posée :**  
Comment adapter Q7.3 pour utiliser trois repères et comparer les modèles équitablement ?

**Réponse reçue :**  
Utiliser trois repères, fixer le découpage entraînement/test avec `train_test_split(random_state=0)`, puis faire varier séparément le `random_state` de chaque modèle de 0 à 4. Ainsi, les deux modèles sont évalués sur le même ensemble de test et les différences observées proviennent principalement de la graine utilisée par le modèle.

**Résultats finaux communiqués :**
- Arbre de décision : 60 %, 70 %, 55 %, 60 %, 60 %; moyenne de 61 %; écart maximal-minimal de 15 points.
- Forêt aléatoire : 55 %, 70 %, 65 %, 50 %, 55 %; moyenne de 59 %; écart maximal-minimal de 20 points.

**Réponse reçue :**  
Dans cette expérience, l’arbre de décision a une moyenne légèrement supérieure (61 % contre 59 %) et un écart plus faible (15 contre 20 points). La différence moyenne de 2 points est néanmoins très petite, surtout avec un test d’environ 20 stations. On ne peut donc pas conclure que l’arbre est généralement meilleur. La forêt aléatoire n’apporte pas d’amélioration évidente dans ces résultats. Il faut aussi présenter les explications sur les erreurs des arbres comme des hypothèses, car les cinq scores ne permettent pas de vérifier directement si les arbres font les mêmes erreurs.

## 5. Représentation graphique du réseau et des trajets

**Question posée :**  
Comment expliquer en français ce que le graphe montre mieux qu’une simple liste de stations ?

**Réponse reçue :**  
Le graphe permet de visualiser la structure du réseau et ses cycles, les changements de ligne aux stations de correspondance, les différences entre les trajets trouvés par BFS et Dijkstra, ainsi que la durée de chaque tronçon grâce aux étiquettes. Une liste de stations ne montre pas aussi clairement ces relations spatiales et les durées.

## 6. Formulation des observations en français

**Questions posées :**  
Comment traduire en français les interprétations des résultats et comment préciser à quelle partie du TP une observation fait référence ?

**Réponse reçue :**  
Les explications ont été reformulées en français pour les observations de Q7.1, Q7.2 et Q7.3. Il a également été proposé de préciser « la partie 6 du TP1, consacrée à la construction du tableau de données » plutôt que de mentionner simplement « la partie 6 ».

## 7. Rappels avant la remise

- Relancer le carnet du début à la fin et vérifier qu’il s’exécute sans erreur.
- Vérifier que les nombres des observations correspondent aux résultats finaux du carnet.
- Remplir les cellules d’observation demandées.
- Compléter la déclaration d’utilisation de l’IA selon les consignes de l’enseignant, en indiquant honnêtement les types d’aide reçus.
- Respecter les conventions Git du cours.

## 8. Résumé des types d’aide reçus

Les échanges ont porté sur l’explication de caractéristiques calculées par BFS et Dijkstra, l’interprétation des scores d’entraînement et de test, la comparaison de modèles, l’explication de `random_state`, l’adaptation du code de comparaison de Q7.3, ainsi que la traduction et la reformulation en français d’observations. Ajuster cette liste si nécessaire afin qu’elle corresponde exactement à ce qui a été utilisé dans le travail remis.
