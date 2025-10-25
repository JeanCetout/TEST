# ProRealTime ProScreener - Scripts de Trading

Ce dépôt contient des scripts ProScreener pour ProRealTime, incluant la détection de supports/résistances et l'analyse de métriques de qualité de trading.

## 📋 Qu'est-ce qu'un Support/Résistance Niveau 3 ?

Un support ou une résistance de **niveau 3** est un niveau de prix qui a été testé **au moins 3 fois** avec des rebonds significatifs. Ces niveaux sont considérés comme particulièrement importants car ils ont démontré leur solidité à plusieurs reprises.

### Caractéristiques :
- ✅ **Minimum 3 touches** du niveau de prix
- ✅ **Rebonds confirmés** après chaque touche
- ✅ **Pertinence récente** (testés dans la période d'analyse)
- ✅ **Proximité actuelle** du prix au niveau détecté

## 📁 Scripts Disponibles

### A. Métriques de Qualité de Trading

#### `trading_quality_metrics.prt` - **NOUVEAU**
Script complet pour évaluer la qualité d'un instrument de trading.

**Fonctionnalités :**
- Calcul de 10 métriques de qualité
- Score global de 0 à 10
- Volume vs médiane
- ATR (Average True Range) vs médiane
- Ratio corps/mèche des bougies
- Chevauchement de corps
- Détection de runs directionnels
- Calcul du VWAP et distance au prix
- Approximation du spread et slippage
- Régularité du flux (volume)

**Métriques calculées :**
- Volume/Médiane : Liquidité relative
- Spread% : Coûts de transaction approximés
- ATR/Médiane : Volatilité relative
- Corps% : Force directionnelle
- Chevauchement% : Continuation ou consolidation
- Run : Nombre de bougies consécutives (tendance)
- VWAP% : Distance au VWAP
- Slip/ATR : Slippage potentiel

**📖 Documentation complète :** Voir [TRADING_METRICS_README.md](proscreener/TRADING_METRICS_README.md)

**Recommandé pour :**
- Trading intraday (1min, 5min, 15min)
- Sélection d'instruments à trader
- Évaluation de la qualité de setup
- Filtrage avant entrée en position

---

### B. Support et Résistance Niveau 3

#### 1. Version Complète : `support_resistance_level3.prt`
Script avancé avec analyse détaillée des rebonds et de la force des niveaux.

**Fonctionnalités :**
- Détection précise des pivots hauts et bas
- Analyse de la force des rebonds
- Calcul du nombre de touches pour chaque niveau
- Vérification de la proximité du prix actuel
- Confirmation par le volume (optionnel)

**Paramètres configurables :**
```
lookback = 20        // Période pour l'analyse des pivots
tolerance = 0.5      // Tolérance en % pour considérer un même niveau
minTouches = 3       // Nombre minimum de touches pour niveau 3
maxDistance = 2      // Distance max du prix au niveau (en %)
minBounce = 1        // Force du rebond minimum (en %)
```

#### 2. Version Simplifiée : `support_resistance_level3_simple.prt`
Script simplifié, plus rapide et facile à comprendre.

**Fonctionnalités :**
- Détection directe des niveaux testés plusieurs fois
- Calcul simple du nombre de tests
- Vérification de la proximité du prix
- Indicateurs de force (volume, rebond)

**Paramètres configurables :**
```
period = 50          // Période d'analyse
tolerance = 0.8      // Tolérance en % pour considérer un même niveau
minTests = 3         // Nombre minimum de tests du niveau
priceDistance = 3    // Distance max du prix au niveau (en %)
```

## 🚀 Installation et Utilisation

### Étape 1 : Créer un nouveau ProScreener

1. Ouvrez **ProRealTime**
2. Cliquez sur **Outils** → **ProScreener**
3. Cliquez sur **Nouveau Screener**
4. Donnez-lui un nom (ex: "Support Résistance N3")

### Étape 2 : Copier le code

1. Ouvrez l'un des fichiers `.prt` (version simple recommandée pour débuter)
2. **Copiez tout le contenu** du fichier
3. **Collez-le** dans la fenêtre de code du ProScreener

### Étape 3 : Configurer le screener

1. Sélectionnez votre **liste d'actions** (CAC 40, NASDAQ, etc.)
2. Choisissez l'**unité de temps** (Daily, H1, etc.)
3. Ajustez les **paramètres** selon vos besoins (voir section Paramètres)

### Étape 4 : Lancer le scan

1. Cliquez sur **Lancer le Screener**
2. Les résultats afficheront les actions près d'un support ou résistance niveau 3

## 📊 Interprétation des Résultats

### Colonnes affichées (version simple) :

| Colonne | Description |
|---------|-------------|
| **Support** | Prix du niveau de support détecté |
| **Tests S** | Nombre de fois que le support a été testé |
| **Résistance** | Prix du niveau de résistance détecté |
| **Tests R** | Nombre de fois que la résistance a été testée |
| **Support Fort** | 1 si support avec volume élevé, 0 sinon |
| **Resist Forte** | 1 si résistance avec volume élevé, 0 sinon |

### Comment utiliser ces informations :

#### Signal d'ACHAT (Support Niveau 3) :
- ✅ Le prix approche un **support** testé 3+ fois
- ✅ **Support Fort** = 1 (avec volume)
- ✅ Configuration idéale pour un rebond haussier

**Action recommandée :** Surveiller pour un signal d'entrée long (achat)

#### Signal de VENTE (Résistance Niveau 3) :
- ✅ Le prix approche une **résistance** testée 3+ fois
- ✅ **Resist Forte** = 1 (avec volume)
- ✅ Configuration idéale pour un rejet baissier

**Action recommandée :** Surveiller pour un signal d'entrée court (vente) ou sortie

## ⚙️ Personnalisation des Paramètres

### Pour des niveaux plus STRICTS (moins de faux signaux) :
```
minTests = 4 ou 5       // Exiger plus de touches
tolerance = 0.5         // Tolérance plus stricte
priceDistance = 2       // Plus proche du niveau
```

### Pour plus de SIGNAUX (plus de détections) :
```
minTests = 2            // Accepter moins de touches
tolerance = 1.0 ou 1.5  // Tolérance plus large
priceDistance = 5       // Distance plus grande
```

### Pour différentes unités de temps :
- **Day (journalier)** : `period = 50-100`
- **H1 (horaire)** : `period = 100-200`
- **M15 (15 min)** : `period = 200-500`

## 💡 Conseils d'Utilisation

1. **Combinez avec d'autres indicateurs** : RSI, MACD, moyennes mobiles
2. **Vérifiez visuellement** : Tracez les niveaux sur le graphique
3. **Utilisez le volume** : Les niveaux avec fort volume sont plus fiables
4. **Tenez compte du contexte** : Tendance générale du marché
5. **Définissez vos stops** : Placez stop-loss au-delà du support/résistance

## 📈 Exemples de Stratégies

### Stratégie 1 : Rebond sur Support N3
1. Screener détecte une action près d'un support niveau 3
2. Attendre la confirmation (chandelier haussier, volume)
3. Entrée LONG au-dessus du plus haut de la bougie
4. Stop-loss sous le support
5. Objectif : Résistance suivante ou 2x le risque

### Stratégie 2 : Cassure de Résistance N3
1. Screener détecte une action près d'une résistance niveau 3
2. Attendre la cassure avec fort volume
3. Entrée LONG sur retest de l'ancienne résistance (devenue support)
4. Stop-loss sous le nouveau support
5. Objectif : Extension de la cassure (projection de la range)

### Stratégie 3 : Rejet à la Résistance N3
1. Screener détecte une action près d'une résistance niveau 3
2. Attendre un chandelier de rejet (pin bar, étoile filante)
3. Entrée SHORT sous le plus bas de la bougie
4. Stop-loss au-dessus de la résistance
5. Objectif : Support suivant ou 2x le risque

## ⚠️ Avertissements

- ⚠️ **Aucun système n'est infaillible** : Les supports/résistances peuvent casser
- ⚠️ **Gestion du risque** : Ne risquez jamais plus de 1-2% par trade
- ⚠️ **Backtesting** : Testez toujours sur données historiques avant trading réel
- ⚠️ **Conditions de marché** : Les niveaux techniques fonctionnent mieux en range

## 🔧 Dépannage

### Le screener ne retourne aucun résultat :
- Réduire `minTests` à 2
- Augmenter `tolerance` à 1.0 ou 1.5
- Augmenter `priceDistance` à 5
- Vérifier la période d'analyse (augmenter `period`)

### Trop de résultats :
- Augmenter `minTests` à 4 ou 5
- Réduire `tolerance` à 0.3 ou 0.5
- Réduire `priceDistance` à 1 ou 2

### Erreurs de syntaxe :
- Vérifier que tout le code a été copié
- S'assurer qu'aucun caractère spécial n'a été altéré
- Utiliser la version simple en cas de problème

## 📚 Ressources Complémentaires

- [Documentation ProRealTime](https://www.prorealtime.com/fr/support)
- [Forum ProRealTime](https://www.prorealcode.com/forum/)
- [Langage ProBuilder](https://www.prorealtime.com/fr/probuilder)

## 📝 Licence

Ces scripts sont fournis à des fins éducatives. Utilisez-les à vos propres risques.

---

**Créé pour ProRealTime ProScreener v11+**
**Testé sur actions, indices, forex et crypto**
**Compatible avec toutes les unités de temps**
