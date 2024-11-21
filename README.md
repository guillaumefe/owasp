# 🚀 Guide DemoKit - Formation

## 📥 Installation Rapide
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venvScriptsactivate     # Windows
pip install demokit
demokit
```
→ Placer vos apps dans le dossier "apps" créé
→ Relancer demokit

## 🎯 Deux Modes d'Utilisation

### 🌐 Mode Navigateur (recommandé)
- Élèves : accès web uniquement via URL fournie
- Aucune installation requise

### 💻 Mode Installation
- Élèves : suivent installation pip ci-dessus
- Apps : https://github.com/guillaumefe/owasp/blob/main/demokit1.2.zip
- Accès : http://localhost:8000

## 🔗 Option : Accès Distant avec ngrok
*Outil tiers à utiliser après lancement de DemoKit*

1. Lancer DemoKit avec vos apps
2. Dans un nouveau terminal :
   - Créer compte [ngrok.com](https://ngrok.com)
   - `ngrok config add-authtoken [TOKEN]`
   - `ngrok http 8000`
   - Utiliser l'URL https://*.ngrok.io générée

⚠️ URL change à chaque redémarrage

# 🚀 Tutoriel : Build et Rebuild avec DemoKit

Ce guide rapide vous explique comment **builder** et **rebuilder** vos applications avec **DemoKit** en seulement 4 étapes.

---

## 🛠️ Étape 1 : Préparer le projet

1. **Créez un dossier `apps/` si ce n'est pas déjà fait** :  
   Si vous n'avez pas encore lancé DemoKit, exécutez la commande suivante pour qu'il initialise automatiquement la structure du projet :
   ```bash
   demokit
   ```

2. **Ajoutez vos applications dans `apps/`** :  
   Chaque application doit contenir un fichier `Dockerfile` et un fichier `app-info.json` :
   ```plaintext
   apps/
   ├── app1/
   │   ├── app-info.json
   │   └── Dockerfile
   ├── app2/
   │   ├── app-info.json
   │   └── Dockerfile
   ```

   Exemple de `app-info.json` :
   ```json
   {
       "title": "Mon Application",
       "description": "Description de l'application",
       "version": "1.0.0"
   }
   ```

---

## 🛠️ Étape 2 : Build (première construction)

1. **Lancez DemoKit pour builder les applications** :  
   ```bash
   demokit
   ```

2. **Attendez la construction de toutes les applications** :  
   La console affichera des messages comme :
   ```plaintext
   Construction de l'image pour app1...
   Lancement du conteneur app1 sur le port 3000...
   ✅ Conteneur app1 déployé avec succès sur le port 3000
   ```

3. **Accédez à l'URL du serveur principal** :  
   Une fois le build terminé, ouvrez cette URL dans votre navigateur :
   ```plaintext
   http://localhost:8000
   ```

---

## 🛠️ Étape 3 : Rebuild (mise à jour des applications)

1. **Modifiez vos applications** :  
   Ajoutez ou mettez à jour les fichiers dans le dossier `apps/`.

2. **Relancez DemoKit pour effectuer un rebuild** :  
   Exécutez à nouveau la commande :
   ```bash
   demokit
   ```

   Les applications seront reconstruites et redéployées automatiquement.

3. **Vérifiez que les nouvelles versions sont en ligne** :  
   Ouvrez à nouveau l'index principal pour voir les modifications :
   ```plaintext
   http://localhost:8000
   ```

---

## 🛠️ Étape 4 : Résolution des problèmes (optionnel)

1. **Supprimer des conteneurs existants avant le rebuild** :  
   Si DemoKit ne reconstruit pas correctement vos applications, supprimez les conteneurs Docker manuellement :
   ```bash
   docker ps -a    # Liste les conteneurs
   docker rm -f <nom_du_conteneur>   # Supprime un conteneur
   ```

2. **Nettoyer les images Docker** :  
   Si des anciennes images causent des conflits, nettoyez-les :
   ```bash
   docker rmi <image_id>
   ```

3. **Rebuild complet** :  
   Relancez DemoKit pour un rebuild propre :
   ```bash
   demokit
   ```

---

## 🛠️ Étape 5 : Vérification des URLs

1. Une fois le build ou le rebuild terminé, la console affichera les URLs des applications :
   ```plaintext
   📌 Serveur principal : http://localhost:8000
   📌 Catalogue des applications : http://localhost:8101/catalog.html
   ```

2. **Vérifiez les ports associés à chaque application** :  
   Par exemple :
   ```plaintext
   http://localhost:3000  # app1
   http://localhost:3001  # app2
   ```

---

# 🐍 Publier un package Python avec Flit

Ce tutoriel vous guide pour publier un package Python sur **PyPI** en utilisant **Flit**.

---

## 📂 Étape 1 : Préparez votre structure de projet

Assurez-vous que votre projet respecte cette structure :

📁 mon_projet/ 
├── 📁 mon_package/ 
│ ├── init.py 
│ ├── main.py 
│ ├── autres_fichiers.py 
├── README.md 
├── pyproject.toml 
└── dist/


### 🛠 Points importants :
- **`__init__.py`** : Identifie le dossier comme un package Python.
- **`__main__.py`** : Contient le point d’entrée si votre package est exécutable avec `python -m`.
- **`pyproject.toml`** : Fichier de configuration essentiel pour Flit.
- **`README.md`** : Optionnel mais recommandé pour une meilleure présentation sur PyPI.

---

## 📝 Étape 2 : Créez un fichier `pyproject.toml`

Voici un exemple minimal :

```toml
[build-system]
requires = ["flit_core>=3.2,<4"]
build-backend = "flit_core.buildapi"

