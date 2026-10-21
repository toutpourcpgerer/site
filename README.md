# Tout pour Cpgérer — site Hugo

Site statique en français, géré depuis GitHub.  
Cloudflare Pages reconstruit le site à chaque modification.

---

## Comment le sommaire est relié aux pages

### Règle d’or

| Dossier dans `content/` | URL sur le site | Lien dans le sommaire |
|-------------------------|-----------------|------------------------|
| `content/chimie/` | `/chimie/` | doit pointer vers `chimie/` |
| `content/chimie/annales/centrale/` | `/chimie/annales/centrale/` | doit pointer vers `chimie/annales/centrale/` |
| `content/lycee/livre-d-or/` | `/lycee/livre-d-or/` | doit pointer vers `lycee/livre-d-or/` |

**Le sommaire ne se met PAS à jour tout seul.**  
Il est écrit à la main dans le fichier :

```
layouts/partials/header.html
```

Quand tu ajoutes, renommes ou supprimes un dossier dans `content/`,  
tu dois aussi modifier ce fichier pour que les liens restent justes.

### Où modifier le sommaire

1. Ouvre `layouts/partials/header.html` sur GitHub
2. Cherche la zone `sidebar-nav` (le menu latéral)
3. Chaque lien ressemble à ceci :

```html
<a href="{{ "chimie/" | relURL }}">Chimie</a>
```

- `chimie/` = chemin du dossier dans `content/` (sans le mot `content`)
- `Chimie` = texte affiché dans le menu

Pour ajouter un lien :

```html
<a href="{{ "mon-nouveau-dossier/" | relURL }}">Mon titre</a>
```

Pour supprimer un lien : efface toute la ligne `<a ...>...</a>`.

---

## Organisation actuelle (alignée sur le Google Sites)

```
content/
├── _index.md                          → Accueil (/)
│
├── chimie/                            → Chimie
│   ├── _index.md
│   └── annales/
│       ├── centrale/                  → Annales Centrale
│       │   └── corrige_cen_pc_24.md
│       └── MinesPC/                   → Annales Mines PC
│           └── corrige_mines_pc_2024_chimie.md
│
├── agregation-physique-chimie/        → Agrégation Physique-Chimie
│   ├── _index.md
│   ├── physique/
│   ├── informatique/
│   └── mathematiques/
│
├── integration/                       → Intégration
│
├── lycee/                             → Lycée
│   ├── _index.md
│   ├── liens-utiles/
│   └── livre-d-or/
│
└── informatique-physico-chimique/     → Informatique physico-chimique
```

C’est la même ossature que le menu du Google Sites :

- Accueil
- Chimie
- Agrégation Physique-Chimie (Physique, Informatique, Mathématiques)
- Intégration
- Lycée (Liens utiles, Livre d’or)

---

## Comment créer une nouvelle page

### 1. Créer le dossier (si besoin)

Exemple : une nouvelle fiche de chimie  
→ crée le fichier dans `content/chimie/` (ou un sous-dossier).

### 2. Créer le fichier Markdown

Exemple : `content/chimie/equilibres.md`

```toml
+++
title = "Équilibres chimiques"
date = 2026-10-21
summary = "Fiche de révision sur les équilibres."
pdf = "/pdfs/equilibres.pdf"   # optionnel
+++

## À retenir

Ton texte ici…
```

### 3. (Optionnel) Ajouter le lien dans le sommaire

Si tu veux que la page apparaisse dans le menu latéral,  
ajoute une ligne dans `layouts/partials/header.html`.

Sinon, elle sera listée automatiquement sur la page de sa rubrique  
(ex. : toutes les pages de `content/chimie/` apparaissent sur `/chimie/`).

### 4. PDF

1. Téléverse le PDF dans `static/pdfs/`
2. Indique le chemin dans le front matter : `pdf = "/pdfs/nom.pdf"`

---

## Fichiers importants

| Fichier | Rôle |
|---------|------|
| `layouts/partials/header.html` | **Sommaire + menu** (à modifier quand tu changes la structure) |
| `layouts/partials/footer.html` | Pied de page |
| `layouts/_default/list.html` | Affichage d’une rubrique (liste des pages) |
| `layouts/_default/single.html` | Affichage d’une page individuelle + lecteur PDF |
| `layouts/index.html` | Page d’accueil |
| `assets/main.css` | Apparence (couleurs, tailles, sommaire rétractable) |
| `hugo.toml` | Titre du site, liens Instagram / Blogger |
| `content/` | **Toutes tes pages** |
| `static/pdfs/` | Fichiers PDF |

---

## Configuration Cloudflare Pages

- Branche : `main`
- Commande de build : `hugo --minify`
- Répertoire de sortie : `public`

---

## En cas de lien cassé dans le sommaire

1. Vérifie que le dossier existe bien dans `content/`
2. Ouvre `layouts/partials/header.html`
3. Corrige le chemin dans le `href="{{ "chemin/" | relURL }}"`
4. Enregistre → Cloudflare reconstruit le site
