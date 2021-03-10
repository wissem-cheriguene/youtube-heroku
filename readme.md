# Notes

- Pour que les variables d'env. configurées dans le fichier *docker-compose.yml* soient pris en compte par Symfony il faut passer par la commande(**sudo important**) `sudo symfony console` (pour les migrations et ttes autre actions en relation avec la BDD) [explication](https://symfonycasts.com/screencast/symfony-doctrine/console#play)

# Déploiement Heroku

1. `heroku create`
2. ajouter fichier Procfile => `echo 'web: heroku-php-apache2 public/' > Procfile`
3. Creation de la BDD (DATABASE_URL automatiquement MAJ) => `heroku addons:create heroku-postgresql:hobby-dev` 
4. Passer la var d'env. APP_ENV à prod => `heroku config:set APP_ENV=prod`
5. Ajouter au fichier composer.json (pour les migrations sur heroku) : 
```
"compile": [
            "php bin/console doctrine:migrations:migrate"
        ]
```
6. Ajouter le fichier .htaccess (= règles de réécriture Apache) `composer require symfony/apache-pack`