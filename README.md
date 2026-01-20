# 🤖 Chatbot IA avec n8n + Groq

Un chatbot intelligent propulsé par n8n et l'API Groq (Llama 3.1), avec une interface web moderne et responsive.

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![n8n](https://img.shields.io/badge/n8n-workflow-orange)
![Groq](https://img.shields.io/badge/Groq-API-purple)

## ✨ Fonctionnalités

- 🎨 **Interface web moderne** avec design Docker + n8n
- ⚡ **Réponses ultra-rapides** grâce à Groq (Llama 3.1)
- 💬 **Chat en temps réel** avec formatage intelligent
- 📱 **100% Responsive** (mobile & desktop)
- 🔄 **Workflow n8n** simple et personnalisable
- 🆓 **Entièrement gratuit** avec quota généreux

## 📸 Aperçu

```
┌─────────────────────────────────────┐
│     🤖 Chatbot IA ✨                │
│   Propulsé par n8n + Groq           │
├─────────────────────────────────────┤
│                                      │
│  🤖 Bonjour ! Je suis ton           │
│     assistant IA...                 │
│                                      │
│             Qu'est-ce que Docker ? 👤│
│                                      │
│  🤖 Docker est une plateforme...    │
│                                      │
└─────────────────────────────────────┘
```

## 🚀 Installation rapide

### Prérequis

- [Docker](https://www.docker.com/) installé
- [n8n](https://n8n.io/) en cours d'exécution
- Compte [Groq](https://console.groq.com) (gratuit)

### Étape 1 : Lancer n8n

```bash
docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

Accédez à n8n : `http://localhost:5678`

### Étape 2 : Importer le workflow

1. Téléchargez `chatbot_workflow.json`
2. Dans n8n : **Menu** → **Import from File**
3. Sélectionnez le fichier
4. Configurez votre clé API Groq

### Étape 3 : Obtenir une clé API Groq

1. Créez un compte sur [console.groq.com](https://console.groq.com)
2. Allez dans **API Keys**
3. Créez une nouvelle clé
4. Copiez-la dans le node HTTP Request

### Étape 4 : Activer le workflow

Cliquez sur le **toggle** en haut à droite du workflow pour l'activer.

### Étape 5 : Lancer l'interface

```bash
# Téléchargez chatbot_interface.html
# Puis lancez un serveur local

python -m http.server 8000
```

Ouvrez : `http://localhost:8000/chatbot_interface.html`

## 🔧 Configuration

### Modifier l'URL du webhook

Dans `chatbot_interface.html`, ligne 354 :

```javascript
const API_URL = 'http://localhost:5678/webhook/chatbot';
```

Remplacez par votre URL si nécessaire.

### Personnaliser les questions d'exemple

Dans `chatbot_interface.html`, cherchez la section `example-questions` :

```html
<button class="example-btn" onclick="askQuestion('Votre question')">
    Texte du bouton
</button>
```

### Changer le modèle IA

Dans le workflow n8n, node HTTP Request, modifiez :

```json
{
  "model": "llama-3.1-8b-instant"
}
```

Modèles disponibles :
- `llama-3.1-8b-instant` (rapide)
- `llama-3.1-70b-versatile` (plus puissant)
- `mixtral-8x7b-32768` (grande fenêtre de contexte)

## 📁 Structure du projet

```
chatbot-ia-n8n/
├── chatbot_interface.html      # Interface web
├── chatbot_workflow.json        # Workflow n8n à importer
├── Guide_Exercices.docx         # Guide détaillé
└── README.md                    # Ce fichier
```

## 🎨 Personnalisation

### Couleurs

Modifiez les couleurs dans le CSS :

```css
/* Bleu Docker */
background: #0DB7ED;

/* Orange n8n */
background: #FF6F3D;

/* Fond dégradé */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
```

### Prompt système

Dans le workflow n8n, modifiez le message système :

```json
{
  "role": "system",
  "content": "Tu es un assistant spécialisé en..."
}
```

## 🌐 Déploiement

### Option 1 : Netlify (Recommandé)

1. Créez un compte sur [Netlify](https://netlify.com)
2. Glissez-déposez `chatbot_interface.html`
3. Votre chatbot est en ligne ! 🎉

### Option 2 : Vercel

```bash
npm i -g vercel
vercel --prod
```

### Option 3 : GitHub Pages

1. Créez un repo GitHub
2. Uploadez `chatbot_interface.html` (renommez en `index.html`)
3. Activez GitHub Pages dans Settings

## 🔒 Sécurité

⚠️ **Important pour la production :**

- ✅ Utilisez HTTPS (pas HTTP)
- ✅ Ajoutez une authentification sur n8n
- ✅ Configurez le rate limiting
- ✅ Stockez les clés API dans les variables d'environnement
- ✅ Activez CORS uniquement pour vos domaines

## 🐛 Dépannage

### Le chatbot ne répond pas

1. Vérifiez que n8n est actif : `http://localhost:5678`
2. Vérifiez que le workflow est **activé** (toggle vert)
3. Testez le webhook directement :

```bash
curl -X POST http://localhost:5678/webhook/chatbot \
  -H "Content-Type: application/json" \
  -d '{"question": "Test"}'
```

### Erreur CORS

Ajoutez dans les variables d'environnement n8n :

```bash
N8N_CORS_ORIGINS=https://votre-domaine.com
```

### Interface ne charge pas

1. Ouvrez la console (F12)
2. Vérifiez les erreurs
3. Assurez-vous que l'URL du webhook est correcte

## 📊 Workflow n8n

Le workflow contient 3 nodes :

1. **Webhook** : Reçoit les questions via POST
2. **HTTP Request** : Appelle l'API Groq
3. **Code** : Formate la réponse JSON

```
[Webhook] → [HTTP Request] → [Code]
```

## 💡 Améliorations futures

- [ ] Historique de conversation persistant
- [ ] Upload de fichiers/images
- [ ] Synthèse vocale (TTS)
- [ ] Support multilingue
- [ ] Thème dark/light
- [ ] Markdown rendering
- [ ] Bouton copier les réponses
- [ ] Système de feedback

## 🤝 Contribution

Les contributions sont les bienvenues ! 

1. Fork le projet
2. Créez votre branche (`git checkout -b feature/AmazingFeature`)
3. Commit vos changements (`git commit -m 'Add AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrez une Pull Request

## 📝 License

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 🙏 Remerciements

- [n8n](https://n8n.io/) - Plateforme d'automatisation
- [Groq](https://groq.com/) - API IA ultra-rapide
- [Llama 3.1](https://ai.meta.com/llama/) - Modèle de langage

---

⭐ **Si ce projet vous a été utile, n'hésitez pas à lui donner une étoile !**

---

**Fait avec ❤️ par Farah** | Propulsé par n8n 🚀 + Groq ⚡
