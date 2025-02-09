---
title: "Les modes de rendu web"
author: "@henri"
dates:
  published: "2025-02-09"
---

À l'origine du web, le rendu des pages était simple : un serveur générait du contenu statique en HTML que les navigateurs interprétaient pour afficher des pages. Les premiers sites web étaient des collections de fichiers HTML fixes, chaque page étant créée individuellement et servie directement au navigateur. Avec l'émergence de sites plus complexes, notamment avec l'arrivée du contenu dynamique, les besoins ont évolué. C’est dans ce contexte que les trois principaux modes de rendu actuels ont émergé : Server Side Rendering (SSR), Static Site Generation (SSG) et Client Side Rendering (CSR). Dans cet article, nous explorerons le fonctionnement de chacun, les cas d’usage pour lesquels ils sont les mieux adaptés, ainsi que les solutions hybrides qui combinent leurs avantages pour optimiser la performance, le SEO et l’expérience utilisateur.

# Le Server Side Rendering (SSR)

Le SSR est l'une des approches les plus anciennes pour générer des pages web dynamiques. Dans ce modèle, le serveur génère le HTML de manière dynamique à chaque requête avant de l'envoyer au navigateur. Cela signifie que le contenu est déjà pré-rendu et prêt à être affiché dès que l'utilisateur reçoit la page.

## Étapes du processus SSR :

  1. Le navigateur envoie une requête au serveur.
  2. Le serveur génère dynamiquement le HTML en fonction des données et des modèles.
  3. Le HTML complet est envoyé au navigateur, qui l'affiche immédiatement.

## Avantages du SSR :

### Amélioration du SEO :
Comme le contenu est déjà pré-rendu côté serveur, les moteurs de recherche peuvent facilement indexer les pages sans avoir à attendre l'exécution du JavaScript. Cela permet une optimisation SEO efficace, notamment pour les sites qui dépendent d'un bon classement sur Google.

*Exemple : Un site d'actualités ou un blog avec du contenu fréquemment mis à jour bénéficiera grandement du SSR pour s'assurer que les nouveaux articles sont indexés rapidement.*

### Contenu immédiatement disponible :
Le SSR permet d’afficher rapidement du contenu même avant que tous les scripts JavaScript ne soient chargés. Cela améliore l’expérience utilisateur, notamment sur les connexions lentes, car l’utilisateur voit quelque chose à l’écran tout de suite.

*Exemple : Un site e-commerce où il est crucial que les utilisateurs voient rapidement les produits dès l'ouverture de la page.*

### Meilleure compatibilité :
Les utilisateurs qui désactivent JavaScript ou les moteurs de recherche qui n'exécutent pas de JS peuvent toujours accéder au contenu car il est déjà disponible dans le HTML initial.

*Exemple : Un service public en ligne qui doit garantir l’accessibilité à un large public, y compris ceux avec des configurations spécifiques.*

## Inconvénients du SSR :

### Temps de réponse plus long :
À chaque requête utilisateur, le serveur doit générer le HTML, ce qui peut introduire une latence supplémentaire, surtout sous une forte charge. En cas de pic de trafic, les serveurs doivent traiter chaque requête de manière individuelle, augmentant la pression sur les ressources.

*Exemple : Lors des soldes sur un site e-commerce, des milliers d’utilisateurs peuvent se connecter simultanément, augmentant le temps de réponse à cause de la génération dynamique des pages.*

### Coût d’hébergement plus élevé :
Le SSR sollicite constamment le serveur à chaque requête, nécessitant donc une infrastructure plus puissante ou plus de serveurs pour traiter le trafic. Cela peut rapidement augmenter les coûts d’hébergement, notamment pour des sites avec un trafic élevé.

### Complexité accrue pour certaines optimisations côté client :
Avec SSR, il peut être plus compliqué de gérer des interactions très dynamiques ou des comportements côté client qui dépendent de JavaScript, car il faut jongler entre le rendu initial côté serveur et les mises à jour via JS. Cela nécessite souvent de mettre en place une logique d’hydratation, où le côté client prend le relais une fois que le HTML est rendu.

*Exemple : Une application SaaS avec une interface utilisateur riche et beaucoup d’interactions personnalisées peut rencontrer des difficultés à équilibrer SSR et réactivité.*

