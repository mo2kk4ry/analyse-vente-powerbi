# analyse-vente-powerbi
# 📊 Tableau de Bord Power BI – Analyse des Ventes

## Description

Ce projet Power BI a été réalisé dans le cadre d'un atelier pratique d'analyse de données. Il couvre l'ensemble du pipeline BI : importation et nettoyage des données dans Power Query, modélisation relationnelle, création de mesures DAX, et construction d'un tableau de bord interactif multi-onglets avec navigation, filtres, info-bulles et sécurité par rôles.

---

## 📁 Contenu du projet

```
projet-powerbi/
│
├── data/
│   └── sales_2.csv               # Jeu de données source
├── dashboard/
│   └── rapport_ventes.pbix       # Fichier Power BI principal
├── theme/
│   └── theme.json                # Thème personnalisé importé
├── icons/                        # Icônes utilisées dans le menu et les signets
└── README.md
```

---

## 🔧 Étapes réalisées

### 1. Importation & Qualité des données
- Importation du fichier `sales_2.csv` dans Power Query
- Analyse via les outils : Qualité des colonnes, Distribution, Profil
- Vérification et correction des types de données
- Renommage des colonnes avec des libellés explicites (ex. `OrderID` → `Id commande`)

### 2. Normalisation (Power Query)
Création de tables de référence à partir de la table brute :

| Table | Colonnes |
|-------|----------|
| **Clients** | Id client, Nom client |
| **Produits** | Id produit, Nom produit, Catégorie produit |
| **Régions** | Id région, Nom région |
| **Ventes** | Table principale (colonnes redondantes supprimées) |

### 3. Modèle de données
- Vérification et création manuelle des relations entre tables
- Modèle en étoile : table **Ventes** au centre, reliée aux tables de dimension

### 4. Mesures DAX

**Onglet Suivi des ventes :**
```dax
Total ventes = SUM(Ventes[Prix total])
Nombre de commandes = DISTINCTCOUNT(Ventes[Id commande])
Quantité vendue = SUM(Ventes[Quantité])
Commande moyenne = DIVIDE([Total ventes], [Nombre de commandes])
```

**Onglet Commandes annulées :**
```dax
Total commandes annulées =
    CALCULATE(COUNT(Ventes[Id commande]), Ventes[Statut commande] = "Cancelled")

Montant commandes annulées =
    CALCULATE(SUM(Ventes[Prix total]), Ventes[Statut commande] = "Cancelled")

Pourcentage commandes annulées =
    DIVIDE([Total commandes annulées], [Nombre de commandes])
```

---

## 📈 Dashboard

### Onglet 1 – Suivi des ventes
- 4 KPI : Total ventes, Nombre de commandes, Quantité vendue, Commande moyenne
- Graphique en courbe/aires : évolution du CA et des volumes dans le temps
- Graphique en barres horizontales : répartition du CA par région
- Graphique en Donut : répartition du CA par catégorie de produit
- Tableau détaillé des commandes
- Filtres : plage de dates, statut de commande, région

### Onglet 2 – Commandes annulées
- 3 KPI spécifiques aux commandes annulées
- Courbe d'évolution du % de commandes annulées
- Histogramme vertical : part des annulations par région
- Treemap : CA annulé par catégorie et par produit
- Graphique Ruban : évolution trimestrielle des annulations par produit

### Navigation & UX
- Menu latéral avec icônes et liens vers chaque onglet
- Info-bulles avancées (tooltips) sur l'histogramme régions et le donut catégories
- Thème personnalisé (`#1E2D38` fond, `#232448` briques)

---

## ⭐ Fonctionnalités bonus

- **Donut KPI personnalisé** : affichage du % de données filtrées (PayPal KPI Donut Chart)
- **Signets (Bookmarks)** :
  - Filtre Mobiles (Smartphone, Headphone, SmartWatch)
  - Filtre Bureautique (Tablet, Monitor, Laptop, Keyboard, Mouse)
  - Réinitialisation de tous les filtres
- **Sécurité par rôles (RLS)** :
  - Rôle 1 : accès limité aux sociétés *AI Systems* et *TechCorp*
  - Rôle 2 : accès limité à la région *South*
- **Version mobile** : mise en page adaptée pour l'onglet Suivi des ventes
- **Publication** sur Power BI Service

---

## 🛠️ Technologies utilisées

- **Power BI Desktop**
- **Power Query** – nettoyage et transformation des données
- **DAX** – création des mesures et indicateurs
- **Power BI Service** – publication du rapport

---

## 👤 Auteure

- **Sanaba Kanté** – étudiante en analyse de données

---

## 📄 Licence

Ce projet est réalisé à des fins éducatives uniquement.
