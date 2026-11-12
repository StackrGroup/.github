# Contribuer aux dépôts StackrGroup

Ces règles valent pour tout dépôt de l'organisation, pour toute personne qui contribue, interne ou
externe, et pour les agents IA. Le guide d'un dépôt n'y ajoute que ce qui lui est propre, et
l'emporte en cas d'écart.

## Avant de commencer

- Un ticket, Jira ou à défaut issue GitHub « Spec », n'entre en développement que s'il est
  **prêt**. Son PRD est la seule spec du changement et n'est plus maintenu après la livraison. Le
  formulaire d'issue « Spec » reprend la liste ci-dessous champ par champ : toute modification de
  l'une s'applique à l'autre.
  - Le contexte et le comportement attendu.
  - Les critères d'acceptation au format EARS, un par ligne, numérotés (CA1, CA2…), chacun un
    scénario de test avec sa donnée et son résultat observable :
    `Quand <événement>, l'application <réponse>`, `Tant que <état>, …`, `Si <condition>, alors …`,
    `Là où <option>, …` ou `L'application doit …`, dont au moins un `Si …, alors …` d'erreur ou de
    refus.
  - Le hors-scope, y compris ce qui doit rester identique.
  - Le comportement de l'application remplacée s'il y en a une, la maquette si le ticket touche un
    écran.
  - Des dépendances levées (ADR « Accepté » si une décision d'architecture est en jeu), trois
    jours-homme au plus, ni secret ni donnée client.
  - Un PRD de 30 à 50 lignes de Markdown, hors titres du formulaire et réponses « Sans objet » ;
    au-delà de 50, le ticket est à découper.
- Dans un dépôt équipé de la fabrique IA, l'étiquette `claude`, posée par une personne qui a le
  droit d'écriture, confie l'issue à la fabrique : Claude ouvre une pull request en brouillon, ou
  répond par des questions si l'issue n'est pas prête. Claude ne fusionne jamais. Poser l'étiquette,
  c'est répondre du contenu de l'issue telle qu'elle est, même écrite par quelqu'un d'autre : la
  relire avant.
- Installation locale : voir le README du dépôt.

## Branches et commits

- `main` est protégée : aucun push direct.
- Une branche courte par ticket, préfixée par la clé Jira : `GDM2-123-bouton-primaire`. Un travail
  sans ticket Jira (outillage, CI, documentation, issue « Spec ») prend le type de commit en
  préfixe : `ci/release`.
- Commits au format [Conventional Commits](https://www.conventionalcommits.org/fr/) (`feat:`, `fix:`,
  `chore:`…). Le versioning en dépend.

## Pull requests

- Une préoccupation par PR, liée à son ticket Jira (clé dans le nom de la branche et dans la
  description). Un travail sans ticket Jira l'indique dans la description : « sans ticket », ou
  « sans ticket (issue #N) » pour une issue « Spec ».
- Titre au format Conventional Commits : il devient le message du commit de squash.
- Avant d'ouvrir la PR, jouer les vérifications indiquées dans le README du dépôt : la CI rejoue les
  mêmes.
- Avant le merge : CI au vert, revue IA (CodeRabbit) traitée (chaque remarque corrigée ou justifiée,
  et son fil résolu), relecture humaine selon le risque de la PR.
- Merge en squash uniquement.
- Un comportement qui change en profondeur met à jour, dans la même PR, le contexte du module et
  l'ADR s'il y a lieu.

## Relecture selon le risque

La section « Impacts » du modèle de PR donne le risque. En cas de doute, le niveau supérieur
s'applique, et le relecteur peut relever le niveau annoncé.

| Risque | PR                                                                                                               | Relecture                                                                                                                                      |
| ------ | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Faible | Aucun comportement ne change : documentation, outillage de développement, refactorisation couverte par les tests | CodeRabbit traité ; une approbation si les règles du dépôt l'imposent. Renovate fusionne seul les mises à jour que son preset autorise.        |
| Normal | Un comportement change, aucune case d'impact cochée                                                              | Approuvée par un autre développeur que l'auteur                                                                                                |
| Élevé  | Au moins une case d'impact cochée                                                                                | Approuvée par un autre développeur qui connaît la partie touchée, et qui vérifie chaque ligne d'impact : migration, isolation des tenants, ADR |

## Rédiger la PR

Le [modèle de PR](pull_request_template.md) sert deux lecteurs : le développeur qui relit le code, puis
la QA qui recette le ticket. Une section sans objet le dit (« aucune », « sans objet ») au lieu d'être
supprimée.

- **Vérifications faites** : une ligne par critère d'acceptation du ticket, avec le test Xray qui le
  décrit (sans objet pour une issue « Spec ») et le test automatisé qui le joue (toujours exigé). La
  vérification manuelle dit ce qui a été joué, où et avec quelles données.
  Captures avant et après dès qu'un écran change, sans donnée client.
- **Recette** : de quoi rejouer le comportement en recette sans lire le code : prérequis, données,
  étapes.
- **Impacts** : chaque case cochée porte une ligne d'explication. Dans un produit multi-tenant, toute
  PR qui lit ou écrit des données de tenant prouve par un test qu'un tenant ne voit pas les données
  d'un autre, et toute migration de base s'applique à tous les tenants. Une rupture de compatibilité
  se déclare aussi dans le commit (`!` et `BREAKING CHANGE:`), ce qui fixe la version majeure.
- **Non-régression** : l'auteur, qui connaît le code touché, liste les parcours existants qu'il a pu
  affecter indirectement (composant, service, table ou workflow partagés) et les tests Xray à rejouer.
  La QA complète en recette. « Aucune » n'est valable que si la PR ne touche rien de partagé.

Un ticket n'est **terminé** qu'une fois mergé, couvert par des tests automatisés sur ses critères
d'acceptation, et validé par la QA en recette.

## Versions et publication

- Semver calculé à partir des commits : `fix` → patch, `feat` → mineure, rupture → majeure.
- Release Please tient la PR de release et le changelog ; sa fusion crée le tag, qui déclenche la
  publication. Aucun tag à la main ; une publication échouée se relance sur le tag existant.

## Dépendances et sécurité

- Versions exactes, sans `^` ni `~` ; lockfiles versionnés, installation en `npm ci` et
  `dotnet restore --locked-mode`. Versions NuGet centralisées dans `Directory.Packages.props`.
- Actions GitHub épinglées par SHA, images Docker par digest.
- Renovate propose les mises à jour, avec le preset commun de
  [shared-workflows](https://github.com/StackrGroup/shared-workflows).
- Jamais de secret ni de donnée client dans le code, les tests, les fixtures, les tickets ou
  Confluence. Chaque dépôt cherche les secrets au pre-commit (secretlint) et en CI (gitleaks) ; aucun
  outil ne repère les données client, c'est à l'auteur et au relecteur d'y veiller.