[tool.flit.metadata]
module = "mon_package"
author = "Votre Nom"
author-email = "votre.email@example.com"
home-page = "https://github.com/votre-repo"
description = "Une courte description"
license = "MIT"
requires-python = ">=3.7"
requires = ["click>=8.0"]

[tool.flit.scripts]
mon_package = "mon_package.__main__:main"

## 🏗️ Étape 3 : Construisez votre package

1. Nettoyez le dossier `dist/` :
   ```bash
   rm -rf dist/
   ```

2. Construisez le package :
   ```bash
   flit build
   ```

✅ Vérifiez :
Après la commande, le dossier dist/ contiendra :

📁 dist/
├── mon_package-1.0.0.tar.gz
└── mon_package-1.0.0-py3-none-any.whl

## 🧪 Étape 4 : Testez votre package localement

1. Installez le package&nbsp;:
   ```bash
   pip install ./dist/mon_package-1.0.0-py3-none-any.whl
   ```

2. Testez l’exécution&nbsp;:
   - Avec `python -m`&nbsp;:
     ```bash
     python -m mon_package
     ```
   - Avec la commande CLI (si configurée)&nbsp;:
     ```bash
     mon_package
     ```

---

## 🚀 Étape 5&nbsp;: Publiez votre package

### Option 1&nbsp;: TestPyPI (dépôt de test)

1. Configurez TestPyPI dans `~/.pypirc`&nbsp;:
   ```
   [distutils]
   index-servers =
       pypi
       testpypi

   [testpypi]
   repository = https://test.pypi.org/legacy/
   username = __token__
   password = pypi-votre-jeton-testpypi
   ```

2. Publiez sur TestPyPI&nbsp;:
   ```bash
   flit publish --repository testpypi
   ```

3. Vérifiez votre projet sur [TestPyPI](https://test.pypi.org).

---

### Option 2&nbsp;: PyPI (dépôt principal)

1. Configurez PyPI dans `~/.pypirc`&nbsp;:
   ```
   [pypi]
   repository = https://upload.pypi.org/legacy/
   username = __token__
   password = pypi-votre-jeton-pypi
   ```

2. Publiez sur PyPI&nbsp;:
   ```bash
   flit publish
   ```

3. Vérifiez votre projet sur [PyPI](https://pypi.org).

---

## 🛠️ Résolution des problèmes fréquents

### ❌ Erreur&nbsp;: `403 Forbidden`
- Assurez-vous que votre **jeton API** est valide.
- Vérifiez que le nom du projet est unique sur PyPI.

### ❌ Erreur&nbsp;: `ModuleNotFoundError`
- Installez les dépendances listées dans `pyproject.toml`&nbsp;:
  ```bash
  pip install -r requirements.txt
  ```

---
