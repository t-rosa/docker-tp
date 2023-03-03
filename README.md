- Récupérer l’image sur le Docker Hub
``
docker pull nginx
```

- Vérifier que cette image est présente en local
```bash
docker images | grep nginx
```

- Créer un fichier index.html simple
```bash
touch index.html && echo "test" > index.html
```

- Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume
```bash
docker run --name nginx -v ${PWD}/index.html:/usr/share/nginx/html/index.html -d -p 8080:80 nginx
```

- Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp
```bash
docker container stop nginx 
docker container rm nginx
docker run --name nginx -d -p 8080:80 nginx
docker cp index.html nginx:/usr/share/nginx/html/
```

- A l’aide d’un Dockerfile, créer une image
```bash
touch Dockerfile
```
```yaml
FROM nginx:latest
COPY index.html /usr/share/nginx/html/
```
```bash
docker build -t nginx_custom_image .
```

- Exécuter cette nouvelle image de manière à servir la page html
```bash
docker run --name nginx_custom -d -p 8080:80 nginx_custom_image
```

- Quelles différences observez-vous entre les procédures 5. et 6. ?
```
Les procédures 5. et 6. nous permette toutes deux d'exécuter un serveur web dans un conteneur docker.

La procédure 5. ne demande pas de créer un Dockerfile et de construire une image personnalisé et donc pour pouvoir servir une page html personnalisé avec cette procédure il faut ajouter des étapes suplémentaire comme le fait de mettre en place un volume ou de directement copier le fichier html dans le conteneur.

Contrairement à la procédure 5., la 6. nous demande de créer un Dockerfile et de construire une image personnalisé, ça nous permet de surcharger l'image de base (FROM) afin de simplifier les étapes suivante. De ce fait j'ai pu inclure dans mon image personnalisé la copie de mon fichier html et donc je n'ai pas besoin d'exécuter la commande "docker cp".
```

- Avantages et inconvénients de l’une et de l’autre méthode
```
La procédure 5. est plus accéssble mais ne nous laisse pas la possibilité de surcharger une image facilement.
La procédure 6. demande un peu plus d'éffort mais nous permet de surcharger une image de base à souhait.
```
