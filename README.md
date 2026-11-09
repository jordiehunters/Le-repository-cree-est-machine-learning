# Application Streamlit — quatre travaux de machine learning

Cette application réunit les deux exemples du professeur et les deux travaux sur les voitures :

| Travail | Cible | Modèles inclus |
|---|---|---|
| Téléphones — classification | `etat` | Régression logistique, arbre de décision, forêt aléatoire |
| Taxis — régression | `Trip_Price` | Régression linéaire, Ridge, arbre de décision, forêt aléatoire |
| Voitures — classification | `Venant_Occasion` | Régression logistique, Ridge Classifier, arbre de décision, forêt aléatoire |
| Voitures — régression | `Selling_Price` | Régression linéaire, Ridge, arbre de décision, forêt aléatoire |

Chaque modèle propose une **prédiction simple** et une **prédiction multiple par CSV**. Pour chaque interface multiple, l'application fournit un modèle CSV à remplir et un fichier de résultats téléchargeable.

## Lancer localement

1. Installer Python 3.10 ou plus récent.
2. Ouvrir un terminal dans le dossier `streamlit_car_models`.
3. Installer les dépendances :

   ```bash
   pip install -r requirements.txt
   ```

4. Lancer l'application :

   ```bash
   streamlit run app.py
   ```

Streamlit entraîne en mémoire les modèles du travail sélectionné. Les modèles des notebooks où les meilleurs paramètres étaient disponibles reprennent ces paramètres. Pour le notebook Taxi, dont les cellules de résultats étaient vides, l'application lance les recherches GridSearchCV du professeur sur le CSV chargé. Ce premier entraînement peut prendre un peu de temps ; il est mis en cache ensuite.

## Déployer avec GitHub et Streamlit Community Cloud

Après avoir extrait le ZIP, depuis un terminal ouvert dans `streamlit_car_models`, crée un dépôt Git et envoie les fichiers sur un dépôt GitHub vide :

```bash
git init
git add .
git commit -m "Ajouter l'application Streamlit de machine learning"
git branch -M main
git remote add origin https://github.com/TON_UTILISATEUR/NOM_DU_DEPOT.git
git push -u origin main
```

Remplace `TON_UTILISATEUR` et `NOM_DU_DEPOT` par tes informations GitHub. Ensuite, dans Streamlit Community Cloud, crée une nouvelle application, sélectionne ce dépôt, la branche `main` et le fichier `app.py`, puis lance le déploiement.

## Fichiers CSV de prédiction multiple

Dans l'onglet **Prédiction multiple**, télécharge le modèle CSV proposé, remplis une ligne par téléphone, trajet ou voiture, puis importe le fichier. Garde les noms de colonnes du modèle. La cible est facultative ; si elle est fournie, l'application ajoute une comparaison entre valeur réelle et prédite.

## Préparation et limites des données

Les CSV sont fournis dans `data/`. La préparation suit les notebooks : catégories encodées avec `LabelEncoder`, `MinMaxScaler` pour les téléphones et `RobustScaler` pour les autres travaux. Pour le CSV Taxi, les 49 lignes sans `Trip_Price` sont exclues de l'entraînement, les catégories manquantes sont remplacées par leur mode et les valeurs numériques manquantes des caractéristiques sont estimées par KNN. La cible n'est jamais imputée.

Les valeurs extrêmes ne sont pas remplacées automatiquement. Le dataset de classification des voitures contient des prix très atypiques ; vérifie les annonces concernées à la source avant un usage commercial. `LabelEncoder` attribue des codes sans ordre réel aux marques, adresses et catégories ; l'application refuse une catégorie inconnue plutôt que de lui attribuer silencieusement un code.