## Le SSR et l’hydratation :

Dans un site SSR classique, chaque changement de page ou navigation implique une requête complète au serveur. Prenons l'exemple d'un utilisateur sur un site e-commerce qui clique sur un produit pour voir ses détails. Ce processus entraîne une charge importante côté serveur, car chaque clic ou navigation déclenche une nouvelle génération du HTML. 

Imaginons maintenant que l'utilisateur reste sur la même page et interagit avec des éléments dynamiques de l'interface, comme ajouter un produit au panier, filtrer des résultats, ou cliquer sur un bouton « J'aime ». Le JavaScript côté client gère l'interaction : même dans un site SSR, des fonctionnalités peuvent être implémentées avec JavaScript pour offrir une interactivité sur le front-end. Dans notre exemple du « J’aime », c’est un code JavaScript côté client qui interceptera cet événement (souvent via un appel API au serveur) et mettra à jour le DOM sans avoir besoin de régénérer entièrement la page. Mises à jour dynamiques du DOM : Les interactions qui ne nécessitent pas de chargement de nouvelles données HTML peuvent être gérées localement par JavaScript. Ainsi, bien que la page ait été initialement rendue côté serveur, JavaScript peut continuer à rendre l’interface plus dynamique et interactive après coup. Cela permet d'éviter des rafraîchissements lourds pour chaque petite interaction.


# Static Site Generation (SSG)

Dans l'approche SSG, tout le contenu HTML est généré au moment de la phase de build, avant toute requête utilisateur. Chaque page est pré-rendue côté serveur, ce qui signifie que lorsque le client demande une page, elle est déjà prête et n'a pas besoin d'être générée dynamiquement. Cela permet des temps de chargement extrêmement rapides et une excellente optimisation pour le SEO.

Cette méthode est particulièrement adaptée aux sites dont le contenu ne change pas souvent ou qui affichent les mêmes informations à tous les utilisateurs, comme les blogs ou les pages documentaires.

## Étapes du processus SSG :

  1. Les pages HTML statiques sont construites en amont lors du build.
  2. Le serveur renvoie la page pré-rendue à chaque requête.

## Avantages du SSG

### Excellentes performances :

Les pages étant prérendues lors du build, elles sont servies directement par un serveur, sans nécessiter de génération de contenu dynamique à chaque requête.
Cela entraîne des temps de chargement ultra rapides, car aucune logique côté serveur n’est requise pour construire la page à la demande. La page est servie "telle quelle", souvent depuis un CDN (Content Delivery Network), ce qui réduit encore les temps de latence.

### Coût d'hébergement réduit :

Les fichiers HTML étant statiques, l’hébergement de sites SSG est très économique. Il n’est pas nécessaire de maintenir un serveur complexe pour traiter des requêtes dynamiques. Un hébergement statique suffit (comme Netlify, GitHub Pages, Vercel, etc.).
Cela rend aussi le site plus scalable, car il peut gérer des pics de trafic élevés sans surcharger le serveur.

### SEO optimal :

Les pages étant déjà rendes côté serveur, le contenu est immédiatement accessible pour les moteurs de recherche. Cela améliore considérablement le référencement naturel (SEO) par rapport à une approche client-side (CSR), où le contenu n’est pas visible tant que le JavaScript n’a pas été exécuté.
L'indexation par les moteurs de recherche est donc plus simple et plus efficace.
Sécurité accrue :

Comme il n'y a pas de serveur back-end actif en permanence qui traite des requêtes ou génère des pages à la demande, la surface d'attaque est réduite. Il y a moins de points d'entrée pour les pirates, car les pages statiques n'exécutent aucun code serveur.

## Inconvénients du SSG

### Manque de personnalisation :

Puisque les pages sont générées à l'avance, il est difficile de les personnaliser dynamiquement en fonction des utilisateurs ou des données contextuelles.
Tous les utilisateurs reçoivent exactement la même page. Il est donc impossible de proposer des interfaces personnalisées à moins d’utiliser du JavaScript côté client pour modifier l’affichage après coup, ce qui pourrait entraîner une surcharge du côté client.

### Mise à jour plus complexe :

