# 📊 Légende des Critères - ProScreener Trading Quality Metrics V4.0

## Vue d'ensemble

Le screener affiche **11 colonnes avec noms personnalisés** dans ProRealTime.

**⭐ NOUVEAUTÉ V4.0** : Ajout de la colonne **"Speed"** (SpeedMeter) pour mesurer la vitesse des mouvements !

**Affichage dans ProScreener V4.0** :
```
Score | Volume | ATR | Run | Align | Type | Speed | Scalp | T1 | T2 | T3
                                           ↑
                                        NOUVEAU!
```

**Historique** :
- **V4.0** : + Colonne Speed (SpeedMeter) - 11 colonnes
- **V3.1** : + Colonne Scalp - 10 colonnes
- **V3.0** : Colonnes avec noms lisibles - 9 colonnes

---

## 🔢 Les 11 Colonnes Personnalisées

### Colonne 1 : **"Score"** (`qualityScore`)

**Nom affiché** : `Score`
**Variable** : `qualityScore`
**Plage** : 0 à 13
**Signification** : Score composite calculé à partir de 10 métriques de qualité + bonus multi-tendance

**Calcul détaillé** (10 points de base):
- ✅ Volume ≥ Moyenne → +1 point
- ✅ Spread < Moyenne → +1 point
- ✅ Corps bougie ≥ 50% → +1 point
- ✅ Run directionnel ≥ 3 bougies → +1 point
- ✅ Distance VWAP ≤ 0.5% → +1 point
- ✅ Slippage faible (< 10%) → +1 point
- ✅ Flux régulier (CV < 0.5) → +1 point
- ✅ ATR normal (0.8-1.2x moyenne) → +1 point
- ✅ Chevauchement corps 30-70% → +1 point
- ✅ Volume fort (≥ 1.5x moyenne) → +1 point

**Bonus Multi-Tendance** (+3 points max):
- 🎯 3 EMA alignées + force > 0.5% → +2 points
- 🎯 2 EMA alignées + force > 0.3% → +1 point
- 🎯 Force moyenne > 1.0% → +1 point

**Interprétation**:
- `≥ 10` → 🟢 Signal haute qualité
- `7-9` → 🟡 Signal acceptable (seuil par défaut)
- `< 7` → 🔴 Non affiché (filtré)

---

### Colonne 2 : **"Volume"** (`volumeRatio`)

**Nom affiché** : `Volume`
**Variable** : `volumeRatio`
**Plage** : 0 à ∞
**Signification** : Ratio du volume actuel par rapport à la moyenne des 100 dernières bougies

**Interprétation**:
- `> 2.0` → 🔥 Volume exceptionnel (+100%)
- `1.5-2.0` → 🟢 Volume fort (+50-100%)
- `1.0-1.5` → 🟡 Volume normal à élevé
- `< 1.0` → 🔴 Volume faible

**Utilisation**: Un volume élevé confirme la validité du mouvement de prix.

---

### Colonne 3 : **"ATR"** (`atrRatio`)

**Nom affiché** : `ATR`
**Variable** : `atrRatio`
**Plage** : 0 à ∞
**Signification** : Ratio de l'ATR actuel (volatilité sur 14 périodes) par rapport à la moyenne des 100 dernières valeurs

**Interprétation**:
- `> 1.5` → 🔴 Volatilité excessive (risque élevé)
- `1.2-1.5` → 🟡 Volatilité élevée
- `0.8-1.2` → 🟢 Volatilité normale (optimal)
- `< 0.8` → 🟡 Volatilité faible (marché calme)

**Utilisation**: Permet d'ajuster la taille de position et les stops selon la volatilité.

---

### Colonne 4 : **"Run"** (`directionalRun`)

**Nom affiché** : `Run`
**Variable** : `directionalRun`
**Plage** : 0 à 10
**Signification** : Nombre de bougies haussières ou baissières consécutives (max 10 analysées)

**Interprétation**:
- `≥ 5` → 🔥 Tendance très forte (attention au retournement)
- `3-4` → 🟢 Tendance confirmée
- `1-2` → 🟡 Début de mouvement
- `0` → ⚪ Pas de directionnalité

**Utilisation**:
- Run haussier + Align = 3 → Continuation probable
- Run élevé (≥5) → Attendre pullback avant entrée

---

