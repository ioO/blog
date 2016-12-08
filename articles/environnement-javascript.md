# Environnement javascript

Pour le projet [écrire](https://github.com/ioO/ecrire), je m'intéresse à l'écosystème javascript. Sur le long terme je 
souhaite utiliser [electron](http://electron.atom.io/) pour proposer une application de bureau. Avant d'arriver à ce 
résultat, je me suis replongé dans les outils disponibles pour créer un environnement de travail. 

Voici les outils que j'ai sélectionnés pour me créer une base de travail pour démarrer ce projet :
* npm
* babel
* eslint
* mocha
* chai
* babel plugin coverage
* nyc

L'objectif est de pouvoir coder en apprenant la syntaxe es6 et d'utiliser des outils qui m'aident à garder une qualité 
de code. La base de code de cet article est celle du [tag v.0.0.1](https://github.com/ioO/ecrire/releases/tag/v0.0.1) 
dans le dépôt.

## npm
Node package manager est un outil agréable. Le fichier _package.json_ permet de gérer son projet correctement. 

Les options _--save-dev_ et _--save_ permettent de bien gérer les dépendances du projet[^1].

    "devDependencies": {
        "babel-cli": "^6.14.0",
        "babel-plugin-__coverage__": "^11.0.0",
        "babel-preset-es2015": "^6.14.0",
        "chai": "^3.5.0",
        "eslint": "^3.6.1",
        "mocha": "^3.0.2",
        "nyc": "^8.3.0"
    }

J'apprécie énormément les scripts et leur facilité de syntaxe. Cela permet de remplacer les 
[Makefile](https://fr.wikipedia.org/wiki/Make#Makefile) simplement. La syntaxe qui permet de découper des tâches, par 
exemple avec les tâches _babelify_ donne une souplesse.

    "babelify:test": "$(npm bin)/babel test/tests.es6 --out-file test/tests.js",
    "babelify:app": "$(npm bin)/babel index.es6 --out-file index.js",
    "babelify": "npm run babelify:test && npm run babelify:app"

### Astuce 

  $(npm bin) retrouve le chemin vers les exécutables dans le dossier node_modules de votre projet.

## Babel et eslint

Apprendre la syntaxe ECMAscript 6.0 me semble une évidence. Quitte à être novice sur un langage, autant apprendre la 
prochaine syntaxe. [Babel](http://babeljs.io/) permet de convertir le code es6 en javascript es5. 
[eslint](http://eslint.org/) me permet de vérifier mon apprentissage de la syntaxe.

## Mocha et Chai

Au départ je n'ai utilisé que [Mocha](https://mochajs.org/). Par chance, un simple test à faire m'a amené à utiliser la 
fonction _isArray_.

Cela m'a permis de comprendre la différence entre mocha, qui est un moteur de tests, et [Chai](http://chaijs.com/), qui 
apporte les fonctions de tests (assert, should, expect). Vous pouvez utiliser seulement mocha, dans ce cas ce sont [les 
fonctions de tests de nodejs](https://nodejs.org/api/assert.html) que vous utilisez.

Le point qui m'a fait choisir Mocha c'est la lisibilité tant sur l'écriture des tests que sur la lecture des résultats.

## Couverture de code

La couverture de code permet dans un premier temps de se forcer à faire des tests mais aussi de découvrir les outils de 
tests. Sur le plus long terme c'est un indicateur de l'évolution de la qualité du code.

Sur cet exercice j'ai touché la problématique de l'environnement _nodejs_ : le nombre de paquets pour faire une chose. 
A contrario, je suis agréablement surpris par la qualité de la documentation des projets.

Par contre cela fait beaucoup de lecture et comme les paquets s'intègrent de manières différentes entre eux, la 
digestion est difficile.

J'ai opté pour [babel-plugin-__coverage__](https://www.npmjs.com/package/babel-plugin-__coverage__) et 
[nyc](https://github.com/istanbuljs/nyc) pour la création de comptes-rendus.

## Conclusion

Je connais quelques points à améliorer, comme l'automatisation de la conversion avec babel, une meilleure intégration 
de nyc pour la couverture de code.

Au fur et à mesure, cette base d'outils pour le projet va évoluer et, par expérience, je sais que j'ajouterai d'autres 
outils. Mais l'essentiel est là, j'ai un environnement de travail qui me permet de démarrer le projet.

[^1]: contrairement [à pip, dommage](/articles/j-y-pip-rien.md)
