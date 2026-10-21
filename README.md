# Tout pour Cpgérer — site Hugo

Site statique en français, pensé pour être géré depuis l'interface web de GitHub, sans installer Hugo ni Git sur l'ordinateur. Cloudflare Pages construit le site à chaque mise à jour du dépôt.

## Configuration Cloudflare Pages

- Branche de production : `main` (ou la branche principale réelle du dépôt)
- Commande de build : `hugo --minify`
- Répertoire de sortie : `public`
- Framework : Hugo

Dans `hugo.toml`, la valeur `baseURL` est encore réglée sur l’ancienne adresse `workers.dev`. Si tu publies désormais sur une adresse `pages.dev`, remplace-la par l’adresse exacte du projet Pages pour que les URL canoniques soient correctes.

La commande `hugo --minify` s'exécute sur les serveurs de Cloudflare, pas sur l'ordinateur. Elle transforme les fichiers Markdown et les modèles HTML en site publiable.

## Personnaliser l'apparence

- `assets/css/main.css` : couleurs, typographie, espaces, cartes et responsive mobile.
- `layouts/index.html` : contenu et structure de la page d'accueil.
- `layouts/partials/header.html` : marque et menu principal.
- `layouts/partials/footer.html` : liens et pied de page.
- `layouts/_default/list.html` : présentation des rubriques.
- `layouts/_default/single.html` : modèle des pages individuelles, dont le lecteur PDF.
- `hugo.toml` : titre, description et liens du site.

Palette actuelle : bleu clair, doré et noir. La marque affichée est un monogramme typographique temporaire ; si tu as le fichier image de ton logo original, ajoute-le dans `static/` puis adapte `layouts/partials/header.html`.

## Ajouter une ressource manuellement

1. Dans GitHub, ouvre `static/pdfs/` et téléverse le PDF.
2. Crée toi-même un fichier Markdown dans le dossier de la bonne rubrique :
   - `content/fiches-chimie/`
   - `content/annales-centrale/`
   - `content/informatique-physico-chimique/`
3. Ajoute le titre, le résumé, le texte et le chemin du PDF dans les métadonnées du fichier.
4. Enregistre : Cloudflare Pages reconstruira le site automatiquement.

**Important : déposer un PDF ne crée aucune page automatiquement.** Les pages sont créées et classées manuellement.

### Modèle de page Markdown avec PDF

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

Le champ `pdf` est facultatif. S'il est renseigné, la page affiche un lecteur PDF et un bouton de téléchargement. MathJax rend les formules LaTeX écrites dans le contenu HTML. MathJax ne compile pas un fichier `.tex` en PDF : compile le PDF séparément puis téléverse-le dans `static/pdfs/`.

## Liens externes

Le lien Blogger est configuré dans `hugo.toml`. Le lien Instagram peut être ajouté au paramètre `instagramURL` lorsque l'URL souhaitée est connue.
