# ArtificialInquiries_4 — Memorable Conversations

Exercice 4 du protocole **Artificial Inquiries** (Vademecum, septembre 2025, bloc *Qualifying*), transformé en outil numérique dans le cadre du cours *Langages du Web* (Master THYP, Université Paris 8).

Compte GitHub : `lenaisi`

🔗 **Application en ligne :** https://lenaisi.github.io/ArtificialInquiries_4/response.html

## 1. Description de l'exercice

L'exercice invite à revenir sur des conversations avec un LLM qui ont laissé une impression durable :
1. Noter le **titre** de la conversation et décrire brièvement son **contenu**.
2. Expliquer **pourquoi elle a marqué** : émotion ressentie (enthousiasme, frustration, amusement, peur…), questions morales ou éthiques, changement de point de vue sur les LLM, conséquences sur le travail.
3. **Noter la performance** du LLM de 1 (très mauvaise) à 5 (excellente), l'évaluer brièvement et expliquer pourquoi il a eu cette performance.

## 2. Solutions techniques

| Besoin | Solution |
|---|---|
| Stockage des données | **Omeka S** en local (Apache + PHP + MySQL avec XAMPP) |
| Vocabulaire | Vocabulaire **artinq** (`artificial_inquiries.ttl`), espace de noms `https://humanum-p8.fr/omk_artificialinquiries/onto/artinq#` |
| Modèle de données | Diagramme de classes (`diagram_class.md`) traduit en **6 modèles de ressources** Omeka S (`resource-template/`) |
| Communication avec Omeka S | **API REST** d'Omeka S |
| Interface CRUD | `response.html` en **HTML / CSS / JavaScript**, publiée avec **GitHub Pages** |
| Authentification | Local (clé API Omeka S), GitHub (jeton d'accès) |
| Diagrammes | **Mermaid** |
| Versionnement | **Git / GitHub** |

## 3. Modèle de données

| Classe | Rôle |
|---|---|
| **ConversationMemorable** | La conversation : titre, contenu, pourquoi elle a marqué, note, évaluation et explication de la performance |
| **Participant** | La personne qui fait l'exercice |
| **LLM** | Le modèle utilisé (ChatGPT, Claude…) |
| **Emotion** | L'émotion ressentie |
| **TypeImpact** | Le type d'impact (émotionnel, éthique, professionnel…) |
| **CategorieTache** | La catégorie de tâche (traduction, rédaction, code…) |

## 4. Fichiers du dépôt

| Fichier / dossier | Contenu |
|---|---|
| `README.md` | Ce document |
| `response.html` | Interface CRUD de l'exercice (GitHub Pages) |
| `diagram_class.md` | Diagramme de classes Mermaid |
| `artificial_inquiries.ttl` | Vocabulaire **artinq** |
| `resource-template/` | Les 6 modèles de ressources Omeka S |
| `omk.sql` | Export de la base de données Omeka S locale |

## 5. Interface CRUD (`response.html`)

- Un onglet par classe : **lister**, **afficher**, **créer**, **modifier** et **supprimer** des items via l'API REST d'Omeka S.
- Les formulaires sont générés à partir des modèles de ressources ; les liens (participant, LLM, émotion…) se choisissent dans des listes.
- **Authentification** : Local (email + clé API Omeka S, lecture et écriture), GitHub (jeton d'accès personnel, lecture seule). Google et CAS : non configurés.

**Utilisation :** démarrer XAMPP (Apache + MySQL), ouvrir la page en ligne, indiquer l'adresse de l'API (`http://localhost/omeka-s/api/`) et se connecter.

**Configuration CORS :** des en-têtes `Access-Control-Allow-*` ont été ajoutés au fichier `.htaccess` d'Omeka S pour autoriser la page GitHub Pages à appeler l'API locale.

## 6. Utilisation de l'IA

Ce travail a été réalisé avec l'aide de l'IA générative **Claude** (Anthropic), utilisée pour la préparation des modèles de ressources et de l'interface `response.html`. J'ai moi-même conçu le diagramme de classes et le vocabulaire, configuré Omeka S, importé les fichiers, créé et vérifié les items de test, puis mis le travail en ligne.
