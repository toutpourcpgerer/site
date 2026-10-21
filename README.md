# Tout pour Cpgérer — site Hugo publié par Cloudflare Pages

Ce dépôt contient le site web. Tu peux gérer le contenu depuis le navigateur, avec l'interface GitHub. **Tu n'as pas besoin d'installer Hugo ni Git sur ton ordinateur.** Cloudflare exécute Hugo sur ses propres serveurs à chaque mise à jour.

## 1. Mettre le projet sur GitHub

1. Crée un dépôt GitHub vide.
2. Décompresse cette archive sur ton ordinateur.
3. Dans le dépôt GitHub, clique sur **Add file → Upload files** et téléverse le contenu du dossier `tout-pour-cpgerer` (les dossiers `content`, `layouts`, `assets`, `static`, ainsi que `hugo.toml` et `README.md`). Il faut téléverser les fichiers du projet, pas seulement l'archive ZIP.
4. Clique sur **Commit changes**.

## 2. Relier GitHub à Cloudflare Pages

Dans Cloudflare, ouvre **Workers & Pages → Create → Pages → Connect to Git** et sélectionne le dépôt GitHub.

Paramètres de compilation :

- **Framework preset** : Hugo (ou configuration personnalisée si Hugo n'est pas proposé)
- **Build command** : `hugo --minify`
- **Build output directory** : `public`
- **Production branch** : `main` si c'est le nom de la branche principale de ton dépôt

La commande `hugo --minify` est lancée **par Cloudflare**, pas par ton ordinateur. Elle construit les pages HTML à partir des fichiers du dépôt. Après un commit GitHub, Cloudflare relance normalement la compilation et publie le site.

Dans `hugo.toml`, remplace `https://example.pages.dev/` par l'adresse réelle de ton site Cloudflare, avec un `/` final. Tu peux faire cette modification directement dans GitHub avec le bouton de modification du fichier.

## 3. Ajouter un PDF et sa page manuellement

Chaque PDF et chaque page HTML sont ajoutés séparément : **aucune page n'est créée automatiquement à partir du nom d'un PDF**. Tu choisis toi-même la rubrique, le titre, la description et le contenu de chaque page.

### Téléverser le PDF

1. Dans GitHub, ouvre `static/pdfs/`.
2. Clique sur **Add file → Upload files**.
3. Téléverse le PDF final, puis clique sur **Commit changes**.

Exemple de chemin : `static/pdfs/corrige-centrale-pc-2025.pdf`. L'adresse publique sera `https://TON-SITE.pages.dev/pdfs/corrige-centrale-pc-2025.pdf`.

### Créer la page HTML

1. Ouvre le dossier correspondant, par exemple `content/annales/`.
2. Clique sur **Add file → Create new file**.
3. Crée un fichier Markdown, par exemple `corrige-centrale-pc-2025.md`.
4. Utilise cette structure et personnalise tous les champs :

```markdown
---
title: "Corrigé de Centrale PC 2025"
date: 2026-10-21
lastmod: 2026-10-21
description: "Corrigé détaillé de Centrale PC 2025 : méthodes et résultats expliqués."
tags: ["annales", "corrigé", "PC"]
draft: false
pdf: "/pdfs/corrige-centrale-pc-2025.pdf"
---

## Présentation

Présente ici l'épreuve, les exercices et les principales méthodes utilisées.

## Notions abordées

- Première notion importante.
- Deuxième notion importante.

## Résultat à retenir

Par exemple, tu peux écrire une formule qui sera rendue dans la page HTML par MathJax :

$$
\\sum_{k=0}^{n} q^k = \\frac{1-q^{n+1}}{1-q}, \qquad q \\ne 1.
$$
```

Vérifie que la valeur de `pdf` correspond exactement au nom du fichier téléversé. La page HTML affichera le texte, les formules MathJax, un lecteur PDF intégré et un lien de téléchargement. Enregistre la page avec **Commit changes**.

Pour une page de cours sans PDF, crée simplement un fichier dans `content/cours/` et retire la ligne `pdf`. Pour une fiche de méthode, utilise `content/methodes/`. Tu peux créer d'autres rubriques, mais il faudra alors adapter le menu et les modèles si tu veux les afficher dans la navigation.

## 4. Contrôler les rubriques et les pages d'accueil

Les fichiers `content/cours/_index.md`, `content/annales/_index.md` et `content/methodes/_index.md` décrivent les pages de rubrique. Modifie-les directement sur GitHub pour ajuster leur titre et leur introduction. Les pages publiées apparaissent dans leur rubrique selon les modèles du site ; les fichiers avec `draft: true` ne sont pas publiés.

Les fichiers `exemple-...md` sont des modèles de démonstration laissés en brouillon. Copie leur structure pour créer tes pages, ou supprime-les quand tu n'en as plus besoin.

## MathJax et PDF : deux rôles différents

- **MathJax** affiche les formules écrites en LaTeX dans le texte HTML, par exemple `\\(e^x\\)` ou un bloc `$$ ... $$`.
- **LaTeX sur ton ordinateur** sert à compiler tes fichiers `.tex` en PDF. Continue de faire cette compilation comme d'habitude, puis téléverse uniquement le PDF final dans `static/pdfs/`.
- **Hugo sur Cloudflare** transforme les fichiers Markdown en pages HTML et publie le site. Tu n'as pas à lancer Hugo toi-même.

## Référencement

Rédige une description utile pour chaque page, explique réellement le contenu du document et crée des liens entre les ressources connexes. Une publication ou un sitemap ne garantit pas l'indexation par Google. Conserve Google Sites et Blogger pendant la transition, le temps de vérifier le nouveau site.

Liens utiles :
- Hugo : https://gohugo.io/documentation/
- Cloudflare Pages : https://developers.cloudflare.com/pages/
- Google Search Console : https://search.google.com/search-console/
