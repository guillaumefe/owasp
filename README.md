# 🚀 Guide DemoKit - Formation

## 📥 Installation Rapide
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
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
