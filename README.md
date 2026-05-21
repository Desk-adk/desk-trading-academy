# Desk Trading Academy — V1

**Plateforme de gestion et de suivi pédagogique pour une académie de trading**

> *Investir avec sagesse, prospérer avec foi.*

---

## 🎯 Vue d'ensemble

Desk Trading Academy (DTA) est une application web **tout-en-un** conçue pour :
- **Administrateurs** : Gérer les élèves, suivre leurs progrès, analyser les performances globales
- **Élèves** : Enregistrer et analyser leurs trades (live & backtest), suivre leur classement, recevoir des feedbacks pédagogiques

### Caractéristiques principales

✅ **Gestion des élèves**
- Création automatique d'ID et mots de passe
- Profils détaillés avec historique et logs
- Statuts flexibles (Actif, Suspendu, Attention, Diplômé)

✅ **Journal de trades complet**
- Enregistrement live avec checklist pré-trade
- Backtesting avec validation de stratégie
- Suivi des émotions (avant/après)
- Capture d'écran et analyse

✅ **Système de scoring intelligent**
- **Score global** = Winrate (40%) + Profit Factor (25%) + Discipline (35%)
- **Score discipline** basé sur la gestion du risque et la checklist
- **Système de garde-fous** : alerte DD journalier, pertes consécutives, overtrading

✅ **Classement académique**
- Ranking en temps réel
- Médailles et indicateurs visuels
- Comparaison par pairs

✅ **Statistiques détaillées**
- Winrate, Profit Factor, Max Drawdown
- Top setups, meilleures sessions, actifs
- Analyse psychologique (émotions vs résultats)

✅ **Dashboard & Analytics**
- KPIs académie en temps réel
- Graphiques d'évolution
- Alertes pédagogiques

---

## 🚀 Démarrage rapide

### Installation

1. **Clonez le repository**
   ```bash
   git clone https://github.com/Desk-adk/desk-trading-academy.git
   cd desk-trading-academy
   ```

2. **Ouvrez le fichier HTML**
   ```bash
   # Simplement ouvrir index.html dans votre navigateur
   open index.html
   ```
   Ou hébergez sur un serveur web (GitHub Pages, Netlify, Vercel, etc.)

### Identifiants par défaut

**Administrateur :**
- ID : `admin`
- Mot de passe : `dta2026`

**Élève :** Généré lors de la création du compte

---

## 📱 Interface utilisateur

### Design
- **Thème sombre** premium avec accents or (palette cohérente)
- **Responsive** : Desktop, Tablet, Mobile
- **Icônes Tabler** pour une meilleure UX
- **Typographie** : Syne (headings) + Figtree (body)

### Sections principales

#### Admin
1. **Dashboard** - KPIs, top 5 du classement, activité récente, alertes
2. **Gestion élèves** - Liste, filtres, création, édition, suppression
3. **Profil élève** (admin view)
   - Onglets : Journal Live, Backtesting, Statistiques, Commentaires, Logs
4. **Journal global** - Tous les trades de l'académie avec filtres
5. **Leaderboard** - Classement global par score composite
6. **Statistiques académie** - Top setups, sessions, actifs, émotions

#### Élève
1. **Mon Dashboard** - Score, KPIs, derniers trades, feedbacks coach
2. **Journal Live** 
   - Formulaire complet avec checklist pré-trade
   - Émotions avant/après
   - Erreurs et leçons retenues
3. **Backtesting**
   - Validation automatique de stratégie (min 20 backtests, WR≥55%, RR≥1.5)
4. **Mes statistiques** - Performance détaillée
5. **Mon classement** - Position et comparaison avec les autres

---

## 💾 Données & Stockage

**Technologie** : `localStorage` (client-side)
- Toutes les données sont sauvegardées localement
- **Export JSON** disponible via le bouton Export (admin)
- Pas de serveur requis

### Structure de données

```json
{
  "admin": { "user": "admin", "pass": "dta2026" },
  "students": [
    {
      "id": 1234567890,
      "ci": 0,
      "name": "Ibrahim Moussa",
      "email": "eleve@email.com",
      "studentId": "DTA-123456",
      "password": "XxYyZz89",
      "trades": [...],
      "btTrades": [...],
      "comments": [...],
      "log": [...]
    }
  ],
  "activity": [...]
}
```

---

## 🧮 Algorithmes clés

### Score global
```
Global Score = (Winrate × 0.4) + (min(PF × 20, 100) × 0.25) + (Discipline × 0.35)
```

