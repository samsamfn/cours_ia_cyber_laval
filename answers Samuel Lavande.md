
Partie 1

Q1 

X.shape
(2494, 28)
Il y a donc 2494 exemplaires 

Q2
y.value_counts()

•	East North Central : 758
•	West North Central : 358
•	Middle Atlantic : 334
•	South Atlantic : 248
•	Pacific : 243
•	Mountain : 190
•	West South Central : 172
•	East South Central : 97
•	New England : 94

La région la plus représentée est East North Central (758).
La moins représentée est New England (94).
Donc la target est déséquilibrée.




Q3 
len(X.columns) 
X.columns
Il y a 28 features 


Q4
Non il n’y a pas de valeurs manquantes

Q5
X["How_much_do_you_personally_identify_as_a_Midwesterner"].value_counts()
La réponse la plus fréquente est :
“Not at all” (965 réponses).

Q6 
from sklearn.metrics import recall_score

recall_lr = recall_score(y_test, y_pred_lr, pos_label="North Central")
recall_rf = recall_score(y_test, y_pred_rf, pos_label="North Central")
recall_gb = recall_score(y_test, y_pred_gb, pos_label="North Central")

recall_lr, recall_rf, recall_gb

Le modèle qui a le meilleur recall est Gradient Boosting
car il obtient un recall de 0.9895, ce qui est supérieur à celui de Random Forest (0.9238) et largement supérieur à la Régression Logistique (0.00).



Q7

from sklearn.metrics import classification_report

print("Logistic")
print(classification_report(y_test, y_pred_lr))

print("Random Forest")
print(classification_report(y_test, y_pred_rf))

print("Gradient Boosting")
print(classification_report(y_test, y_pred_gb))



Le modèle ayant la meilleure application pratique est Gradient Boosting, car il combine :
•	Très forte précision (peu de faux positifs coûteux)
•	bon recall (trouve presque tous les cas positifs)
•	Meilleure accuracy globale
C’est donc le modèle le plus rentable dans ce contexte.


Q8
Le modèle qui généralise le mieux est Gradient Boosting, car :
•	Il obtient la meilleure performance globale
•	Il présente des scores élevés et équilibrés
•	Il ne montre pas de comportement instable
 

PARTIE 2

Q1
•	Il est créé par du code Python via le fichier du module midwest_survey_models nommé « transformers.py. »
•	Le code construit un chemin vers un dossier tmp, le crée si besoin, puis écrit security_breach.txt.
Le fichier est créé dans la méthode transform() d’un transformer.
Il est exécuté lorsque le modèle est utilisé (predict/transform).
Cela montre qu’un modèle pickle peut exécuter du code arbitraire.


Q2 

Ce fichier pourrait supprimer des fichiers, exfiltrer des données, chiffré les données ou encore exécuter des commandes systèmes 



Q3

Pour partager un modèle de manière plus sécurisée, il est préférable d’utiliser skops plutôt que pickle. Lorsque l’on charge un fichier pickle, Python peut exécuter automatiquement du code contenu dans l’objet sérialisé.
Cela signifie qu’un modèle malveillant peut :
•	Créer des fichiers,
•	Supprimer des données,
•	Exécuter des commandes système,
•	Ou voler des informations.

Skops a été conçu spécialement pour partager des modèles scikit-learn de manière plus sécurisée.
Il ne recharge pas du code arbitraire et il est conçu pour le partage



