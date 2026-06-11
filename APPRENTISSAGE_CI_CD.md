# 📚 Programme d'Apprentissage CI/CD - Niveau Débutant

**Étudiant** : Mamadou Djoulde Djoulde  
**Domaine** : Génie Logiciel  
**Durée** : 2-3 semaines  
**Rythme** : 30-60 minutes par jour

---

## 🎯 Objectif Global

Apprendre la CI/CD (Intégration Continue & Déploiement Continu) avec GitHub Actions, de zéro jusqu'à créer des workflows complets et automatisés.

---

## 📅 Semaine 1 : Les Fondamentaux

### **Jour 1-2 : Concepts de base**

**Objectifs d'apprentissage :**
- Comprendre ce qu'est la CI/CD
- Pourquoi c'est important dans le développement moderne
- Différence entre CI, CD et DevOps
- Voir des exemples concrets dans des projets réels

**À retenir :**
- **CI (Intégration Continue)** : Automatiser les tests et vérifications à chaque commit
- **CD (Déploiement Continu)** : Automatiser le déploiement en production
- Gain : Détection rapide des bugs, déploiements plus fréquents, confiance accrue

**Ressources :**
- https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions

**Exercice :**
- Lis la documentation
- Note 3 exemples réels de CI/CD que tu trouves online

---

### **Jour 3-4 : GitHub Actions - Introduction**

**Objectifs d'apprentissage :**
- Naviguer dans l'interface GitHub Actions
- Comprendre la structure d'un workflow
- Apprendre les concepts clés : jobs, steps, actions
- Savoir où placer les fichiers

**Concepts clés :**
- **Workflow** : Le fichier YAML qui définit l'automatisation
- **Job** : Une unité de travail (par exemple : "test", "build", "deploy")
- **Step** : Une étape dans un job (par exemple : "installer les dépendances", "exécuter les tests")
- **Action** : Une réutilisable (ex : actions/checkout, actions/setup-python)
- **Événement** : Ce qui déclenche le workflow (push, pull_request, schedule, etc.)

**Structure d'un fichier :**
```yaml
name: Mon Premier Workflow
on: push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: echo "Hello World"
```

**Où placer les fichiers :**
```
mon-repo/
├── .github/
│   └── workflows/
│       └── mon-workflow.yml
├── src/
└── README.md
```

**Ressources :**
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions

**Exercice :**
- Ouvre un repository existant ou crée-en un nouveau
- Crée le dossier `.github/workflows/`
- Note les 5 concepts clés sur un papier

---

### **Jour 5-6 : Ton premier workflow simple**

**Objectifs d'apprentissage :**
- Créer ton premier fichier `.yml`
- Déclencher une action sur `push`
- Afficher "Hello World"
- Vérifier les logs

**Étapes :**

1. **Crée le fichier** `.github/workflows/hello.yml`

2. **Ajoute ce contenu :**
```yaml
name: Hello World Workflow

on:
  push:
    branches: [ main, master ]

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - name: Afficher Hello World
        run: echo "Hello World! Je suis en train d'apprendre la CI/CD"
```

3. **Fais un commit et push** vers GitHub

4. **Vérifie l'exécution :**
   - Va dans ton repository
   - Clique sur l'onglet "Actions"
   - Clique sur le workflow qui s'est exécuté
   - Vérifie les logs

**Exercice :**
- Modifie le message "Hello World" par ton nom
- Crée un 2e step qui affiche la date
- Fais un push et vérifie dans GitHub Actions

---

### **Jour 7 : Premiers tests**

**Objectifs d'apprentissage :**
- Exécuter des commandes basiques
- Tester un script simple
- Consulter l'historique des exécutions

**Étapes :**

1. **Crée un script Python simple** `hello.py` :
```python
def greet(name):
    return f"Bonjour {name}!"

if __name__ == "__main__":
    print(greet("Mamadou"))
```

2. **Mets à jour ton workflow** `.github/workflows/hello.yml` :
```yaml
name: Test Python

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: python hello.py
```

3. **Fais un commit et push**

4. **Vérifie les logs dans GitHub Actions**

**Exercice :**
- Crée un script Python/Node.js qui fait un calcul simple
- Ajoute-le à ton workflow
- Vérifie que ça s'exécute correctement

---

## 📅 Semaine 2 : Tests et Automatisation

### **Jour 8-9 : Tester du code**

**Objectifs d'apprentissage :**
- Installer des dépendances
- Exécuter une suite de tests
- Afficher les résultats

**Exemple avec Python (pytest) :**

1. **Crée** `test_hello.py` :
```python
from hello import greet

def test_greet():
    assert greet("Mamadou") == "Bonjour Mamadou!"

def test_greet_empty():
    assert greet("") == "Bonjour !"
```

2. **Crée** `requirements.txt` :
```
pytest==7.0.0
```

3. **Mets à jour** `.github/workflows/hello.yml` :
```yaml
name: Test Python

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install -r requirements.txt
      - run: pytest -v
```

