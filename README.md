# ArtificialInquiries_4


Outil numérique pour l'exercice 4 — « Memorable Conversations » du vademecum
[*Artificial Inquiries*](https://hal.science/hal-05327878) (Alcaras, Ricci, Prinetti & de Vries, 2025, Éditions Annexes).

## 1. L'exercice papier

Le participant revient sur des conversations avec un LLM qui l'ont marqué (titres repérés à l'ex. 3b) :

1. Copier le titre de la conversation et décrire brièvement son contenu.
2. Expliquer pourquoi elle a marqué : émotion (excitation, frustration, amusement, peur…), question morale ou éthique, changement de point de vue sur les LLM, conséquences sur le travail.
3. Noter la performance du LLM de 1 (Terrible) à 5 (Excellent), l'évaluer par écrit, puis chercher pourquoi il a ainsi performé.

Sur papier, ces fiches restent difficiles à comparer, à filtrer ou à partager au sein d'un groupe ; c'est ce que l'outil numérique doit permettre.

## 2. Objectif de l'outil

Remplacer les fiches papier par une collection numérique où chaque conversation mémorable est une notice structurée, que l'on peut :

- saisir via un formulaire (une fiche = un item) ;
- filtrer et rechercher (par émotion, par note, par LLM, par catégorie de tâche) ;
- comparer entre participants d'un même groupe (le vademecum recommande le travail collectif).

## 3. Solution technique : Omeka S

[Omeka S](https://omeka.org/s/) est un CMS de gestion de collections, basé sur le web sémantique, qui convient bien à des notices structurées.

| Besoin | Fonction Omeka S |
|---|---|
| Une fiche = une conversation | **Item** |
| Fiche de saisie structurée | **Resource template** « Ex4 – Conversation mémorable » |
| Champs propres à l'exercice | **Vocabulaire personnalisé** (module *Custom Vocab* ou import d'un vocabulaire RDF) |
| Regrouper par participant ou par groupe | **Item sets** |
| Liste fermée (émotions, impact) | **Custom Vocab** de type liste |
| Note de 1 à 5 | module **Numeric Data Types** (*integer*) |
| Recherche et filtres | recherche avancée native (par propriété, classe, template) |
| Site de consultation | **Site** + thème (pages « navigation » et « parcourir les items ») |

### Modèle de données

Voir [`diagram_class.md`](diagram_class.md). Correspondance proposée avec les propriétés :

| Champ de l'exercice | Propriété (proposition) |
|---|---|
| Conversation Title | `dcterms:title` |
| Content | `dcterms:description` |
| Why it stood out | `ai:pourquoiMarquante` (texte long) |
| Émotion | `ai:emotion` (Custom Vocab : excitation, frustration, amusement, peur, autre) |
| Type d'impact | `ai:typeImpact` (Custom Vocab) |
| Score 1–5 | `ai:note` (numeric:integer) |
| Describe the performance | `ai:evaluationPerformance` (texte long) |
| Pourquoi cette performance | `ai:explicationPerformance` (texte long) |
| LLM utilisé | `ai:llm` (lien vers un item « LLM ») |
| Catégorie de tâche (ex. 3b) | `ai:categorieTache` |
| Participant | item set + `dcterms:creator` |

`ai:` est un préfixe de vocabulaire propre au projet, à créer (ex. `http://example.org/artificial-inquiries#`).

### Variante possible

Pour que les participants saisissent eux-mêmes leurs fiches sans accès à l'administration, étudier un module de contribution publique (par exemple *Contribute*) ; à vérifier selon la version d'Omeka S installée.

## 4. Installation locale d'Omeka S

Procédure officielle : <https://omeka.org/s/docs/user-manual/install/>. Prérequis (versions exactes à vérifier sur cette page) :

- serveur **Apache** (module `mod_rewrite` activé) ;
- **PHP** avec les extensions requises ;
- **MySQL** ou MariaDB ;
- ImageMagick (miniatures).

Étapes résumées :

1. Installer une pile locale (XAMPP, MAMP, WAMP ou Docker).
2. Créer une base de données et un utilisateur MySQL dédiés.
3. Télécharger l'archive Omeka S et la décompresser dans le dossier web (ex. `htdocs/omeka-s`).
4. Renseigner `config/database.ini` (hôte, base, utilisateur, mot de passe).
5. Ouvrir `http://localhost/omeka-s/` et créer le compte administrateur.
6. Installer les modules *Custom Vocab* et *Numeric Data Types* (dossier `modules/`, puis activation dans l'administration).

## 5. Mise en place pour l'exercice 4

1. **Vocabulaire** : créer le vocabulaire `ai:` (Vocabularies → Import) avec les propriétés du tableau ci-dessus.
2. **Custom Vocab** : créer les listes « Émotion » et « Type d'impact ».
3. **Resource template** « Ex4 – Conversation mémorable » : associer les propriétés, marquer comme obligatoires titre, description et note, choisir le type de donnée adapté à chaque champ.
4. **Item sets** : un par participant ou par groupe.
5. **Site** : créer un site public avec une page « Parcourir » filtrée sur le template.

## 6. Plan de test

| # | Test | Résultat attendu |
|---|---|---|
| 1 | Installation : connexion à l'administration | Tableau de bord accessible |
| 2 | Créer 3 items avec le template (exemples ci-dessous) | Fiches enregistrées, champs structurés |
| 3 | Saisir une note hors 1–5 (ex. 7) | Refusée ou signalée |
| 4 | Recherche avancée : `ai:note` ≥ 4 | Seules les conversations bien notées |
| 5 | Recherche par émotion = frustration | Fiches concernées |
| 6 | Ajouter les items à un item set « Participant A » | Regroupement visible sur le site |
| 7 | Consulter le site public | Fiches lisibles sans connexion |

### Données d'exemple

| Titre | Contenu | Pourquoi marquante | Émotion | Note |
|---|---|---|---|---|
| Traduction d'emails | Traduction d'emails pour un sommet économique | Le LLM a parfaitement saisi le registre | excitation | 5 |
| Traduction d'emails (échec) | Même sujet | Réponses vagues, hallucinations | frustration | 1 |
| Plat pour 60 personnes | Idées de plats pour un anniversaire | Réponse utile mais générique | amusement | 3 |

## 7. Structure du dépôt

```
ArtificialInquiries_04/
├── README.md
└── diagram_class.md
```

## 8. Références

- Alcaras, G., Ricci, D., Prinetti, T., & de Vries, Z. (2025). *Artificial Inquiries*. Éditions Annexes. CC BY-NC.
- Omeka S, manuel utilisateur : <https://omeka.org/s/docs/user-manual/>
- Mermaid, diagramme de classes : <https://mermaid.ai/open-source/syntax/classDiagram.html>
