# Tout pour Cpgérer — site Hugo

Site statique en français, pensé pour être géré depuis l’interface web de GitHub, **sans installer Hugo ni Git** sur ton ordinateur.  
Cloudflare Pages reconstruit le site automatiquement à chaque modification.

---

## Structure des dossiers (à ne pas renommer)

| Dossier     | Rôle                                      | Comment le voir |
|-------------|-------------------------------------------|-----------------|
| `assets/`   | Mise en page (fichier CSS)                | Style du site   |
| `content/`  | Pages (fichiers Markdown)                 | Contenu         |
| `layouts/`  | Structure HTML des pages                   | Templates       |
| `static/`   | Fichiers fixes (PDF, images, favicon…)    | Fichiers        |
| `archetypes/` | Modèles pour créer de nouvelles pages   | Squelettes      |

**Important :** ne renomme pas ces dossiers. Hugo les cherche par leur nom exact.

---

## Configuration Cloudflare Pages

- **Branche de production** : `main`
- **Commande de build** : `hugo --minify`
- **Répertoire de sortie** : `public`
- **Framework** : Hugo

---

## Personnaliser l’apparence

| Fichier | Ce qu’il contrôle |
|---------|-------------------|
| `assets/main.css` | Couleurs, polices, espacements, cartes, mobile |
| `layouts/index.html` | Page d’accueil |
| `layouts/partials/header.html` | Logo + menu |
| `layouts/partials/footer.html` | Pied de page |
| `layouts/_default/list.html` | Liste d’une rubrique |
| `layouts/_default/single.html` | Page d’une ressource + lecteur PDF |
| `hugo.toml` | Titre, description, liens Instagram/Blogger |

Palette actuelle : bleu clair, doré et noir.

---

## Ajouter une ressource manuellement

1. Dans GitHub, ouvre `static/pdfs/` et **téléverse le PDF**.
2. Crée un fichier Markdown dans la bonne rubrique :
   - `content/fiches-chimie/`
   - `content/annales-centrale/`
   - `content/informatique-physico-chimique/`
3. Remplis le front matter (voir modèle ci-dessous).
4. Enregistre → Cloudflare reconstruit le site automatiquement.

**Important :** déposer un PDF ne crée **aucune page** automatiquement.  
Chaque page doit être créée manuellement.

### Modèle de page avec PDF

Crée par exemple `content/fiches-chimie/equilibres-chimiques.md` :

```toml
+++
title = "Équilibres chimiques"
date = 2026-10-21
summary = "Une fiche pour réviser les équilibres chimiques."
pdf = "/pdfs/equilibres-chimiques.pdf"
+++

## À retenir

Ajoute ici ta présentation, les explications et les formules.

$$
K^\circ = \prod_i a_i^{\nu_i}
$$
```

- Le champ `pdf` est **facultatif**.
- S’il est renseigné, un lecteur PDF et un bouton de téléchargement apparaissent.
- MathJax affiche les formules LaTeX écrites dans le contenu.

---

## Liens externes

Les liens Blogger et Instagram sont configurés dans `hugo.toml` (section `[params]`).

---

## En cas de problème de build

Si Cloudflare affiche une erreur liée à `minify` ou `resources.Get` :

1. Vérifie que le fichier CSS s’appelle bien `main.css`
2. Vérifie qu’il se trouve bien dans le dossier `assets/` (pas `assets/css/`)
3. Dans `layouts/_default/baseof.html`, la ligne doit être :

```
{{ $style := resources.Get "main.css" | minify | fingerprint }}
```