4. **Push et vérifie**

**Exemple avec Node.js (Jest) :**

1. **Package.json** :
```json
{
  "scripts": {
    "test": "jest"
  },
  "devDependencies": {
    "jest": "^29.0.0"
  }
}
```

2. **Workflow** :
```yaml
name: Test Node.js

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm test
```

**Exercice :**
- Crée une suite de tests pour ton code
- Configure le workflow pour les exécuter
- Ajoute un 2e test qui échoue, puis corrige-le
- Vérifie que tout passe dans GitHub Actions

---

### **Jour 10-11 : Linting et Formatage**

**Objectifs d'apprentissage :**
- Vérifier la qualité du code
- Formater automatiquement
- Bloquer les PR si le code ne passe pas

**Python - Pylint et Black :**

1. **requirements.txt** :
```
pylint==2.16.0
black==22.12.0
pytest==7.0.0
```

2. **Workflow** `.github/workflows/quality.yml` :
```yaml
name: Code Quality

on: [push, pull_request]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - run: pip install -r requirements.txt
      - run: black --check .
      - run: pylint *.py
      - run: pytest
```

**Node.js - ESLint et Prettier :**

1. **Package.json** :
```json
{
  "scripts": {
    "lint": "eslint .",
    "format": "prettier --write ."
  },
  "devDependencies": {
    "eslint": "^8.0.0",
    "prettier": "^3.0.0"
  }
}
```

2. **Workflow** :
```yaml
name: Code Quality

on: [push, pull_request]

jobs:
  quality:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm install
      - run: npm run lint
      - run: npm test
```

**Exercice :**
- Configure le linting pour ton projet
- Crée du code mal formaté et vérifie que le workflow le détecte
- Corrige le code et vérifie que ça passe

---

### **Jour 12-13 : Variables et Secrets**

**Objectifs d'apprentissage :**
- Utiliser des variables d'environnement
- Stocker des secrets (API keys, tokens)
- Les utiliser dans ton workflow

**Variables d'environnement :**

```yaml
name: Variables Demo

on: push

env:
  ENVIRONMENT: production

jobs:
  demo:
    runs-on: ubuntu-latest
    env:
      JOB_VAR: "valeur au niveau du job"
    steps:
      - run: echo "Environment: $ENVIRONMENT"
      - run: echo "Job Var: $JOB_VAR"
      - name: Step with env
        env:
          STEP_VAR: "valeur au niveau du step"
        run: echo "Step Var: $STEP_VAR"
```

**Secrets :**

1. **Va dans ton repository** → Settings → Secrets and variables → Actions

2. **Crée un secret** (ex : `MY_SECRET_TOKEN`)

3. **Utilise-le dans le workflow** :
```yaml
name: Secrets Demo

on: push

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Token: ${{ secrets.MY_SECRET_TOKEN }}"
```

**Exercice :**
- Crée 2 variables (DEBUG_MODE, PROJECT_NAME)
- Crée 1 secret (MY_API_KEY)
- Affiche-les dans un workflow
- Vérifie que les secrets ne s'affichent pas en clair dans les logs

---

### **Jour 14 : Construire des artefacts**

**Objectifs d'apprentissage :**
- Créer une archive/build
- Stocker les résultats
- Télécharger les artefacts

**Exemple :**

```yaml
name: Build Artifacts

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Créer un artefact
        run: |
          mkdir -p build
          echo "Mon artefact build" > build/output.txt
      
      - name: Upload artefact
        uses: actions/upload-artifact@v3
        with:
          name: mon-artefact
          path: build/
      
      - name: Download artefact (pour vérification)
        uses: actions/download-artifact@v3
        with:
          name: mon-artefact
          path: downloaded/
```

**Exercice :**
- Crée un workflow qui compile du code
- Stocke le résultat comme artefact
- Vérifie dans GitHub Actions que tu peux télécharger l'artefact

---

## 📅 Semaine 3 : Déploiement & Cas Réels

### **Jour 15-16 : Déclencher des workflows**

**Objectifs d'apprentissage :**
- Différents événements de déclenchement
- Conditions et filtres
- Workflows paramétrés

**Événements :**

```yaml
name: Différents Déclencheurs

on:
  push:
    branches: [ main, develop ]
    paths:
      - 'src/**'
      - 'tests/**'
  pull_request:
    branches: [ main ]
  schedule:
    - cron: '0 9 * * MON'  # Tous les lundis à 9h UTC
  workflow_dispatch:  # Déclenchement manuel

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Workflow déclenché!"
```

**Conditions :**

```yaml
name: Conditions

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    if: github.event_name == 'push'
    steps:
      - run: echo "Ceci n'exécute que sur push"
  
  deploy:
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - run: echo "Ceci n'exécute que sur la branche main"
```

