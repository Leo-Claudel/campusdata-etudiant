# Dossier de conception - équipe à renseigner

**Membres :** à renseigner. **Version du dossier / commit :** à renseigner.
**Date de revue :** à renseigner. **Relecteur :** à renseigner.

Cette trame se complète dès S1 puis évolue avec les décisions réellement prises.
Remplacer les consignes par vos réponses ; conserver les limites utiles.
Ne pas recopier tout l’énoncé : expliquer son application à votre réalisation.

## 1. Besoin et utilisateurs

Rédiger cinq phrases : utilisateur, problème, action principale, donnée durable,
limite du prototype. Décrire ensuite un parcours de démonstration et un cas d’erreur.
Préciser que le responsable déclaré n’est pas un compte authentifié.

- Problème observé : à renseigner.
- **Résultat attendu** par le commanditaire : à renseigner.
- Périmètre obligatoire retenu : à renseigner à partir des US du contrat.
- Exclusions et extensions éventuelles : à renseigner.

## 2. Backlog et critères d’acceptation

| ID | En tant que… je veux… afin de… | Priorité | Étant donné / Quand / Alors | Responsable | Test/preuve |
|---|---|---|---|---|---|
| US à renseigner | Besoin utilisateur | Priorité | **Résultat observable** | Membre | Référence |

Pour chaque US, décomposer réalisation, validation et documentation en tâches.
Prévoir un critère négatif lorsqu’il existe un refus attendu. Une tâche n’est
terminée qu’après observation et revue de son résultat.

## 3. Maquettes et interactions

Insérer écran principal et édition. Annoter champs, labels, boutons et messages.
Documenter états vide, chargement, succès et erreur ainsi que le parcours clavier.
Décrire ce qui reste saisi après un échec, la confirmation de suppression et
l’absence de requête lorsque l’utilisateur annule.

## 4. Architecture et flux

Produire les diagrammes de composants, séquence de création et déploiement.
Ajouter une séquence de refus de transition avec l’emplacement du **rollback**.
Indiquer les ports, noms réseau, frontières poste/conteneur/VM et **stockage durable**.

| Contexte | Point d’entrée utilisateur | Accès API | Accès DB depuis API | Lieu du stockage |
|---|---|---|---|---|
| Développement | À relever | À relever | À relever | À relever |
| Compose | À relever | À relever | À relever | À relever |
| **k3d** | À relever | À relever | À relever | À relever |
| AWS/K3s | À relever | À relever | À relever | À relever |

## 5. Données et contrat

Présenter le dictionnaire des trois tables (datasets, ingestions, measurements),
types, **contraintes SQL**, clés étrangères et **valeurs par défaut**. Expliquer qui
produit UUID et **horodatages**, quelles valeurs peuvent être nulles, et quelle
contrainte d’unicité rend l’ingestion idempotente.

Ajouter la matrice des statuts d’un dépôt, les règles de contrôle d’une ligne CSV,
les routes et des exemples HTTP : création d’un jeu, dépôt accepté (202), relance
refusée (409), fichier trop volumineux (413) et suppression sans corps de réponse.
Expliquer 404, 409, 413, 415, 422, 503 et le traitement d’une erreur inattendue.

## 6. Découpage du code et transactions

| Module | Responsabilité | Dépendances | Invariant/commentaire important | Test associé |
|---|---|---|---|---|
| À renseigner | Une responsabilité précise | Modules utilisés | Règle protégée | Scénario |

Préciser le responsable du **commit**, le **rollback**, la fermeture des sessions,
le **verrou de ligne** et la sérialisation. Décrire l’initialisation explicite et
la limite de create_all face à une évolution de schéma.

## 7. Décisions argumentées

| Décision | Option retenue | Alternative étudiée | Motif concret | Conséquence/limite | Preuve ou référence |
|---|---|---|---|---|---|
| À renseigner | Choix | Alternative | Contrainte satisfaite | Coût ou risque accepté | Référence |

Une préférence seule ne justifie pas un choix. Relier la décision au temps,
au contrat, à la reproductibilité ou au comportement observé.

## 8. Risques et mesures

| Risque | Effet utilisateur | Détection | Mesure prévue | Limite restante |
|---|---|---|---|---|
| Panne API | À compléter | À compléter | À compléter | À compléter |
| Panne DB | À compléter | À compléter | À compléter | À compléter |
| Perte du nœud | À compléter | À compléter | À compléter | À compléter |
| **Secret** exposé | À compléter | À compléter | À compléter | À compléter |
| Ressource cloud oubliée | À compléter | À compléter | À compléter | À compléter |

## 9. Validation croisée

Noter qui a relu le dossier, quelles ambiguïtés ont été trouvées et corrigées.
Identifier les différences entre conception initiale et réalisation finale.
Conserver les questions non résolues et leurs effets, sans les présenter comme validées.

## Exemple de justification à adapter

**Exemple de forme, à relier à votre réalisation :** « Nous utilisons une session
par requête pour séparer les transactions des utilisateurs. La dépendance ferme
la session même si une erreur remonte. Nous vérifions que l’ingestion est
idempotente en redéposant le même fichier puis en relisant le nombre de mesures. »

Ajoutez le nom de votre module, le test correspondant et la limite observée.
Ne reprenez pas cette explication si votre implémentation utilise une autre
organisation : décrivez alors son fonctionnement réel.
