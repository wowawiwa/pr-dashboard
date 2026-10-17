# PR Dashboard

Une carte de tes pull requests GitHub ouvertes : une ligne par repo, une colonne pour tes PR, une pour les reviews qu'on te demande.

Page : https://wowawiwa.github.io/pr-dashboard/

## Ce que fait la page

- **Mes PR** sont triées de la plus avancée à la moins avancée : approuvées, retour reçu, en attente de review, rien demandé. Des badges ronds, alignés sur toutes les cartes, disent ce qui manque : draft, review en attente, avis, checks, conflit. Le survol explique chaque badge.
- **Reviews demandées** montre d'abord celles qui te visent nommément, puis celles faites à ton équipe, de la plus ancienne à la plus récente. Des liens mènent aux PR que tu as déjà reviewées ou commentées.
- **Post** met une PR de côté en bas de sa case. **Masquer** la cache jusqu'à son prochain mouvement.

## Token

La page appelle l'API GitHub directement depuis le navigateur, sans serveur. Elle n'enregistre jamais le token. Il vit dans ton gestionnaire de mots de passe, puis dans la mémoire de l'onglet, et il n'est envoyé qu'à `api.github.com`. Fermer l'onglet l'oublie.

À l'ouverture, la page affiche un formulaire de connexion avec un seul champ. Pour que Bitwarden le remplisse, crée un identifiant avec le token comme mot de passe et `https://wowawiwa.github.io/pr-dashboard/` comme URI. Bitwarden le remplit alors avec son raccourci (Cmd+Shift+L), depuis son menu dans le champ, ou tout seul si tu actives pour cet identifiant le remplissage automatique au chargement. La page démarre dès que le champ est rempli.

Ta liste de repos et tes PR en post ou masquées restent dans le localStorage du navigateur. Rien de tout ça n'est sensible.

Les réglages proposent deux liens de création pré-remplis :

- un token fine-grained en lecture seule, limité à un seul owner. Selon l'org, il peut demander l'approbation d'un owner ;
- un token classique avec les scopes `repo` et `read:org`, si l'org bloque les tokens fine-grained ou si les checks restent vides.

## Développement

Un seul fichier, `index.html`, sans dépendance ni build. Pour tester le rendu sans token, passe une réponse de la requête `prdash.query` à `prdash.render(json)` dans la console.