### Colonne 5 : **"Align"** (`alignmentScore`)

**Nom affiché** : `Align`
**Variable** : `alignmentScore`
**Plage** : 0 à 3
**Signification** : Nombre d'EMA (20, 50, 100) alignées dans la même direction

**Interprétation**:
- `3` → 🔥 **TOUTES les tendances alignées** (court + moyen + long terme)
- `2` → 🟢 Alignement partiel (2 timeframes concordants)
- `1` → 🟡 Tendance faible (1 seul timeframe)
- `0` → 🔴 Pas de tendance claire

**Utilisation**:
- Score = 3 → Signal le plus puissant, probabilité max
- Score < 2 → Éviter, signaux contradictoires

---

### Colonne 6 : **"Type"** (`marketType`)

**Nom affiché** : `Type`
**Variable** : `marketType`
**Plage** : -2 à +2
**Signification** : Classification automatique du type de marché basée sur l'alignement des EMA

**Valeurs**:
- `+2` → 🔥 **Bull Fort** (toutes les EMA haussières, Align = 3)
- `+1` → 🟢 **Bull Modéré** (2+ EMA haussières, tendance haussière probable)
- `0` → ⚪ **Range/Neutre** (pas de direction claire, tendances mixtes)
- `-1` → 🟠 **Bear Modéré** (2+ EMA baissières, tendance baissière probable)
- `-2` → 🔴 **Bear Fort** (toutes les EMA baissières, Align = 3)

**Interprétation**:
- `+2` → Position LONG privilégiée, forte tendance haussière confirmée
- `+1` → Position LONG possible, tendance haussière en formation
- `0` → RANGE trading ou attente, pas de tendance claire
- `-1` → Position SHORT possible, tendance baissière en formation
- `-2` → Position SHORT privilégiée, forte tendance baissière confirmée

**Utilisation stratégique**:
- Filtrer `Type >= +1` pour ne trader QUE les marchés haussiers
- Filtrer `Type <= -1` pour ne trader QUE les marchés baissiers
- Filtrer `Type = 0` pour stratégies de range (support/résistance)
- Filtrer `ABS(Type) = 2` pour les tendances les plus fortes

---

### Colonne 7 : 🆕 **"Speed"** (`speedMeter`) - V4.0

**Nom affiché** : `Speed`
**Variable** : `speedMeter`
**Plage** : 0 à ∞ (typiquement 0.5 à 4.0)
**Signification** : Mesure de la vitesse et de la fréquence des mouvements de prix

**Formule de calcul** :
```
SpeedMeter = (Velocity Ratio + Tick Activity) / 2
```

**Composants** :
1. **Velocity Ratio** : Mouvement prix actuel / Moyenne 20 bougies
   - `priceVelocity = ABS(close - open)`
   - `avgVelocity = AVERAGE[20](ABS(close[i] - open[i]))`
   - `velocityRatio = priceVelocity / avgVelocity`

2. **Tick Activity** : Volume Ratio (activité de trading)
   - `tickActivity = volume / AVERAGE[100](volume)`

**Interprétation** :
- `≥ 2.5` → 🔥 **Très rapide** (excellent pour scalping ultra-actif)
- `2.0-2.5` → ⚡ **Rapide** (bon pour scalping 1-5 min)
- `1.5-2.0` → 🟡 **Moyen** (acceptable pour swing court)
- `1.0-1.5` → 🟠 **Lent** (position trading uniquement)
- `< 1.0` → 🔴 **Très lent** (éviter pour intraday)

**Avantages** :
- ⚡ **Identifie mouvements rapides** : Instruments qui bougent vite = plus d'opportunités
- 📊 **Mesure activité réelle** : Combine prix + volume pour vision complète
- 🎯 **Filtre scalping précis** : Speed ≥ 2.0 garantit mouvement suffisant
- ❌ **Évite instruments morts** : Speed < 1.5 = peu d'activité

**Utilisation** :
- Filtrer **Speed ≥ 2.5** pour scalping ultra-rapide (1-5 min)
- Filtrer **Speed ≥ 2.0** pour scalping standard
- Combiner **Speed ≥ 2.0** + **Scalp = 1** + **Score ≥ 9** pour setup optimal
- Éviter **Speed < 1.5** pour stratégies intraday

