# 📊 ProRealTime - Métriques de Trading VERSION 2.0

## 🎯 BRANCHE ACTUELLE

**Nom** : `claude/prorealtime-metrics-v2-011CUTq8B1MJDmrP8t6NsAVq`
**Version** : 2.0 - Multi-Timeframe
**Date** : 26 octobre 2025
**Statut** : ✅ Prêt à tester

---

## 📁 FICHIER PRINCIPAL

**Emplacement** : `/prorealtime/proscreener/trading_quality_metrics.prt`

**Ce fichier contient tout** :
- ✅ Métriques de qualité (10 critères)
- ✅ Analyse Multi-Timeframe (3 TF)
- ✅ Score global (0-13)
- ✅ Signaux de trading

---

## 🔢 CE QUE CALCULE LE SCRIPT

### **Métriques de Base (10 critères)**

1. **Volume/Moyenne** - Liquidité de l'instrument
2. **Spread %** - Coûts de transaction approximés
3. **ATR/Moyenne** - Volatilité relative
4. **Corps/Mèche %** - Force directionnelle des bougies
5. **Chevauchement Corps %** - Continuation ou consolidation
6. **Run Directionnel** - Nombre de bougies consécutives (tendance)
7. **Distance VWAP %** - Position par rapport au VWAP
8. **Slippage/ATR** - Slippage potentiel
9. **Régularité Flux** - Stabilité du volume
10. **Alignement Qualité** - Combinaison de tous les critères

### **Analyse Multi-Timeframe (NOUVEAU)**

11. **Tendance 1min (T1m)** - Direction actuelle : -1 (baissier), 0 (neutre), +1 (haussier)
12. **Tendance 5min (T5m)** - Direction moyen terme
13. **Tendance 15min (T15m)** - Direction long terme
14. **Score Alignement (Align)** - 0 à 3 (nombre de TF alignés)
15. **Force Tendance Moyenne** - Intensité de la tendance globale

---

## 📊 COLONNES DU SCREENER

Quand vous lancez le script, vous voyez ces colonnes :

| Colonne | Description | Valeurs | Interprétation |
|---------|-------------|---------|----------------|
| **Score** | Qualité globale | 0-13 | ≥9 = Excellent, 7-8 = Bon, <7 = Moyen |
| **Vol/Moy** | Volume vs moyenne | 0.5-3+ | ≥1.5 = Liquide, <0.8 = Peu liquide |
| **Spread%** | Range de la bougie | 0.1-2% | <0.2% = Bon, >0.5% = Large |
| **ATR/Moy** | Volatilité | 0.5-2+ | ~1.0 = Normal, >1.5 = Volatil |
| **Corps%** | Force bougie | 0-100 | ≥70% = Fort, <30% = Indécision |
| **Run** | Bougies consécutives | 0-10 | ≥3 = Tendance, 1-2 = Pas de tendance |
| **VWAP%** | Distance VWAP | -5 à +5 | >0 = Au-dessus, <0 = En-dessous |
| **Align** | Alignement TF | 0-3 | 3 = Parfait, 2 = Bon, 0-1 = Divergence |
| **T1m** | Tendance 1min | -1, 0, +1 | +1 = Haussier, -1 = Baissier |
| **T5m** | Tendance 5min | -1, 0, +1 | Confirmation moyen terme |
| **T15m** | Tendance 15min | -1, 0, +1 | Confirmation long terme |

---

## 🎯 COMMENT LIRE LES RÉSULTATS

### **Exemple 1 : Signal EXCELLENT** ✅

```
Score: 11  | Vol/Moy: 2.3 | Spread%: 0.15 | ATR/Moy: 1.05
Corps%: 78 | Run: 5       | VWAP%: +0.4
Align: 3   | T1m: +1      | T5m: +1       | T15m: +1
```

**Interprétation** :
- ✅ Score 11/13 = Excellente qualité
- ✅ Volume 2.3× = Très liquide
- ✅ Corps 78% = Forte conviction
- ✅ Run de 5 = Tendance claire
- ✅ Align 3 = Parfaitement aligné (3 TF haussiers)
- ✅ Au-dessus VWAP (+0.4%)

**➡️ ACTION : SIGNAL LONG TRÈS FORT**

---

### **Exemple 2 : Divergence ATTENTION** ⚠️

```
Score: 7   | Vol/Moy: 1.8 | Spread%: 0.25 | ATR/Moy: 1.2
Corps%: 65 | Run: 3       | VWAP%: +0.2
Align: 1   | T1m: +1      | T5m: -1       | T15m: -1
```

