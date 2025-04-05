# Plan de Développement : Site de Poésie avec Administration via GitHub Token

---

## Vue d'ensemble

Un site web statique en **français** pour publier vos poèmes, avec une interface d'administration sécurisée par un **token GitHub** (utilisé comme mot de passe, jamais stocké).  
Le site sera **responsive** (mobile & desktop, 16:9 et 9:16) et permettra la **recherche** dans les poèmes.

---

## Architecture Globale

```mermaid
flowchart TD
    subgraph Site Public
        A[HTML/CSS/JS statique]
        B[Poèmes (Markdown/JSON)]
        C[Recherche]
        A --> C
        A --> B
    end

    subgraph Dépôt GitHub
        B
    end

    subgraph Page Admin
        D[Connexion avec Token GitHub]
        E[Validation du Token via API GitHub]
        F[Gestion Poèmes (Ajouter/Modifier/Supprimer)]
        G[Push via API GitHub]
        D --> E --> F --> G --> B
    end

    Page Admin -->|Fetch| Dépôt GitHub
    Site Public -->|Fetch| Dépôt GitHub
```

---

## Étapes détaillées

### 1. Création du site public

- **Langue** : Français
- **Design** : Minimaliste, agréable, adapté à la poésie
- **Responsive** : Compatible mobile (vertical/horizontal) et desktop
- **Organisation** :
  - Par titre, date, tags (optionnel)
  - Affichage clair et structuré
- **Recherche** :
  - JavaScript côté client
  - Filtrage par mots-clés, titre, date, tags
- **Stockage des poèmes** :
  - Fichiers Markdown individuels dans `/poems/`
  - Ou un fichier unique `poems.json`

---

### 2. Stockage des poèmes

- **Format Markdown** (préféré pour la mise en forme) ou JSON
- Métadonnées :
  - Titre
  - Date
  - Contenu
  - Tags (optionnel)

---

### 3. Développement de la page d'administration

- **Page séparée** (`/admin.html`)
- **Connexion** :
  - Formulaire pour entrer le token GitHub
- **Vérification du token** :
  - Appel API GitHub (ex: `GET /user` ou `GET /repos/:owner/:repo`)
  - Si succès, accès accordé
  - Sinon, erreur
- **Gestion des poèmes** :
  - Lister les poèmes
  - Ajouter un poème (formulaire)
  - Modifier un poème
  - Supprimer un poème
- **Intégration API GitHub** :
  - Utiliser le token pour créer/modifier/supprimer des fichiers via REST API
  - Commits directs dans le dépôt (mise à jour automatique du site via GitHub Pages)

---

### 4. Sécurité

- **Token jamais stocké** (ni localement, ni côté serveur)
- **Présent uniquement en mémoire navigateur**
- **Utiliser HTTPS** pour sécuriser la transmission
- **Token à portée limitée** (accès contenu repo uniquement recommandé)

---

### 5. Hébergement

- **GitHub Pages** pour héberger le site statique
- **Page admin** dans le même repo (protégée par vérification token)
- **Option** : héberger la page admin ailleurs pour plus de sécurité

---

## Résumé

| Élément            | Détail                                                      |
|--------------------|--------------------------------------------------------------|
| **Frontend**       | HTML/CSS/JS statique, responsive, en français               |
| **Backend**        | Aucun, tout via API GitHub côté client                      |
| **Auth Admin**     | Token GitHub entré à chaque session, vérifié via API        |
| **Gestion Poèmes** | CRUD via API GitHub                                         |
| **Hébergement**    | GitHub Pages                                                |
| **Sécurité**       | Token non stocké, session uniquement                        |

---

## Prochaines étapes

1. Initialiser le dépôt GitHub avec la structure de base
2. Développer le site public (index.html, style, affichage poèmes, recherche)
3. Développer la page admin (login, vérification token, gestion poèmes)
4. Intégrer API GitHub pour modifications
5. Tester l’ensemble
6. Améliorer design et expérience utilisateur
7. Documenter l’utilisation

---