### Score discipline
```
Discipline = 100 - pénalités
- Risque > limite : -5 par trade
- Pas de setup défini : -3
- Checklist < 5/5 : -2 × (5 - score)
- RR < 1.5 : -2
```

### Validation stratégie backtest
```
Valide si :
  - Minimum 20 backtests ✓
  - Winrate ≥ 55% ✓
  - RR moyen ≥ 1.5 ✓
```

### Système de garde-fous
```
Alerte ROUGE si :
  - Pertes consécutives ≥ limite
  - Drawdown journalier ≥ limite
```

---

## 🔐 Sécurité

⚠️ **Version V1 - Développement/Démo**
- Authentification basique (pas de hachage)
- Données en localStorage (non chiffrées)
- ✅ **Pour production** : 
  - Intégrer backend avec JWT
  - Hacher les mots de passe (bcrypt)
  - Base de données sécurisée
  - HTTPS obligatoire

---

## 🎨 Customisation

### Modifier les couleurs
Dans le `<style>`, modifiez les variables CSS :
```css
:root {
  --gold: #C9A84C;      /* Couleur principale */
  --gr: #1FC97A;        /* Vert (wins) */
  --rd: #E04545;        /* Rouge (losses) */
  --bl: #3A8FE8;        /* Bleu (RR/stats) */
  /* ... etc */
}
```

### Modifier les limites par défaut
Dans `addStudent()` :
```javascript
const stu = {
  maxRisk: 2,          // Risque max par trade (%)
  maxDailyDD: 5,       // Drawdown journalier max (%)
  maxConsecLoss: 3,    // Pertes consécutives max
  accountSize: 1000    // Taille compte initial ($)
};
```

---

## 📊 Statistiques calculées

La plateforme calcule automatiquement :

| Métrique | Formule | Usage |
|----------|---------|-------|
| **Winrate** | (Wins / Total) × 100 | Performance globale |
| **Profit Factor** | Gross Profit / Gross Loss | Rentabilité |
| **RR moyen** | Σ(RR) / Nombre de trades | Qualité des setups |
| **Max Drawdown** | Peak - Trough | Risque réalisé |
| **Discipline** | 100 - pénalités | Gestion du risque |

---

## 🔄 Flux utilisateur

### Administrateur
```
Login → Dashboard → Gérer élèves → Ajouter/Éditer/Voir profil → Analyser performance
```

### Élève
```
Login → Mon Dashboard → Enregistrer trade → Analyser statistiques → Suivre classement
```

---

## 📁 Structure des fichiers

```
desk-trading-academy/
├── index.html          # Application complète (monolithe)
├── README.md           # Ce fichier
└── .gitignore          # (optionnel)
```

### 🔮 V2 (Roadmap)
- [ ] Backend Node.js/Express
- [ ] Base de données MongoDB
- [ ] Authentification JWT
- [ ] API REST
- [ ] Support vidéo/PDF pour les cours
- [ ] Notifications email
- [ ] Système de badges/achievements
- [ ] Export PDF des rapports
- [ ] Intégration MT4/MT5 (trade feed)
- [ ] Mobile app native

---

## 🐛 Troubleshooting

**Q: Mon historique a disparu ?**
A: Les données sont stockées en localStorage. Nettoyez le cache ou vérifiez que le site n'est pas en mode privé.

**Q: Comment réinitialiser les données ?**
A: Ouvrez la console (F12) et tapez :
```javascript
localStorage.removeItem('dta_v1');
location.reload();
```

**Q: Puis-je sauvegarder les données elsewhere ?**
A: Oui ! Admin → Export → Télécharge un JSON. Conservez ce fichier en backup.

---

## 📝 Notes pédagogiques

### Checklist pré-trade (5 critères)
1. ✅ Analyse HTF (H4/Daily)
2. ✅ Setup = Plan de trading
3. ✅ Kill zone valide
4. ✅ Risque ≤ limite
5. ✅ Stabilité émotionnelle

### Setups SMC supportés
- BOS + FVG
- Supply/Demand
- Liquidity Sweep
- CHOCH
- OB + Confirmation
- MSS
- EQH/EQL

### Sessions de trading
- London
- New York
- Asian
- London/NY overlap

---

## 👨‍💼 Support & Contact

- **Créateur** : Desk Trading Academy
- **Version** : 1.0 (Mai 2026)
- **License** : Propriétaire
- **Repository** : [GitHub](https://github.com/Desk-adk/desk-trading-academy)

---

## 📄 License

© 2026 Desk Trading Academy. Tous droits réservés.

---

**Prêt à trader intelligemment ?** 🚀📈