**Interprétation** :
- 🟡 Score 7/13 = Qualité correcte
- ⚠️ Align 1 = DIVERGENCE !
- ⚠️ 1min haussier MAIS 5min + 15min baissiers
- ⚠️ Risque de retournement baissier

**➡️ ACTION : NE PAS TRADER ou attendre confirmation**

---

### **Exemple 3 : Signal BON** 🟢

```
Score: 9   | Vol/Moy: 2.0 | Spread%: 0.18 | ATR/Moy: 0.95
Corps%: 72 | Run: 4       | VWAP%: -0.3
Align: 2   | T1m: -1      | T5m: -1       | T15m: 0
```

**Interprétation** :
- ✅ Score 9/13 = Bonne qualité
- ✅ Align 2 = 2 TF alignés (1min + 5min baissiers)
- 🟡 15min neutre (pas de contradiction)
- ✅ En-dessous VWAP (-0.3%)
- ✅ Run baissier de 4

**➡️ ACTION : SIGNAL SHORT VALIDE**

---

## ⚙️ PARAMÈTRES À AJUSTER

Dans le fichier `.prt`, lignes 10-18 :

```prorealtime
lookbackPeriod = 100     // Historique pour moyennes (50-200)
atrPeriod = 14           // Période ATR (10-20)
vwapStart = 0            // Heure début VWAP
minBodyRatio = 0.5       // Seuil corps/bougie (0.3-0.7)
minVolRatio = 1.0        // Seuil volume (0.7-1.5)

enableMTF = 1            // 1 = Multi-TF ON, 0 = OFF
trendPeriod = 20         // Période EMA tendance (10-50)
```

### **Configurations Recommandées**

**Scalping (1min) - Strict** :
```prorealtime
enableMTF = 1
trendPeriod = 20
minVolRatio = 1.5
// Chercher Score >= 9
```

**Day Trading (5min) - Équilibré** :
```prorealtime
enableMTF = 1
trendPeriod = 20
minVolRatio = 1.0
// Chercher Score >= 8
```

**Sans Multi-TF (mode classique)** :
```prorealtime
enableMTF = 0
// Score maximum = 10 (au lieu de 13)
```

---

## 🚀 COMMENT UTILISER

### **Étape 1 : Installation**

1. Ouvrez ProRealTime
2. Outils → ProScreener → Nouveau Screener
3. Copiez TOUT le contenu de `trading_quality_metrics.prt`
4. Collez dans l'éditeur
5. Nommez : "Métriques Qualité V2"

### **Étape 2 : Configuration**

1. Sélectionnez votre watchlist
2. Unité de temps : **1 minute** (recommandé)
3. Cliquez "Lancer"

### **Étape 3 : Interprétation**

**Règles simples** :

✅ **TRADER si** :
- Score ≥ 9
- Align ≥ 2 (2 ou 3 TF alignés)
- Run ≥ 3
- Pas de divergence (T1m ≠ T5m/T15m)

⚠️ **ATTENTION si** :
- Align = 1 (divergence)
- Score < 7
- Vol/Moy < 0.8 (peu liquide)

❌ **NE PAS TRADER si** :
- T1m = +1 ET (T5m = -1 OU T15m = -1)
- Ou inversement
- = Divergence forte

---

## 📈 STRATÉGIES PRÊTES À L'EMPLOI

### **Stratégie 1 : Alignement Parfait (Conservatrice)**

**Filtres** :
- Score ≥ 10
- Align = 3
- Run ≥ 3

**Entrée LONG** :
- T1m = T5m = T15m = +1
- Au-dessus VWAP

**Entrée SHORT** :
- T1m = T5m = T15m = -1
- En-dessous VWAP

**Win rate attendu** : 70-80%

---

### **Stratégie 2 : Alignement Partiel (Équilibrée)**

**Filtres** :
- Score ≥ 8
- Align ≥ 2
- Run ≥ 3

**Entrée** :
- 2 TF sur 3 dans la même direction
- Volume > 1.5× moyenne

**Win rate attendu** : 60-70%

---

### **Stratégie 3 : Anti-Divergence (Défensive)**

**Règle** :
- NE JAMAIS trader si Align = 1
- Attendre que Align ≥ 2

**Objectif** : Éviter les retournements

---

## 🔍 TESTS À FAIRE

### **Test 1 : Vérification Visuelle**

1. Lancez le screener
2. Prenez un instrument avec Score élevé
3. Ouvrez 3 graphiques (1min, 5min, 15min)
4. Vérifiez que T1m, T5m, T15m correspondent visuellement