Chaque fois que du contenu ou des données changent, le site doit être rebuild pour régénérer les pages statiques. Cela peut prendre du temps, surtout pour des sites volumineux avec de nombreuses pages.
Pour des applications où les données changent fréquemment (ex. : un site de news ou une application e-commerce avec des prix qui fluctuent), cette approche est peu flexible.

### Temps de build prolongé :

Plus un site contient de pages, plus la phase de build peut devenir longue et coûteuse en ressources. Sur des sites volumineux, chaque modification (même mineure) entraîne la régénération de nombreuses pages, ce qui peut ralentir considérablement le processus de développement et de mise en production.

### Problèmes d’interactivité sans JavaScript :

Bien que les pages soient rendues très rapidement, elles sont statistiques, ce qui signifie qu'elles sont limitées en termes de fonctionnalités interactives. Pour ajouter des fonctionnalités interactives, il faut charger des scripts JavaScript additionnels, ce qui peut ralentir l’expérience utilisateur et réduire certains des avantages de performance de SSG.

Sur un site en SSG, bien que les pages soient statiques lors du chargement initial, l’hydratation permet d’ajouter une couche d’interactivité via JavaScript, de la même façon que pour le SSR. Ainsi, même des actions comme l’ajout au panier sont possibles grâce à des appels API et une mise à jour dynamique du DOM. Ce modèle hybride (pages statiques + hydratation) permet d’offrir à la fois des performances élevées et une expérience utilisateur interactive sans compromettre les avantages du SSG.


# Client Side Rendering (CSR)

Le CSR diffère des deux autres approches en ce sens que la génération du HTML se fait entièrement dans le navigateur de l'utilisateur, à l'aide de JavaScript. Le serveur envoie initialement une page HTML vide ou presque, accompagnée d'un bundle JavaScript qui s'exécute ensuite pour générer dynamiquement le contenu de la page.

Cette approche est courante avec les frameworks JavaScript modernes comme Vue.js ou React, où l'accent est mis sur l'interactivité et les applications à page unique (SPA).

## Étapes du processus CSR :

  1. Le navigateur envoie une requête au serveur.
  2. Le serveur renvoie une page HTML de base et un bundle JS.
  3. Le navigateur exécute le JS pour remplir dynamiquement le DOM.

## Avantages du CSR

### Interactivité fluide :

Le CSR permet une expérience utilisateur très fluide grâce à la gestion dynamique des mises à jour du DOM. Les interactions, comme les clics sur les boutons ou les saisies dans les formulaires, n'entraînent pas de rechargement complet de la page, ce qui rend les applications plus réactives.

### Chargement initial rapide après la première requête :

Une fois le bundle JavaScript chargé, les pages se chargent rapidement lors des navigations suivantes. Le contenu est mis à jour de manière dynamique sans nécessiter de nouveaux chargements de HTML, offrant une expérience utilisateur rapide et continue.

### Développement modulaire et réutilisation de composants :

Avec des frameworks comme React, Vue ou Angular, le CSR encourage une architecture basée sur des composants. Cela favorise la réutilisation du code, rend le développement plus efficace et facilite la maintenance des applications.

### Riche écosystème JavaScript :

Le CSR permet de tirer parti de l'écosystème JavaScript très vaste, avec de nombreuses bibliothèques et outils disponibles pour faciliter le développement et l'ajout de fonctionnalités.

## Inconvénients du CSR

### Mauvaise indexation par les moteurs de recherche (SEO) :

Le CSR peut poser des problèmes d'indexation pour le SEO, car les robots des moteurs de recherche ne rendent souvent pas le JavaScript. Si le contenu dépend de l'exécution de JavaScript pour être affiché, il peut ne pas être indexé correctement.

### Temps de chargement initial plus long :

Le temps de chargement initial peut être plus long car le navigateur doit télécharger le bundle JavaScript avant de rendre le contenu. Cela peut être frustrant pour les utilisateurs, en particulier sur des connexions lentes.

### Dépendance à JavaScript :

Si un utilisateur désactive JavaScript dans son navigateur, le site peut devenir complètement inutilisable. Cela représente un problème d'accessibilité, car certains utilisateurs peuvent ne pas avoir la capacité d'exécuter JavaScript.

### Coût de l'exécution côté client :

La charge de travail de l'exécution de l'application est transférée au client, ce qui peut affecter les performances sur des appareils moins puissants. Les utilisateurs sur des appareils plus anciens ou à faible puissance peuvent éprouver des ralentissements.

