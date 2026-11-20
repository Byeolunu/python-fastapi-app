# Reponses du tp 6 : 
•	Q1. Pourquoi la variable n'est-elle pas disponible dans la step qui l'a définie, mais seulement dans les suivantes ?
  - Parce que GitHub Actions lit le fichier $GITHUB_ENV après la fin de chaque step. Les variables enregistrées sont donc disponibles à partir de la step suivante, et non dans celle qui les définit.

•	Q2. Ajoutez un second job verify-env avec une step Print APP_NAME et tentez d'y afficher $APP_NAME. Que constatez-vous ? Quelle est donc la portée de GITHUB_ENV ?

  - On constate que APP_NAME n'est pas disponible dans le job verify-env. En effet, chaque job s'exécute sur un runner différent.

  - Donc, $GITHUB_ENV a une portée limitée au job dans lequel les variables sont définies. Pour transmettre une valeur entre deux jobs, il faut utiliser les job outputs.


Q3. Que se passe-t-il si on utilise > au lieu de >> dans GITHUB_OUTPUT ?

  - \> écrase le contenu précédent du fichier, tandis que >> ajoute une nouvelle ligne. Si on définit deux outputs dans la même step avec >, le premier risque donc d'être écrasé par le deuxième.

Q4. Pourquoi GITHUB_ENV ne suffit-il pas ici ?

  - GITHUB_ENV permet de partager des variables entre les steps d'un même job, mais pas entre plusieurs jobs. GITHUB_OUTPUT permet de créer des outputs qui peuvent être exposés au niveau du job et transmis à un autre job.

Q5. Que se passe-t-il si on retire needs: build ?

  - Le job deploy ne dépend plus de build. Les deux jobs peuvent donc s'exécuter en parallèle. De plus, needs.build.outputs.full_version ne sera pas disponible correctement, car needs sert à déclarer cette dépendance.