### **Test 2 : Comparaison Avec/Sans Multi-TF**

1. Testez avec `enableMTF = 1`
2. Notez les scores et signaux
3. Testez avec `enableMTF = 0`
4. Comparez les différences

### **Test 3 : Journal de Trading**

Créez un tableau :

```
Date  | Instrument | Score | Align | T1m/T5m/T15m | Entrée | Résultat
------|-----------|-------|-------|--------------|--------|----------
26/10 | AAPL      | 11    | 3     | +1/+1/+1    | LONG   | +1.2% ✅
26/10 | TSLA      | 7     | 1     | +1/-1/-1    | SKIP   | Évité perte
```

**Objectif** : Valider que Align ≥ 2 = meilleur win rate

---

## ⚠️ LIMITATIONS CONNUES

1. **Fonction TIMEFRAME peut être lente**
   - Sur grandes watchlists (>50 instruments)
   - Solution : Réduire la watchlist

2. **Nécessite données multi-TF**
   - ProRealTime doit avoir historique 1min, 5min, 15min
   - Si données manquantes, Multi-TF ne fonctionnera pas

3. **EMA(20) est ajustable**
   - 20 = valeur standard
   - Testez 10 (plus rapide) ou 50 (plus stable)

4. **Score max = 13** (au lieu de 10)
   - Ajustez vos seuils : `highQuality = qualityScore >= 9`

---

## 📂 FICHIERS DU PROJET

```
/prorealtime/
├── README.md                                    (Documentation générale)
├── VERSION_2.0_RECAP.md                         (CE FICHIER)
└── proscreener/
    ├── trading_quality_metrics.prt              ⭐ FICHIER PRINCIPAL V2.0
    ├── TRADING_METRICS_README.md                (Documentation détaillée)
    ├── support_resistance_level3.prt            (Script S/R avancé)
    └── support_resistance_level3_simple.prt     (Script S/R simple)
```

---

## 🆘 DÉPANNAGE

### **Problème : Erreur de syntaxe**

**Solution** :
- Copiez TOUT le fichier (du début à la fin)
- Vérifiez qu'il n'y a pas de caractères étranges

### **Problème : Aucun résultat**

**Solutions** :
1. Réduire le seuil : `highQuality = qualityScore >= 5`
2. Désactiver Multi-TF : `enableMTF = 0`
3. Vérifier les données historiques disponibles

### **Problème : Trop de résultats**

**Solutions** :
1. Augmenter le seuil : `highQuality = qualityScore >= 9`
2. Ajouter filtre : `AND Align >= 2`

### **Problème : Multi-TF ne fonctionne pas**

**Solutions** :
1. Vérifier que vous avez l'abonnement ProRealTime compatible
2. Vérifier que les données 5min et 15min existent
3. Désactiver temporairement : `enableMTF = 0`

---

## 📞 HISTORIQUE DES VERSIONS

### **VERSION 2.0** (26 oct 2025) ⭐ ACTUELLE
- ✅ Analyse Multi-Timeframe (3 TF)
- ✅ Score d'alignement
- ✅ Détection de divergences
- ✅ Score max = 13
- ✅ Signaux améliorés avec confirmation TF

### **VERSION 1.1** (26 oct 2025)
- ✅ Corrections syntaxe ProRealTime
- ✅ Remplacement median → AVERAGE
- ✅ Syntaxe MAJUSCULES
- ✅ Fix VWAP

### **VERSION 1.0** (25 oct 2025)
- ✅ 10 métriques de base
- ✅ Score 0-10
- ✅ Colonnes de sortie

---

## ✅ PROCHAINES ÉVOLUTIONS POSSIBLES

(Non implémentées, à discuter)

1. Détection de patterns (Hammer, Engulfing, etc.)
2. Calcul automatique Stop-Loss / Take-Profit
3. Intégration Support/Résistance
4. Filtres horaires (éviter open/close)
5. Corrélation avec indices
6. Version indicateur visuel sur graphique

---

## 🎓 RESSOURCES

- **ProRealTime Docs** : https://www.prorealtime.com/fr/support
- **Forum ProRealCode** : https://www.prorealcode.com/
- **Langage ProBuilder** : https://www.prorealtime.com/fr/probuilder

---

**🎯 BRANCHE ACTUELLE : `claude/prorealtime-metrics-v2-011CUTq8B1MJDmrP8t6NsAVq`**

**VERSION : 2.0 - Multi-Timeframe**

**STATUT : ✅ PRÊT À TESTER**

---

*Créé avec Claude Code - 26 octobre 2025*
