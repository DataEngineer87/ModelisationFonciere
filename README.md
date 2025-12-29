<a href="images/AppStreamlit.pdf">
  <img src="images/immo.jpg" alt="Aperçu du PDF" width="800"/>
</a>

# Description

Cette application web interactive développée avec Streamlit permet d’explorer les données publiques DVF (Demandes de Valeurs Foncières) et d’estimer le prix des biens immobiliers en France. Elle combine visualisations dynamiques et prédictions basées sur un modèle de machine learning entraîné.

# Fonctionnalités principales

- Exploration des données DVF par zone géographique (département, commune)

- Visualisation interactive des distributions de prix, surfaces, et types de biens

- Prédiction en temps réel du prix d’un bien immobilier (appartement ou maison) selon ses caractéristiques (surface, localisation, type, etc.)

- Chargement et traitement des données optimisés pour gérer les gros fichiers

- Interface utilisateur simple, intuitive et responsive

  # Stack Technique

| Technologie       | Usage                                       |
| ----------------- | ------------------------------------------- |
| Python            | Langage principal                           |
| Streamlit         | Framework web interactif                    |
| Pandas, GeoPandas | Manipulation et traitement des données      |
| Scikit-learn      | Modélisation et prédiction machine learning |
| Joblib            | Sérialisation du modèle                     |
| Plotly            | Visualisations graphiques interactives      |


### Téléchargement du modèle
Le modèle initial Model_DVF.pkl (3,4 Go) était trop volumineux pour être stocké directement sur GitHub.
La version compressée model_DVF_compress.pkl constitue une version optimisée du modèle original : elle est allégée, compressée et intégrée directement au dépôt GitHub, ce qui permet un chargement plus rapide et un déploiement simplifié.

### Notebook utilitaire
Un notebook utils.ipynb est inclus dans ce projet pour centraliser les fonctions réutilisables, les scripts d’aide au prétraitement, à l’analyse exploratoire, ou à la visualisation. Ce notebook facilite la maintenance et la modularité du code en regroupant les éléments communs utilisés tout au long du projet.
### Exemple d’utilisation du notebook utils.ipynb  
Dans un autre notebook ou script Python, vous pouvez importer les fonctions du notebook utilitaire comme suit :
### Importation des fonctions définies dans le fichier utils.ipynb
import Utils 
### Fonction Convertir_colonnes_booleennes_en_entiers

def convert_bool_to_numeric(df):

    for col in df.select_dtypes(include='bool').columns:
    
        df[col] = df[col].astype(int)
        
    return df
    
df_train = Utils.convert_bool_to_numeric(df_train_cleaned)

# Résultats des Modèles entraînés

Plusieurs algorithmes de machine learning ont été testés afin de prédire le prix des biens immobiliers à partir des données DVF.
Les performances ont été évaluées selon MAE (Mean Absolute Error), RMSE (Root Mean Squared Error) et R² (Coefficient de détermination).

# Résumé des performances
| Modèle                    | MAE (erreur absolue) | RMSE (erreur quadratique) | R²                 |
| ------------------------- | -------------------- | ------------------------- | -------------------|
|**Random Forest**          | **2 667.65**         | **13 234.29**             | **0.9802**         |
|XGBoost                    | 45 024.78            | 59 408.19                 | 0.6008             |
|Hist Gradient Boosting     | 46 122.45            | 60 829.58                 | 0.5814             |

# Interprétation

Random Forest surpasse largement les autres modèles avec un R² de 0.98 et une faible erreur (MAE et RMSE).

XGBoost et Hist Gradient Boosting présentent des performances beaucoup plus faibles.

Le modèle Random Forest a donc été retenu pour la mise en production dans l’application Streamlit.


# Utilisation

Lancer l’application Streamlit :

streamlit run APP_DFV.py
## Auteur
**Alseny — Data Scientist confirmé orienté MLOps & GenAI**
