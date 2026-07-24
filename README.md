# Mon Projet

Site web statique déployé automatiquement via CI/CD.

**URLs en ligne :**
- Vercel : https://ci-cd-rho-virid.vercel.app
- GitHub Pages : https://mohameden19961.github.io/mon-projet/

## Comment ça marche

Tu modifies un fichier (`index.html`, `style.css` ou `script.js`), tu fais `git push`, et le site se met à jour automatiquement sur Vercel et GitHub Pages.

---

## Depuis zéro : étapes complètes

### 1. Créer les fichiers du projet

```
mon-projet/
├── index.html
├── style.css
├── script.js
├── package.json
├── .stylelintrc.json
├── eslint.config.js
└── .github/
    └── workflows/
        └── ci-cd.yml
```

### 2. Initialiser Git

```bash
git init
git branch -m master main
```

### 3. Créer le repo GitHub et pousser

```bash
gh repo create mon-projet --public --source=. --remote=origin --push
```

### 4. Activer GitHub Pages

```bash
gh api repos/mohameden19961/mon-projet/pages -X POST -f build_type=workflow
```

### 5. Déployer sur Vercel

```bash
vercel --yes --prod
```

Vercel connecte le repo GitHub automatiquement. Les prochains push déclenchent un re-déploiement.

### 6. Workflow CI/CD

Le fichier `.github/workflows/ci-cd.yml` fait tout automatiquement :

- **Push sur `main`** → lint (HTML, CSS, JS) → déploiement
- **Pull Request** → lint seul (pas de déploiement)

---

## Commandes utiles

```bash
# Voir les runs du workflow
gh run list --repo mohameden19961/mon-projet

# Voir les logs d'un run
gh run view <ID> --repo mohameden19961/mon-projet --log

# Redéployer manuellement sur Vercel
vercel --yes --prod

# Redéployer manuellement via GitHub Actions
gh workflow run ci-cd --repo mohameden19961/mon-projet
```

---

## Linters

Les linters vérifient le code à chaque push :

| Outil | Fichier vérifié |
|-------|-----------------|
| htmlhint | `**/*.html` |
| stylelint | `**/*.css` |
| eslint | `**/*.js` |

Pour lancer les linters en local :

```bash
npm install
npm run lint:html
npm run lint:css
npm run lint:js
```
