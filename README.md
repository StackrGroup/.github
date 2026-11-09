# .github

Fichiers par défaut des dépôts StackrGroup : GitHub les applique à tout dépôt de l'organisation qui
n'a pas le sien.

| Fichier                                                              | Rôle                            |
| -------------------------------------------------------------------- | ------------------------------- |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                                 | Règles communes pour contribuer |
| [`pull_request_template.md`](pull_request_template.md)               | Modèle de description des PR    |
| [`.github/ISSUE_TEMPLATE/spec.yml`](.github/ISSUE_TEMPLATE/spec.yml) | Formulaire d'issue « Spec »     |

- **Source des règles communes** : une règle qui vaut pour tous les dépôts se change ici, pas dans
  le guide d'un dépôt. Un dépôt qui a son propre `CONTRIBUTING.md` n'y met que ses spécificités et
  renvoie ici. La fabrique IA reçoit ce guide dans son prompt : une modification ici change son
  comportement dans tous les dépôts équipés.
- **Remplacement, pas fusion** : GitHub affiche le fichier d'un dépôt à la place de celui-ci. C'est
  pourquoi le guide d'un dépôt renvoie explicitement au guide commun. Pour les modèles d'issue, le
  remplacement porte sur tout le dossier : un dépôt qui a son propre `.github/ISSUE_TEMPLATE/`, même
  avec un seul `config.yml`, n'a plus le formulaire « Spec » commun.
- **Absents des clones** : ces fichiers n'existent que dans l'interface GitHub. Un outil ou un agent
  qui travaille sur un checkout ne les voit pas, sauf si on les lui donne, comme le fait la fabrique.
- **Dépôt public** : GitHub l'exige pour appliquer ces fichiers. Rien de confidentiel ici : ni nom de
  client, ni adresse d'infrastructure.
