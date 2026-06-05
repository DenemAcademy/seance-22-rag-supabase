# Seance 22 - Moments importants

- Video : `2026-06-05 15-27-56.mp4`
- Duree detectee : 00:42:13
- Transcription brute : `seance-22-creer-un-rag-transcription.txt`
- Segments JSON : `seance-22-creer-un-rag-segments.json`

## Timeline propre

- **00:00 - section 01** : Un RAG sert à donner de la mémoire. Je pars d'un besoin simple : un chatbot sans mémoire répond trop large. Avec un RAG, je lui donne les documents du client comme contexte.
- **00:01 - section 11** : Je pars d'un compte Supabase. Je peux utiliser un compte existant ou créer un compte. Le plan gratuit suffit pour apprendre et pour un premier prototype.
- **00:03 - section 21** : Le bouton Connect ouvre la suite. Dans le projet Supabase, Connect me permet de brancher des clients, dont un agent via MCP.
- **00:04 - section 31** : Le dossier sources est la base du travail. J'ai préparé un dossier de documents restaurant. C'est ce dossier que Codex doit comprendre.
- **00:06 - section 36** : Je donne le premier prompt de compréhension. Je demande à Codex de comprendre les documents et de se mettre en tête qu'on va créer un RAG simple.
- **00:13 - section 41** : Je lance le cadrage du schéma RAG. Après la lecture, je demande le schéma logique : projets, documents, chunks, tests, règles et vues.
- **00:29 - section 51** : Table Editor montre les données. Une fois les tables créées, je peux voir les lignes : projets, documents, chunks, tests.
- **00:21 - section 61** : Le chatbot récupère plusieurs chunks. Une réponse fiable peut combiner plusieurs morceaux : politique, FAQ, procédure et script.
- **00:16 - section 71** : Je découpe la demande avant l'outil. Je commence toujours par la demande : le client veut-il mémoire, automatisation, création, analyse ou interface ?
- **00:38 - section 76** : Je fais un contrôle avant de continuer. Avant de brancher le chatbot, je vérifie la base. Sinon, l'interface masquera les problèmes du corpus.
- **00:38 - section 77** : Je garde un prompt de reproduction. La compétence devient scalable quand je peux répéter la méthode avec variables client, secteur, objectif et documents.

## Prompts importants

### Section 36 - Prompt de découverte des documents

```text
Comprends tous les documents présents dans ce dossier.
Ensuite, mets-toi en tête que nous allons créer un RAG très simple.

Contexte :
- Le client est un restaurant.
- Le futur chatbot devra répondre grâce aux documents fournis.
- Je veux comprendre les sources avant de créer les tables.

Ce que j'attends :
1. Liste les documents trouvés.
2. Explique à quoi chaque document va servir dans le RAG.
3. Propose les grandes catégories de connaissances.
4. Ne crée encore rien dans Supabase.
```

### Section 41 - Prompt de cadrage RAG

```text
Tu vas m'aider à construire un RAG Supabase pour un chatbot restaurant.

Objectif :
Transformer les documents du dossier en corpus exploitable.

Contraintes :
- Garde une trace du fichier source.
- Découpe en chunks courts et utiles.
- Prépare les métadonnées pour filtrer par audience : client, équipe, manager.
- Prévois des tests de retrieval pour vérifier que les bonnes sources ressortent.

Avant d'écrire le SQL, propose le schéma logique et explique les tables.
```

### Section 51 - Prompt pour pousser le SQL et les tables

```text
Tu es connecté au projet Supabase RAG CLIENT.

Pousse maintenant le schéma dans Supabase :
- crée les tables nécessaires ;
- insère les documents ;
- insère les chunks ;
- ajoute les métadonnées utiles ;
- crée les vues de lecture ;
- crée les tests de retrieval ;
- vérifie que le Schema Visualizer montre des relations propres.

Important :
Ne mets aucun secret dans les tables.
Garde les sources traçables.
Explique ensuite ce que tu as créé.
```

### Section 61 - Prompt de test retrieval

```text
Teste le RAG avec ces demandes :

1. Un client demande s'il peut venir avec une allergie sévère.
2. Un client veut réserver pour un groupe privé.
3. Un client demande les horaires en terrasse.
4. Un manager veut savoir quelles règles appliquer pour une demande VIP.

Pour chaque test :
- indique les chunks retrouvés ;
- cite les fichiers sources ;
- dis si la réponse est assez fiable ;
- propose une correction si le retrieval est faible.
```

### Section 76 - Prompt de contrôle avant livraison

```text
Fais un contrôle final de mon RAG Supabase.

Vérifie :
- nombre de documents ;
- nombre de chunks ;
- sources sans contenu ;
- chunks trop longs ou trop courts ;
- tests de retrieval en échec ;
- vues exposées côté client ;
- risques de sécurité ou de données sensibles.

Rends-moi :
1. un diagnostic court ;
2. les corrections prioritaires ;
3. une checklist de livraison client.
```

### Section 77 - Prompt réutilisable pour un nouveau client

```text
Je veux reproduire ce système RAG pour un nouveau client.

Client : [NOM_CLIENT]
Secteur : [SECTEUR]
Objectif du chatbot : [OBJECTIF]
Documents fournis : [LISTE_DOCUMENTS]
Audience principale : [CLIENTS / EQUIPE / MANAGERS]
Contraintes sensibles : [RGPD / PRIX / SANTE / VIP / AUTRE]

Construis-moi :
- le plan de corpus ;
- les tables Supabase ;
- les métadonnées ;
- les tests de retrieval ;
- les points de sécurité ;
- la checklist de livraison.
```
