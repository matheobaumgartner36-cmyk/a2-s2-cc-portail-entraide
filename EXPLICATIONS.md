# A2 – S2 – CC : portail d'entraide

**Nom : Baumgartner — Prénom : Mathéo**

Compte GitHub : `matheobaumgartner36-cmyk`. Les nouveaux commits utilisent mon nom et l'adresse GitHub de confidentialité `233692853+matheobaumgartner36-cmyk@users.noreply.github.com`.

## Départ et branches

L'archive fournie a été extraite entièrement avec son dossier `.git`, sans `git init`. Au départ, le répertoire de travail était propre, aucun dépôt distant n'était configuré et seules les branches `main` et `feature/tutorat` existaient.

- Premier commit de l'histoire : `4a266e1954639271093546da34fcc2178914ced2` (portail et simulateur).
- Pointe de `main` à l'ouverture et départ commun des deux propositions : `76184a8471759fd1f9062c1ae17bec5e0254b7bc`.
- Contribution fournie de tutorat : `a43f314846d7fe8135144e80d3881ccd385d4c3d`, conservée sans recréation.

| Branche conservée | Point de départ | Rôle et commit |
| --- | --- | --- |
| `feature/accueil` | `76184a8` | Modifier le paragraphe existant pour annoncer l'accueil libre sans inscription le jeudi à 16 h : `1e0ffa95cac666d7f2d1dae96eaa7099888b0126`. |
| `feature/contact` | `76184a8` | Rendre `entraide@example.org` cliquable avec `mailto:` : `08ed6c4e33f7670e76691623eb1a074145fa6a88`. |
| `feature/tutorat` | `76184a8`, dans l'histoire fournie | Apporter le tutorat individuel sur inscription le jeudi à 16 h 30 : `a43f314846d7fe8135144e80d3881ccd385d4c3d`. |
| `hotfix/duree` | `f7ca1472c416b6a193cb46297c3473e2363de803`, après intégration | Annuler uniquement l'erreur de durée : `51ba8cb6fb60554f246bf18b0e707b1acaa0c55b`. |

Les deux branches personnelles ont été créées avant toute intégration. `main` est resté sur `76184a8` jusqu'à l'enregistrement des deux propositions. L'accueil a été intégré en avance rapide, puis le contact par la fusion `7bc55e90ea4ee8b69f93b41b07f1a9931c6e9f93`.

## Conflit réellement rencontré

La fusion de `feature/tutorat` dans `main` a produit `CONFLICT (content)` et `UU index.html`. Les histoires avaient divergé : depuis `76184a8`, l'accueil et le tutorat remplaçaient différemment le même paragraphe `permanence`. Git ne pouvait pas choisir le contenu à conserver.

La résolution a remplacé le bloc de conflit par deux paragraphes distincts : accueil libre sans inscription à 16 h, puis tutorat individuel sur inscription à 16 h 30. Le lien de contact et les autres sections ont été conservés. La fusion terminée est `f7ca1472c416b6a193cb46297c3473e2363de803` ; ses parents sont `7bc55e9` et le commit fourni `a43f314`. Aucun marqueur de conflit ni opération Git inachevée ne subsiste.

## Annulation ciblée

Le commit partagé `b88cc98bf3fae11998895be8365305f22b2cc49c` avait changé `dureeCreneau` de 20 à 200. Sur `hotfix/duree`, la commande `git revert --no-edit b88cc98bf3fae11998895be8365305f22b2cc49c` a créé le nouveau commit d'annulation `51ba8cb6fb60554f246bf18b0e707b1acaa0c55b`.

Ce commit ne modifie que la durée dans `app.js`. Il ne supprime aucun commit et ne réécrit pas l'histoire. La réparation a été réunie dans `main` par `9b7b5e0b507958a410752d8391b13d323b9223bf`. Le conseil du README, ajouté après l'erreur, reste inchangé, ainsi que les deux permanences et le contact.

## Tests attendus et observés

Tests effectués par Codex dans le navigateur, avant modification sur `76184a8`, puis après réparation sur `9b7b5e0`. Les propositions accueil et contact ont aussi été vérifiées séparément sur leurs branches avant fusion.

| Test | Résultat correct attendu | Avant : résultat observé | Après : résultat observé |
| --- | --- | --- | --- |
| Durée affichée | 20 minutes | 200 minutes : erreur confirmée | 20 minutes : conforme |
| Ouverture de la page | 0 créneau, 0 minute | 0 / 0 | 0 / 0 |
| Un clic sur Ajouter | 1 créneau, 20 minutes | 1 / 200 | 1 / 20 |
| Deux clics sur Ajouter | 2 créneaux, 40 minutes | 2 / 400 | 2 / 40 |
| Recommencer | 0 créneau, 0 minute | 0 / 0 | 0 / 0 |
| Ajouter puis actualiser | Retour à 0 / 0 | 0 / 0 | 0 / 0 |
| Permanences | Les deux modalités distinctes | Paragraphe générique à 16 h | Accueil libre à 16 h et tutorat sur inscription à 16 h 30 |
| Contact | Lien `mailto:entraide@example.org` | Texte simple | Lien présent ; destination contrôlée dans le navigateur |

Aucun courriel n'a été envoyé au contact de démonstration. Le lancement d'une application de messagerie n'a pas été testé. Aucune erreur de console n'a été observée lors des tests finaux. Le conseil de vérification du README est identique à celui du départ.

## Difficultés et contrôles

Le seul conflit Git a été celui attendu dans `index.html`, résolu et vérifié ci-dessus. Le contrôle des espaces a initialement signalé les fins de ligne Windows déjà utilisées dans les fichiers ; le réglage local `core.whitespace=cr-at-eol` a permis de les conserver, puis `git diff --check` a réussi. L'aperçu local et l'accès réseau ont nécessité une relance avec les autorisations d'exécution adaptées ; les tests de navigateur ont ensuite abouti. Aucun autre incident de contenu n'a été constaté.

## Publication et aides

Le dépôt public est [a2-s2-cc-portail-entraide](https://github.com/matheobaumgartner36-cmyk/a2-s2-cc-portail-entraide). Son accès sans authentification et ses cinq branches ont été vérifiés : `main`, `feature/accueil`, `feature/contact`, `feature/tutorat` et `hotfix/duree`. Les identifiants distants des quatre branches de tâche correspondent à ceux du tableau.

Juste avant l'ajout de ce document, `main` local et `main` sur GitHub pointaient tous deux sur `9b7b5e0b507958a410752d8391b13d323b9223bf`. L'identifiant final incluant ce document sera fourni dans le message de remise après une nouvelle comparaison : il ne peut pas être écrit dans le commit qui le crée. Le contrôle de l'histoire conserve tous les commits fournis et les nouveaux commits ; le README est inchangé et le simulateur a retrouvé la durée du premier commit.

**Aide utilisée :** Codex a exécuté les opérations Git, préparé les modifications, effectué les tests décrits et rédigé ce document à ma demande. Les tests effectués par l'assistant ne sont pas présentés comme des tests personnels.

**Vérifications personnelles déclarées :** j'ai confirmé mon identité et le compte GitHub à utiliser. J'ai confié les manipulations et les vérifications fonctionnelles à Codex ; je ne déclare pas avoir réalisé moi-même ces tests ni rédigé seul ce document.
