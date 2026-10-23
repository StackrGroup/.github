# .github

Fichiers par défaut des dépôts StackrGroup : GitHub les applique à tout dépôt de l'organisation qui
n'a pas le sien.

| Fichier                                                | Rôle                            |
| ------------------------------------------------------ | ------------------------------- |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                   | Règles communes pour contribuer |
| [`pull_request_template.md`](pull_request_template.md) | Modèle de description des PR    |

- **gdm-2 sert de modèle** : ces fichiers reprennent son guide et son modèle de PR, sans ce qui ne vaut
  que pour New GDM. Une règle qui change là-bas se reporte ici.
- **Remplacement, pas fusion** : un dépôt qui a son propre fichier ignore celui-ci en entier.
- **Absents des clones** : ces fichiers n'existent que dans l'interface GitHub. Un outil ou un agent
  qui travaille sur un checkout ne les voit pas.
- **Dépôt public** : GitHub l'exige pour appliquer ces fichiers. Rien de confidentiel ici : ni nom de
  client, ni adresse d'infrastructure.