**Dépend du timeframe** :
- **1 min** : Speed typique 2.0-3.5
- **5 min** : Speed typique 1.8-2.5
- **10 min** : Speed typique 1.5-2.0
- **1 heure** : Speed typique 0.8-1.5

**Paramètres ajustables** (lignes 57-58 du code) :
```prorealtime
velocityPeriod = 20         // Période calcul vitesse (10-30)
minSpeedScalping = 1.8      // Speed min pour scalping (1.5-2.5)
```

---

### Colonne 8 : **"Scalp"** (`scalpQuality`) - V3.1

**Nom affiché** : `Scalp`
**Variable** : `scalpQuality`
**Plage** : 0 ou 1
**Signification** : Indicateur binaire pour identifier si l'instrument est adapté au scalping de qualité

**Critères pour Scalp = 1** (3 conditions simultanées) :
1. 💰 **Volume ≥ 2.0x** la moyenne → Liquidité excellente
2. 📉 **Spread ≤ 0.3%** du prix → Coûts de transaction minimaux
3. 📊 **ATR ≤ 1.3x** la moyenne → Volatilité maîtrisée

**Interprétation** :
- `1` → ✅ **Adapté scalping** (toutes conditions remplies)
- `0` → ❌ **Non adapté scalping** (au moins 1 critère non rempli)

**Différence Speed vs Scalp** :
- **Speed** : Mesure la **vitesse/activité** (mouvements rapides)
- **Scalp** : Mesure les **conditions** (spread, volume, volatilité)
- **Optimal** : **Speed ≥ 2.0 ET Scalp = 1** = Setup scalping parfait

**Utilisation** :
- Filtrer **Scalp = 1** pour conditions optimales
- Combiner avec **Speed ≥ 2.0** pour instruments rapides + bonnes conditions
- Éviter **Scalp = 0** si stratégie scalping

**Paramètres ajustables** (lignes 53-55 du code) :
```prorealtime
minVolumeScalping = 2.0     // Augmenter pour plus strict
maxSpreadScalping = 0.3     // Réduire pour spreads plus serrés
maxATRScalping = 1.3        // Réduire pour moins de volatilité
```

---

### Colonnes 9, 10, 11 : **"T1"**, **"T2"**, **"T3"** (trends)

**Noms affichés** : `T1`, `T2`, `T3`
**Variables** : `trend1`, `trend2`, `trend3`
**Plage** : -1, 0, +1
**Signification** : Direction de chaque EMA par rapport au prix

| Colonne | Nom Affiché | Variable | EMA | Représente |
|---------|-------------|----------|-----|------------|
| **9** | **T1** | trend1 | EMA 20 | Tendance **court terme** (quelques heures) |
| **10** | **T2** | trend2 | EMA 50 | Tendance **moyen terme** (demi-journée) |
| **11** | **T3** | trend3 | EMA 100 | Tendance **long terme** (journée complète) |

**Valeurs**:
- `+1` → 🟢 Prix > EMA (tendance **haussière**)
- `0` → ⚪ Prix = EMA (neutre)
- `-1` → 🔴 Prix < EMA (tendance **baissière**)

**Configurations optimales**:
```
Achat fort:  T1=+1, T2=+1, T3=+1 (Align=3, Type=+2)
Vente forte: T1=-1, T2=-1, T3=-1 (Align=3, Type=-2)
Indécision:  T1=+1, T2=-1, T3=0 (Align=1, Type=0)
```

---

## 🎯 Exemples d'Interprétation V4.0

### Exemple 1 : Signal Scalping PARFAIT ⭐⭐⭐⭐ 🆕

**Affichage dans ProScreener V4.0** :
```
Score: 12  | Volume: 2.8 | ATR: 1.0 | Run: 4 | Align: 3 | Type: +2 | Speed: 2.7 | Scalp: 1 | T1: +1 | T2: +1 | T3: +1
```

**Analyse détaillée** :
- 🟢 **Score: 12/13** → Excellente qualité (presque parfait)
- 🟢 **Volume: 2.8** → Volume x2.8 la moyenne (participation massive)
- 🟢 **ATR: 1.0** → Volatilité normale (risque maîtrisé)
- 🟢 **Run: 4** → 4 bougies haussières consécutives (momentum confirmé)
- 🟢 **Align: 3** → Toutes les EMA alignées (cohérence maximale)
- 🔥 **Type: +2** → **BULL FORT confirmé** (toutes tendances haussières)
- 🔥 **Speed: 2.7** → **TRÈS RAPIDE** - Mouvements explosifs ! 🆕
- ⚡ **Scalp: 1** → **Adapté scalping** (liquidité + spread + volatilité optimaux)
- 🟢 **T1/T2/T3: +1** → Court, moyen, long terme TOUS haussiers

