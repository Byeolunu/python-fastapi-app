# Reponses du tp 6 : 
•	Q1. Pourquoi la variable n'est-elle pas disponible dans la step qui l'a définie, mais seulement dans les suivantes ?
  - Parce que GitHub Actions lit le fichier $GITHUB_ENV après la fin de chaque step. Les variables enregistrées sont donc disponibles à partir de la step suivante, et non dans celle qui les définit.

•	Q2. Ajoutez un second job verify-env avec une step Print APP_NAME et tentez d'y afficher $APP_NAME. Que constatez-vous ? Quelle est donc la portée de GITHUB_ENV ?

  - On constate que APP_NAME n'est pas disponible dans le job verify-env. En effet, chaque job s'exécute sur un runner différent.

  - Donc, $GITHUB_ENV a une portée limitée au job dans lequel les variables sont définies. Pour transmettre une valeur entre deux jobs, il faut utiliser les job outputs.