**Exercice :**
- Crée un workflow déclenché manuellement (workflow_dispatch)
- Crée un workflow qui s'exécute uniquement sur la branche main
- Crée un workflow programmé pour s'exécuter une fois par jour

---

### **Jour 17-18 : Cas réels - Application Node.js**

**Objectifs d'apprentissage :**
- Pipeline complet : Installer → Linter → Tests → Build

**Workflow complet** `.github/workflows/nodejs-pipeline.yml` :

```yaml
name: Node.js Pipeline

on: [push, pull_request]

jobs:
  pipeline:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [16.x, 18.x]
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      
      - name: Install dependencies
        run: npm install
      
      - name: Lint code
        run: npm run lint
      
      - name: Run tests
        run: npm test
      
      - name: Build
        run: npm run build
      
      - name: Upload build artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build-${{ matrix.node-version }}
          path: dist/
```

**Exercice :**
- Applique ce workflow à un projet Node.js existant
- Ajoute des étapes pour la couverture de code
- Teste avec plusieurs versions de Node.js

---

### **Jour 19-20 : Cas réels - Application Python**

**Objectifs d'apprentissage :**
- Pipeline complet pour Python
- Tests avec couverture
- Multiversion

**Workflow complet** `.github/workflows/python-pipeline.yml` :

```yaml
name: Python Pipeline

on: [push, pull_request]

jobs:
  pipeline:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        python-version: ['3.9', '3.10', '3.11']
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install pytest pytest-cov
      
      - name: Lint with Pylint
        run: pylint **/*.py
      
      - name: Format check with Black
        run: black --check .
      
      - name: Run tests with coverage
        run: pytest --cov=. --cov-report=xml
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage.xml
```

**requirements.txt** :
```
pytest==7.0.0
pytest-cov==4.0.0
pylint==2.16.0
black==22.12.0
```

**Exercice :**
- Applique ce workflow à un projet Python existant
- Ajoute une vérification de type avec mypy
- Configure la couverture de code minimale à 80%

---

### **Jour 21 : Projet Capstone**

**Objectif final :**
Créer un workflow complet et automatisé pour **TON** projet personnel

**Checklist à accomplir :**

- [ ] Repository créé et initialisé
- [ ] Dossier `.github/workflows/` en place
- [ ] Fichier de workflow principal créé
- [ ] Gestion des dépendances (npm install, pip install, etc.)
- [ ] Linting configuré et passant
- [ ] Tests configurés et passant
- [ ] Build/compilation si applicable
- [ ] Artefacts générés et stockés
- [ ] Au moins 2 événements de déclenchement (push + PR)
- [ ] Variables et secrets utilisés correctement
- [ ] Workflow visible et fonctionnant dans GitHub Actions

**Exemple de workflow complet** :

```yaml
name: Complete Pipeline

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  quality-and-tests:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - uses: actions/setup-[language]@v[X]  # Python, Node, etc.
        with:
          [language]-version: 'version'
      
      - name: Install dependencies
        run: [install command]
      
      - name: Lint
        run: [lint command]
      
      - name: Tests
        run: [test command]
      
      - name: Build
        run: [build command]
      
      - name: Upload artifacts
        uses: actions/upload-artifact@v3
        with:
          name: build
          path: [build directory]
```

**Exercice Final :**
- Crée le workflow pour TON projet
- Crée un pull request et vérifie que le workflow s'exécute
- Fais un commit, merge et vérifie de nouveau
- Prends une capture d'écran du workflow réussi !

---

## 🎓 Ressources Complètes

### Documentation Officielle
- **GitHub Actions** : https://docs.github.com/en/actions
- **Workflow Syntax** : https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
- **Events** : https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

### Outils et Services
- **GitHub Actions Marketplace** : https://github.com/marketplace?type=actions
- **Actions Populaires** :
  - `actions/checkout@v3`
  - `actions/setup-python@v4`
  - `actions/setup-node@v3`
  - `actions/upload-artifact@v3`
  - `codecov/codecov-action@v3`

### Linters et Testeurs
- **Python** : pytest, pylint, black, mypy
- **Node.js** : jest, eslint, prettier, mocha

---

## 💡 Conseils pour réussir

1. **Pratique quotidienne** : 30-60 minutes par jour minimum
2. **Crée des erreurs exprès** : Pour comprendre comment les workflows réagissent
3. **Consulte les logs** : La clé pour déboguer tes workflows
4. **Réutilise du code** : Copie/adapte les templates d'autres projets
5. **Communique** : Partage tes workflows, reçois des retours
6. **Sois patient** : La CI/CD c'est un concept vaste, ça vient avec la pratique

---

## 📝 Notes Personnelles

**À remplir au fur et à mesure :**

- Jour X : [Ce que j'ai appris]
- Jour X : [Les défis rencontrés]
- Jour X : [Les solutions trouvées]

---

**Bonne chance Mamadou ! 🚀**

N'hésite pas à revenir me poser des questions chaque jour. Chaque concept sera clarifié ensemble.
