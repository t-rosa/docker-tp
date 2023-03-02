- Récupérer l’image sur le Docker Hub
```
docker pull nginx
```

- Vérifier que cette image est présente en local
```
docker images | grep nginx
```

- Créer un fichier index.html simple
```
touch index.html && echo "test" > index.html
```

- Démarrer un conteneur et servir la page html créée précédemment à l’aide d’un volume
```
docker run --name nginx -v ${PWD}/index.html:/usr/share/nginx/html/index.html -d -p 8080:80 nginx
```

- Supprimer le conteneur précédent et arriver au même résultat que précédemment à l’aide de la commande docker cp
```
docker container stop nginx 
docker container rm nginx
docker run --name nginx -d -p 8080:80 nginx
docker cp index.html nginx:/usr/share/nginx/html/
```

```