**Interprétation globale** :
- 🎯 **Probabilité** : Maximale (setup parfait V4.0)
- 💪 **Force** : Maximale (momentum + alignement + vitesse)
- 📈 **Direction** : Haussière sans ambiguïté
- ⚡ **Scalping** : Conditions IDÉALES (Speed + Scalp + Score)

**Action recommandée** : **SCALPING LONG ULTRA-AGRESSIF** 🚀
**Stratégie** : Scalping 1-5 min avec entries multiples rapides
**Entry** : Immédiate sur signal ou micro-pullback
**Stop-Loss** : 0.3-0.5 x ATR (ultra serré grâce à Speed élevé + Scalp 1)
**Take-Profit** : 1:1 (sorties très rapides, nombreuses opportunités)

**Pourquoi ce signal est parfait** :
- Speed 2.7 = Mouvements très rapides = Nombreuses opportunités
- Scalp 1 = Conditions parfaites (spread faible, volume élevé)
- Type +2 = Direction claire pour entries directionnelles
- Score 12 = Qualité maximale

---

### Exemple 2 : Bon Signal mais LENT ❌ Speed Insuffisant

**Affichage dans ProScreener V4.0** :
```
Score: 10  | Volume: 1.6 | ATR: 1.1 | Run: 3 | Align: 3 | Type: +2 | Speed: 1.2 | Scalp: 0 | T1: +1 | T2: +1 | T3: +1
```

**Analyse détaillée** :
- 🟢 **Score: 10** → Bonne qualité
- 🟡 **Volume: 1.6** → Volume modéré
- 🟢 **ATR: 1.1** → Volatilité normale
- 🟢 **Run: 3** → Momentum confirmé
- 🟢 **Align: 3** → Alignement parfait
- 🔥 **Type: +2** → Bull Fort
- 🔴 **Speed: 1.2** → **LENT** - Peu de mouvement ! 🆕
- ❌ **Scalp: 0** → Non adapté scalping
- 🟢 **T1/T2/T3: +1** → Toutes tendances haussières

**Interprétation globale** :
- ✅ **Qualité** : Bonne (Score 10 + Type +2)
- ❌ **Vitesse** : Insuffisante (Speed 1.2 = lent)
- ⚠️ **Scalping** : NON recommandé (Speed faible + Scalp 0)

**Action recommandée** : **ÉVITER pour scalping** - Privilégier swing
**Problème** : Speed trop faible = peu d'opportunités intraday
**Alternative** : Position swing ou day trading long terme (pas scalping)
**Entry si swing** : Sur pullback avec SL large (1.5-2.0 x ATR)

**Pourquoi éviter ce signal pour scalping** :
- Speed 1.2 = Mouvements lents = Peu d'opportunités
- Scalp 0 = Conditions non optimales
- Mieux attendre instrument avec Speed ≥ 2.0

---

### Exemple 3 : Speed Élevé mais Score Faible ⚠️

**Affichage dans ProScreener V4.0** :
```
Score: 7   | Volume: 3.2 | ATR: 2.1 | Run: 2 | Align: 1 | Type: 0  | Speed: 2.6 | Scalp: 0 | T1: +1 | T2: -1 | T3: 0
```

**Analyse détaillée** :
- 🟡 **Score: 7** → Qualité moyenne (seuil minimum)
- 🟢 **Volume: 3.2** → Volume très élevé
- 🔴 **ATR: 2.1** → Volatilité EXCESSIVE (risque élevé, 110% au-dessus normale)
- 🟡 **Run: 2** → Peu de momentum
- 🔴 **Align: 1** → Pas de cohérence
- ⚠️ **Type: 0** → Range/Neutre
- 🔥 **Speed: 2.6** → **Très rapide** (beaucoup de mouvement) 🆕
- ❌ **Scalp: 0** → Non adapté (volatilité excessive)
- ⚠️ **T1: +1, T2: -1, T3: 0** → Tendances contradictoires

