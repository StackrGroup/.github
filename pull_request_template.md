<!-- Titre : format Conventional Commits, il devient le message du commit de squash.
     Rupture de compatibilité : `!` après le type (`feat!:`) et un pied `BREAKING CHANGE:`.
     Guide de rédaction : CONTRIBUTING.md, section « Rédiger la PR »
     (https://github.com/StackrGroup/.github/blob/main/CONTRIBUTING.md#rédiger-la-pr). -->

**Ticket** : <!-- clé Jira, ou « sans ticket » pour l'outillage, la CI ou la documentation -->

## Changements

<!-- Ce que fait la PR, et ce qu'elle ne fait pas (hors-scope du ticket). -->

## Vérifications faites

<!-- Ce que l'auteur a déjà vérifié, pour que la revue ne le refasse pas. -->

| Critère d'acceptation | Test Xray | Test automatisé                                  |
| --------------------- | --------- | ------------------------------------------------ |
| CA1 — …               |           | `Classe.Méthode` ou `fichier.spec.ts` › scénario |

- Vérification manuelle : <!-- parcours joué, où (local, pile Docker), avec quelles données ; « aucune » sinon -->
- Captures avant / après : <!-- dès qu'un écran change, avec le lien Figma ou Storybook de référence -->

## Recette

<!-- Pour la QA : prérequis, données, étapes pour constater le comportement en recette.
     « Sans objet » si rien n'est observable (outillage, refactorisation). -->

## Impacts

<!-- Cocher ce qui s'applique et préciser en une ligne. Rien de coché = aucun effet hors du ticket.
     Une case cochée relève le niveau de relecture : CONTRIBUTING.md, section « Relecture selon le risque ». -->

- [ ] Contrat d'API modifié (route, schéma, code d'erreur), ou entrées et sorties d'un workflow partagé :
- [ ] Rupture de compatibilité (API, données, configuration) :
- [ ] Migration de base, jouée pour tous les tenants : réversible ? reprise de données ? durée sur le plus gros tenant ?
- [ ] Données de tenant lues ou écrites : chaque accès est filtré par tenant, un test prouve qu'un tenant ne voit pas les données d'un autre
- [ ] Donnée ou réglage partagé entre tenants (référentiel, cache, file, stockage) :
- [ ] Configuration nouvelle ou action manuelle au déploiement (variable, secret, entrée Key Vault) :
- [ ] Brique transverse soumise à ADR (auth, session, GED, notifications, traductions, communication, files) :
- [ ] Écart volontaire avec le comportement de l'application que le produit remplace :
- [ ] Dépendance ajoutée, ou montée de version majeure :

**Non-régression** : <!-- Parcours ou modules existants touchés indirectement, et les tests Xray (clés ou plan
de test) que la QA rejoue au-delà du ticket. « Aucune » si la PR est isolée. -->

## Definition of Done

- [ ] Chaque critère d'acceptation est couvert par un test automatisé, rattaché à son test Xray.
- [ ] Chaque remarque de CodeRabbit est corrigée ou justifiée dans la PR.
- [ ] Le contexte du module, et l'ADR s'il y a lieu, sont à jour si le comportement change en profondeur.
- [ ] Aucun secret ni donnée client, y compris dans les fixtures et les captures.