### Gestion des états complexes :

La gestion des états d'application dans le CSR peut devenir complexe, surtout lorsque plusieurs composants interagissent. Cela nécessite une bonne architecture et souvent l'utilisation de bibliothèques de gestion d'état (comme Redux pour React) pour maintenir la clarté et la prévisibilité de l'état de l'application.


# Principales différences selon plusieurs indicateurs
## Temps de chargement
### SSG :
Excellent. Les pages sont déjà rendues avant même que la requête ne soit faite.
### SSR :
Variable. Le rendu se fait à la demande, ce qui peut introduire des latences.
### CSR :
Lent au chargement initial (le temps d’exécuter le bundle JS), mais rapide par la suite grâce à la mise à jour dynamique du DOM.

## SEO
### SSG et SSR :
Très bon. Le contenu est pré-rendu côté serveur, ce qui facilite l'indexation par les moteurs de recherche.
### CSR :
Mauvais.
Les moteurs de recherche peinent à indexer les pages qui nécessitent l'exécution de JavaScript pour afficher le contenu.

## Localisation du rendu
### SSG et SSR :
Le rendu est effectué côté serveur.
### CSR :
Le rendu est effectué côté client.

## Coût d'hébergement
### SSG :
Faible, car tout est pré-généré et les pages sont servies directement sans traitement supplémentaire.
### CSR :
Faible, car seuls des fichiers statiques (HTML, CSS, JS) sont servis.
### SSR :
Élevé, car chaque requête nécessite un rendu côté serveur, ce qui peut augmenter la charge et les coûts d'infrastructure.

## Navigation
### CSR :
Très fluide grâce à la mise à jour dynamique du DOM, sans rechargement de la page.
### SSG :
Moins fluide, car les pages doivent être rechargées, mais le contenu est déjà prêt.
### SSR :
Moins bonne, car chaque interaction entraîne un rechargement et une génération de la page.

## Personnalisation
### CSR :
Très flexible. Le JavaScript côté client permet de personnaliser l'interface en fonction des actions ou des données utilisateur.
### SSR :
Flexible aussi, mais dépend des informations envoyées dans la requête client.
### SSG :
Limitée. Les pages étant statiques, la personnalisation est quasi impossible sans avoir recours à des scripts client.

# Modes de rendu hybrides
Face aux limites des modes de rendu traditionnels, des solutions hybrides ont été développées pour combiner les avantages de chaque approche. Ces modes hybrides permettent d'améliorer les performances, le SEO et l'expérience utilisateur.

## SSR + CSR
Dans cette configuration, le serveur génère une première version du HTML pour permettre un rendu rapide et une bonne indexation SEO. Ensuite, le JavaScript côté client prend le relais pour ajouter des fonctionnalités dynamiques et rendre l'expérience utilisateur plus interactive. Cela permet d’obtenir le meilleur des deux mondes : un bon SEO et une interactivité fluide.

## SSG + CSR
Similaire au mode précédent, mais cette fois, le HTML est généré au moment du build et non à chaque requête. Ce modèle est idéal pour les sites avec des contenus qui changent peu, mais nécessitant des interactions dynamiques. Cela réduit la charge serveur, tout en offrant une bonne performance et un SEO optimisé.

## SSG + SSR
Ici, les pages statiques sont générées lors du build pour les parties du site peu changeantes. Pour les pages nécessitant un contenu dynamique ou personnalisé, le SSR est utilisé. Cela permet une flexibilité maximale, en profitant des performances des pages statiques et de la dynamique des pages rendues côté serveur.

# Conclusion
Le choix du mode de rendu dépend des besoins spécifiques de chaque projet. Le SSR reste une solution fiable pour les sites dynamiques nécessitant une personnalisation à la volée, tandis que le SSG est idéal pour les sites statiques ayant besoin de performances optimales. Le CSR, quant à lui, est essentiel pour les applications web riches et interactives.

Les solutions hybrides offrent la possibilité de combiner ces approches pour maximiser les avantages de chacune. En tant que développeur, il est essentiel de bien comprendre ces modes de rendu pour choisir celui qui correspond le mieux aux besoins de votre projet et à ceux de vos utilisateurs.

