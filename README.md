# Analyse-de-la-Qualite-des-Eaux-Souterraines

Description
Ce projet vise à analyser la qualité des eaux souterraines dans une région du Nord du Maroc en utilisant trois indices de qualité de l'eau (IQEs) différents. Les données ont été collectées à partir de neuf puits entre 2016 et 2017.
Table des matières

Installation
Structure du projet
Utilisation
Méthodologie
Données
Résultats
Contribuer

Installation
Prérequis

Python 3.8 ou version ultérieure
pip (gestionnaire de paquets Python)

Configuration de l'environnement
bashCopy# Cloner le repository
git clone https://github.com/serrhiniabdellah/Analyse-de-la-Qualite-des-Eaux-Souterraines.git
cd Analyse-de-la-Qualit-des-Eaux-Souterraines

# Créer un environnement virtuel
python -m venv env

# Activer l'environnement virtuel
# Sur Windows
env\Scripts\activate
# Sur Linux/Mac
source env/bin/activate

# Installer les dépendances
pip install -r requirements.txt
Dépendances principales
txtCopypandas==2.0.0
numpy==1.24.0
matplotlib==3.7.0
seaborn==0.12.0
openpyxl==3.1.0
jupyter==1.0.0

Structure du projet

Analyse-de-la-Qualite-des-Eaux-Souterraines

├── data/

│   ├── WaterQuality.xlsx

│   └── Parametres.xlsx

├── notebooks/

│   └── analyse_qualite_eau.ipynb

├── requirements.txt

└── README.md

Utilisation
pythonCopyfrom src.indices import calculate_wawqi, calculate_wgwqi, calculate_owqi
import pandas as pd

# Charger les données
data = pd.read_excel('data/WaterQuality.xlsx')
params = pd.read_excel('data/Parametres1.xlsx')

# Calculer les indices
wawqi = calculate_wawqi(data, params)
wgwqi = calculate_wgwqi(data, params)
owqi = calculate_owqi(data, params)

# Afficher les résultats
print(f"WAWQI: {wawqi}")
print(f"WGWQI: {wgwqi}")
print(f"OWQI: {owqi}")
Méthodologie
Le projet utilise trois indices différents pour évaluer la qualité de l'eau :

WAWQI (Weighted Arithmetic Water Quality Index)

pythonCopydef calculate_wawqi(data, weights):
    """
    Calcule l'indice WAWQI
    WAWQI = ∑(Qi × Wi)
    """
    return sum(data['quality_rating'] * weights['normalized_weight'])

WGWQI (Weighted Geometric Water Quality Index)

pythonCopydef calculate_wgwqi(data, weights):
    """
    Calcule l'indice WGWQI
    WGWQI = ∏(Qi^Wi)
    """
    return np.prod(data['quality_rating'] ** weights['normalized_weight'])

OWQI (Oregon Water Quality Index)

pythonCopydef calculate_owqi(data, subindices):
    """
    Calcule l'indice OWQI
    OWQI = √(n / ∑(SI_i^2))
    """
    n = len(subindices)
    return np.sqrt(n / np.sum(subindices['SI']**2))
Données
Les données sont stockées dans deux fichiers Excel :

WaterQuality.xlsx : Contient les mesures des paramètres pour chaque puits
Parametres1.xlsx : Contient les poids et sous-indices pour chaque paramètre

Résultats
Les résultats sont interprétés selon les échelles suivantes :
## Interpretation of Results

## 1. WAWQI (Indice de Qualité de l'Eau par Moyenne Arithmétique Pondérée)

| Plage de Valeurs | Niveau de Qualité | Description |
|------------------|-------------------|-------------|
| WAWQI < 50 | Excellente | Eau de très haute qualité, parfaitement potable |
| 50 ≤ WAWQI ≤ 100 | Bonne | Eau potable nécessitant un traitement mineur |
| 101 ≤ WAWQI ≤ 200 | Médiocre | Eau nécessitant un traitement important |
| 201 ≤ WAWQI ≤ 300 | Très Médiocre | Eau fortement polluée nécessitant un traitement intensif |
| WAWQI > 300 | Impropre | Eau impropre à la consommation humaine |

## 2. WGWQI (Indice de Qualité de l'Eau par Moyenne Géométrique Pondérée)

| Plage de Valeurs | Niveau de Qualité | Description |
|------------------|-------------------|-------------|
| 90 ≤ WGWQI ≤ 100 | Excellente | Qualité optimale pour tous usages |
| 70 ≤ WGWQI ≤ 89 | Bonne | Convient à la plupart des usages |
| 50 ≤ WGWQI ≤ 69 | Moyenne | Nécessite un traitement pour certains usages |
| 25 ≤ WGWQI ≤ 49 | Mauvaise | Usage limité sans traitement important |
| 0 ≤ WGWQI ≤ 24 | Très Mauvaise | Inutilisable sans traitement majeur |

## 3. OWQI (Indice de Qualité de l'Eau de l'Oregon)

| Plage de Valeurs | Niveau de Qualité | Description |
|------------------|-------------------|-------------|
| 90 ≤ OWQI ≤ 100 | Excellente | Qualité exceptionnelle |
| 85 ≤ OWQI ≤ 89 | Bonne | Qualité satisfaisante |
| 80 ≤ OWQI ≤ 84 | Acceptable | Qualité acceptable avec surveillance |
| 60 ≤ OWQI ≤ 79 | Médiocre | Nécessite une attention particulière |
| 0 ≤ OWQI ≤ 59 | Très Médiocre | Qualité préoccupante nécessitant une intervention |


Contribuer

Fork le projet
Créer une branche pour votre fonctionnalité
Commiter vos changements
Pousser vers la branche
Ouvrir une Pull Request

Licence
Ce projet est sous licence MIT. Voir le fichier LICENSE pour plus de détails.
