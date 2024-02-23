# Symfony 6 + php 8.3 avec Docker

## En local

### Clone du projet
```bash
git clone git@github.com:AlexaneTrubert/symfony-6-docker.git
```

### Modification des fichiers

Dans le docker-compose.yaml, modifier les informations pour la base de données. Les identifiants serviront 
également à se connecter à phpMyAdmin

```yaml
environment:
  MYSQL_ROOT_PASSWORD: root
  MYSQL_DATABASE: symfony
  MYSQL_USER: symfony
  MYSQL_PASSWORD: symfony
```
Dans le app/Dockerfile, modifier la version de PHP si besoin ainsi que les identifiants git. 

```Dockerfile
FROM php:8.3.1-cli
RUN git config --global user.email "you@example.com" \
    &&  git config --global user.name "Your Name"
```

Dans le docker-compose.override.yaml, vous pouvez modifier les variables d'environnements.

### Se connecter au container

!Tips: Pour récupérer le nom de son container

```bash
docker ps
```

```bash
docker-compose exec {nom_de_lapp} bash
```

### Créer un nouveau projet symfony

```bash
symfony new {nom_du_projet} --webapp
cd {nom_du_projet}
symfony serve -d
```

### Créer un utilisateur
```bash
adduser {username}
chown {username}:{username} -R .
```
L'application est disponible à l'adresse [http://localhost:8000](http://localhost:8000)

### Se connecter à la base de données
Modifier le fichier .env pour les informations de connexion à la base de données

```env
DATABASE_URL=mysql://symfony:symfony@mysql:3306/symfony
```

### Connecter PHPStorm à XDebug
Dans PHPStorm, allez dans => File > Settings > Languages & Frameworks > PHP > Servers  
* Cliquez sur le + pour ajouter un nouveau serveur.  
* Dans le champ Name, entrez le nom de votre serveur.
* Dans le champ Host, entrez "localhost"
* Dans le champ Port, entrez "8000"
* Cochez la case "Use path mappings"
* Dans le champ "File/Directory", entrez le chemin de votre projet local (/var/www/html)
Vous pouvez appliquer et sortir des paramètres. Il ne reste plus qu'à cliquer sur l'icône de débogage dans PHPStorm pour lancer le débogage (en haut de la page, à côté du "current file".
