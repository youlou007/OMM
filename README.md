# OMM - Site de Poésie

Un site web en français pour publier et gérer vos poèmes, avec une interface d'administration sécurisée par un token GitHub.

---

## Fonctionnalités

- Affichage élégant et responsive de tous les poèmes
- Recherche et filtrage des poèmes
- Interface d'administration protégée par token GitHub
- Ajout, modification et suppression des poèmes via API GitHub
- Hébergement via GitHub Pages

---

## Structure du projet

- `index.html` — Page publique affichant les poèmes
- `admin.html` — Interface d'administration
- `style.css` — Feuille de style commune
- `poems/` — Dossier contenant les fichiers de poèmes (Markdown ou JSON)
- `project_plan.md` — Plan détaillé du projet

---

## Instructions

1. Accédez à la page publique pour lire les poèmes.
2. Accédez à `/admin.html` et connectez-vous avec votre token GitHub pour gérer les poèmes.
3. Les modifications sont directement poussées dans ce dépôt via l'API GitHub.

---

## Sécurité

- Le token GitHub n'est **jamais stocké**.
- Il est utilisé uniquement en mémoire lors de la session d'administration.
- Utilisez un token avec des permissions limitées (accès contenu repo uniquement).

---