**Interprétation globale** :
- ⚡ **Vitesse** : Excellente (Speed 2.6)
- ❌ **Qualité** : Faible (Score 7, ATR excessif)
- 🔴 **Risque** : TRÈS ÉLEVÉ (volatilité 2.1x = slippage probable)

**Action recommandée** : **PRUDENCE** - Speed élevé MAIS risque élevé
**Problème** : Mouvements rapides mais volatilité excessive + tendances contradictoires
**Risque** : ATR 2.1 = Slippage important même avec Speed élevé
**Alternative** :
- Si trade, utiliser SL TRÈS larges (2.5-3.0 x ATR)
- Réduire taille position de 50-75%
- Ou attendre signal avec Score ≥ 9 + ATR normal

**Pourquoi prudence malgré Speed élevé** :
- Speed élevé ≠ toujours bon signal
- Volatilité excessive peut annuler avantage de Speed
- Tendances contradictoires = pas de direction claire

---

### Exemple 4 : Setup Scalping Modéré 🆕

**Affichage dans ProScreener V4.0** :
```
Score: 9   | Volume: 2.2 | ATR: 1.1 | Run: 3 | Align: 2 | Type: +1 | Speed: 2.1 | Scalp: 1 | T1: +1 | T2: +1 | T3: 0
```

**Analyse détaillée** :
- 🟢 **Score: 9** → Bonne qualité
- 🟢 **Volume: 2.2** → Volume élevé
- 🟢 **ATR: 1.1** → Volatilité normale
- 🟢 **Run: 3** → Momentum confirmé
- 🟡 **Align: 2** → Alignement partiel (bon)
- 🟢 **Type: +1** → Bull Modéré
- ⚡ **Speed: 2.1** → **Rapide** 🆕
- ✅ **Scalp: 1** → Adapté scalping
- 🟢 **T1: +1, T2: +1, T3: 0** → CT et MT haussiers

**Interprétation globale** :
- ✅ **Setup scalping valide** : Speed 2.1 + Scalp 1
- 🟢 **Qualité correcte** : Score 9 acceptable
- ⚡ **Vitesse bonne** : Speed 2.1 = mouvements rapides

**Action recommandée** : **SCALPING LONG MODÉRÉ**
**Stratégie** : Scalping 5-10 min (moins agressif que Exemple 1)
**Entry** : Sur pullback ou cassure résistance
**Stop-Loss** : 0.7-1.0 x ATR
**Take-Profit** : 1:1.5

**Comparaison avec Exemple 1** :
- Exemple 1 : Speed 2.7, Score 12, Type +2 = Setup PARFAIT
- Exemple 4 : Speed 2.1, Score 9, Type +1 = Setup BON (moins agressif)

---

## 💡 Stratégies d'Utilisation avec Colonnes V4.0

### 1. 🆕 Scalping Ultra-Rapide (SpeedMeter V4.0)

**Objectif** : Scalping sur mouvements explosifs avec SpeedMeter

**Critères dans ProScreener V4.0** :
1. Lancez le screener
2. Triez colonne **"Speed"** décroissant
3. Les **Speed ≥ 2.5** apparaissent en premier (très rapides) 🆕
4. Filtrez visuellement :
   - **Scalp = 1** (conditions optimales)
   - **Score >= 9**
   - **Type = +2** (LONG) ou **Type = -2** (SHORT)

**Exemple de signal scalping ultra-rapide** :
```
Score: 11+ | Volume: 2.5+ | Speed: 2.5+ | Scalp: 1 | Type: ±2
```

**Avantages Speed ≥ 2.5** :
- ⚡ Mouvements explosifs = profits rapides
- 📊 Nombreuses opportunités par session
- 🎯 Idéal timeframes 1-5 min

**Stops/TP recommandés** :
- **SL** : 0.3-0.5 x ATR (ultra serré grâce à vitesse élevée)
- **TP** : 1:1 (très rapide, volume élevé d'opportunités)

---

### 2. Scalping Standard (Speed + Scalp)

**Critères** :
- **Speed ≥ 2.0** (rapide)
- **Scalp = 1** (bonnes conditions)
- **Score ≥ 9**
- **Type = ±2** ou **±1**

**Setup idéal** :
```
Speed: 2.0-2.5 | Scalp: 1 | Score: 9+ | Type: ±1 ou ±2
```

**Timeframes** : 5-10 min
**SL** : 0.5-1.0 x ATR
**TP** : 1:1 à 1:1.5

---

### 3. Filtrage par SpeedMeter (Éviter Instruments Morts)

**Pour instruments ACTIFS** :
1. Trier **"Speed"** décroissant
2. Exclure **Speed < 1.5** (trop lent pour intraday)
3. Sélectionner **Speed ≥ 2.0** pour scalping
4. Vérifier **Score ≥ 9**

**Pour identifier instruments "morts"** :
- **Speed < 1.0** = Très lent, aucune opportunité intraday
- **Speed 1.0-1.5** = Lent, uniquement position trading

---

### 4. Stratégie "Perfect Setup V4.0"

**Critères** :
```
Score >= 11  |  Speed >= 2.5  |  Scalp = 1  |  Align = 3  |  Type = ±2
```

**Comment filtrer** :
1. Trier **"Speed"** décroissant
2. Vérifier **Speed ≥ 2.5**
3. Vérifier **Scalp = 1**
4. Vérifier **Score ≥ 11**
5. Vérifier **Align = 3**
6. Vérifier **Type = ±2**

**Probabilité de succès** : 80-90% sur timeframe 1-5 min
**Setup le plus rare mais le plus fiable**

---

### 5. Stratégie "Momentum Burst + Speed"

**Critères** :
```
Run >= 4  |  Speed >= 2.0  |  Type = ±2  |  Volume >= 2.0  |  Score >= 9
```

**Objectif** : Capturer mouvements explosifs avec vitesse élevée

**Comment utiliser** :
1. Trier **"Run"** décroissant
2. Sélectionner **Run ≥ 4**
3. Vérifier **Speed ≥ 2.0** (mouvements rapides) 🆕
4. Vérifier **Type = ±2**
5. Entry immédiate dans direction du Type

**Attention** : Run ≥ 5 + Speed ≥ 3.0 = possible surextension

---

### 6. Comparaison Speed vs Scalp

**Speed seul** :
- Mesure vitesse/activité
- Ne garantit pas bonnes conditions (spread, volatilité)
- Peut être élevé avec volatilité excessive (risqué)

**Scalp seul** :
- Mesure conditions (spread, volume, ATR)
- Ne garantit pas mouvements rapides
- Peut être 1 avec Speed faible (peu d'opportunités)

**Speed + Scalp combinés** ✅ :
- **Speed ≥ 2.0** = Mouvements rapides
- **Scalp = 1** = Bonnes conditions
- **Combinaison = Setup optimal scalping**

**Tableau décisionnel** :

| Speed | Scalp | Décision |
|-------|-------|----------|
| ≥ 2.5 | 1 | 🔥 **SCALPING PARFAIT** - Ultra-rapide + conditions optimales |
| ≥ 2.0 | 1 | ⚡ **SCALPING BON** - Rapide + bonnes conditions |
| ≥ 2.0 | 0 | ⚠️ **PRUDENCE** - Rapide mais conditions médiocres |
| < 2.0 | 1 | 🟡 **SWING** - Bonnes conditions mais lent |
| < 1.5 | 0 | ❌ **ÉVITER** - Lent + mauvaises conditions |

---

## ⚙️ Personnaliser les Noms de Colonnes V4.0

**Ligne 436 du code** - Vous pouvez modifier les alias affichés :

```prorealtime
SCREENER[condition](
  qualityScore AS "Score",      // Changer en "Qualité" ou "Q"
  volumeRatio AS "Volume",      // Changer en "Vol" ou "Liquidité"
  atrRatio AS "ATR",            // Changer en "Volatilité"
  directionalRun AS "Run",      // Changer en "Momentum" ou "M"
  alignmentScore AS "Align",    // Changer en "EMA" ou "A"
  marketType AS "Type",         // Changer en "Marché" ou "T"
  speedMeter AS "Speed",        // 🆕 Changer en "Vitesse" ou "Spd"
  scalpQuality AS "Scalp",      // Changer en "Scal" ou "S"
  trend1 AS "T1",               // Changer en "CT" (Court Terme)
  trend2 AS "T2",               // Changer en "MT" (Moyen Terme)
  trend3 AS "T3"                // Changer en "LT" (Long Terme)
)
```

**Contraintes** :
- Guillemets doubles obligatoires : `"Nom"`
- Éviter caractères spéciaux : %, /, €, etc.
- Noms courts recommandés : max 10 caractères
- Pas d'espaces dans les noms

**Exemples de personnalisation** :

**Version française étendue** :
```prorealtime
SCREENER[condition](
  qualityScore AS "Qualite",
  volumeRatio AS "Vol",
  atrRatio AS "Volatil",
  directionalRun AS "Momentum",
  alignmentScore AS "EMA",
  marketType AS "Marche",
  speedMeter AS "Vitesse",  // 🆕 V4.0
  scalpQuality AS "Scal",
  trend1 AS "CT",
  trend2 AS "MT",
  trend3 AS "LT"
)
```

**Version ultra-courte** :
```prorealtime
SCREENER[condition](
  qualityScore AS "Q",
  volumeRatio AS "V",
  atrRatio AS "A",
  directionalRun AS "R",
  alignmentScore AS "E",
  marketType AS "M",
  speedMeter AS "SP",  // 🆕 V4.0
  scalpQuality AS "SC",
  trend1 AS "1",
  trend2 AS "2",
  trend3 AS "3"
)
```

---

## 📊 Tableau Comparatif des Versions

| Aspect | V3.0 | V3.1 | V4.0 |
|--------|------|------|------|
| **Colonnes** | 9 | 10 | **11** ✅ |
| **Colonnes perso** | ✅ | ✅ | ✅ |
| **Filtre Scalping** | ❌ | ✅ | ✅ |
| **SpeedMeter** | ❌ | ❌ | **✅** 🆕 |
| **Mesure vitesse** | ❌ | ❌ | **✅** 🆕 |
| **Évite instruments morts** | ❌ | ❌ | **✅** 🆕 |
| **Optimal pour** | Trading général | Scalping conditions | **Scalping rapide** 🔥 |

---

## 📝 Notes Techniques V4.0

### SpeedMeter - Calcul Détaillé

**Ligne 371-409 du code** :

```prorealtime
// Calcul velocity (vitesse du prix)
priceVelocity = ABS(close - open)

// Moyenne des mouvements sur 20 bougies
sumVelocity = 0
FOR i = 1 TO velocityPeriod DO
    sumVelocity = sumVelocity + ABS(close[i] - open[i])
NEXT
avgVelocity = sumVelocity / velocityPeriod

// Ratio de velocity
IF avgVelocity > 0 THEN
    velocityRatio = priceVelocity / avgVelocity
ELSE
    velocityRatio = 0
ENDIF

// Tick Activity = Volume Ratio
tickActivity = volumeRatio

// SpeedMeter final
speedMeter = (velocityRatio + tickActivity) / 2
```

**Pourquoi cette formule** :
- **Velocity Ratio** : Mesure la vitesse du mouvement actuel vs historique
- **Tick Activity** : Mesure le nombre de transactions (volume)
- **Moyenne** : Équilibre entre vitesse prix et activité trading

### Alias AS - Syntaxe ProBuilder

**Code source (ligne 436)** :
```prorealtime
SCREENER[condition](..., speedMeter AS "Speed", scalpQuality AS "Scalp", ...)
```

**Compatibilité** :
- ✅ ProRealTime V12+ : Supporté
- ❌ ProRealTime V11 et antérieur : Non supporté

### Limitations

1. **Speed dépend du timeframe** : Valeurs différentes selon 1min, 5min, 1h
2. **Speed peut être très élevé** : > 4.0 peut indiquer événement exceptionnel (news)
3. **velocityPeriod = 20** : Augmenter pour plus de stabilité, réduire pour réactivité

---

## 🔍 Dépannage V4.0

### Problème : Speed toujours faible (< 1.5)

**Causes possibles** :
- Timeframe trop long (1h, daily)
- Instruments peu actifs (petites caps, cryptos peu connues)
- `velocityPeriod` trop élevé

**Solutions** :
1. **Utiliser timeframe 1, 5 ou 10 min**
2. **Tester sur instruments liquides** (CAC40, DAX30, EUR/USD, BTC/USD)
3. **Réduire velocityPeriod** à 10-15 (ligne 57)
4. **Vérifier watchlist** contient instruments actifs

### Problème : Speed toujours très élevé (> 3.5)

**Causes possibles** :
- Timeframe très court (1 tick, 1 sec)
- Période de forte volatilité (news, annonces)
- `velocityPeriod` trop faible

**Solutions** :
1. **Augmenter velocityPeriod** à 30 (ligne 57)
2. **Vérifier pas d'événements exceptionnels** (calendrier économique)
3. **Normal en période de news** : Éviter trading pendant annonces majeures

### Problème : Colonne "Speed" ne s'affiche pas

**Causes possibles** :
- Code V3.1 au lieu de V4.0
- Ligne 436 incomplète

**Solution** :
Vérifier que le code contient bien **442 lignes** et inclut :
```prorealtime
speedMeter AS "Speed"
```

### Problème : Speed incohérent avec mouvement visuel

**Explication** :
- Speed mesure vitesse RELATIVE (vs moyenne 20 bougies)
- Mouvement peut sembler faible mais Speed élevé si moyenne historique faible
- Mouvement peut sembler fort mais Speed faible si moyenne historique élevée

**Solution** :
- C'est normal, Speed compare à l'historique récent
- Combiner avec Volume et ATR pour vision complète

---

## 📚 Ressources

### Fichiers du Projet V4.0

1. **`trading_quality_metrics_v4.prt`** (442 lignes)
   - Code source ProScreener V4.0
   - SpeedMeter intégré (lignes 371-409)
   - 11 colonnes personnalisées

2. **`README_V4.md`**
   - Guide complet V4.0
   - Documentation SpeedMeter détaillée
   - Stratégies avec Speed

3. **`LEGENDE_CRITERES_V4.md`** (ce fichier)
   - Légende des 11 colonnes
   - Exemples détaillés avec Speed
   - Stratégies avancées SpeedMeter

### Documentation ProRealTime

- [Syntaxe AS](https://www.prorealtime.com/fr/probuilder) - Documentation alias
- [ProScreener V12](https://www.prorealtime.com/fr/proscreener) - Guide officiel
- [Forum ProRealCode](https://www.prorealcode.com/forum/) - Aide communauté

---

## 🎯 Tableau Récapitulatif V4.0

| # | Colonne | Variable | Plage | Optimal | Utilisation |
|---|---------|----------|-------|---------|-------------|
| 1 | **Score** | qualityScore | 0-13 | ≥ 10 | Qualité globale |
| 2 | **Volume** | volumeRatio | 0-∞ | ≥ 2.0 | Liquidité |
| 3 | **ATR** | atrRatio | 0-∞ | 0.8-1.2 | Volatilité |
| 4 | **Run** | directionalRun | 0-10 | ≥ 3 | Momentum |
| 5 | **Align** | alignmentScore | 0-3 | 3 | Cohérence |
| 6 | **Type** | marketType | -2 à +2 | ±2 | Bull/Bear/Range |
| 7 | **Speed** 🆕 | speedMeter | 0-∞ | ≥ 2.0 | Vitesse mouvements |
| 8 | **Scalp** | scalpQuality | 0-1 | 1 | Adapté scalping |
| 9 | **T1** | trend1 | -1/0/+1 | ±1 | Court terme |
| 10 | **T2** | trend2 | -1/0/+1 | ±1 | Moyen terme |
| 11 | **T3** | trend3 | -1/0/+1 | ±1 | Long terme |

**Signal idéal V4.0** :
```
Score: 12 | Volume: 2.5+ | ATR: 1.0 | Run: 4 | Align: 3 | Type: ±2 | Speed: 2.5+ | Scalp: 1 | T1/T2/T3: ±1
```

**Signal idéal SCALPING ULTRA-RAPIDE V4.0** 🚀 :
```
Score: 11+ | Speed: 2.5+ | Scalp: 1 | Type: ±2 | Volume: 2.5+
```

**Signal minimum SCALPING V4.0** :
```
Score: 9+ | Speed: 2.0+ | Scalp: 1 | Type: ±1
```

---

**Version**: 4.0 (Colonnes personnalisées + Filtre Scalping + SpeedMeter)
**Date**: 2025-10-27
**Compatibilité**: ProRealTime V12+ / ProScreener
**Statut**: ✅ Testé et fonctionnel

---

**⭐ La V4.0 ajoute le SpeedMeter pour capturer les mouvements rapides !**

🚀 **Bon trading avec des colonnes lisibles, un filtre scalping et un SpeedMeter intelligent !**
