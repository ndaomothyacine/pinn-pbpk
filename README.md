# Physics-Informed Neural Networks pour la modélisation pharmacocinétique (PBPK)

Projet de recherche appliquée réalisé dans le cadre de la formation d'ingénieur MAM5 (Mathématiques Appliquées et Modélisation) à **Polytech Lyon**, sous la direction de M. Ciuperca.

> Auteur : Moth Yacine NDAO - Année universitaire 2025-2026

## Le problème

La modélisation pharmacocinétique physiologique (**PBPK**) décrit comment un médicament se distribue dans l'organisme, en s'appuyant sur des principes physiologiques. Mais calibrer ces modèles est difficile : certains paramètres ne sont pas mesurables *in vivo*, les observations sont partielles, et les problèmes d'identifiabilité rendent l'estimation fragile.

Ce projet explore une approche récente pour résoudre ce problème : les **Physics-Informed Neural Networks (PINNs)**, introduits par Raissi et al. (2019), qui combinent apprentissage profond et contraintes physiques pour résoudre simultanément :
- le problème direct (prédire l'évolution des concentrations),
- le problème inverse (estimer les paramètres physiologiques du modèle).

## Ce qui a été fait

- Modélisation d'un système à **4 compartiments corporels** (sang cérébral, tissu cérébral, LCR crânien, LCR spinal), sous forme d'équations différentielles ordinaires (EDO)
- Comparaison de **deux formulations** :
  - un modèle **linéaire à 9 paramètres** (approche phénoménologique)
  - un modèle **PBPK biophysique à 4 paramètres** (approche mécanistique, basée sur des volumes physiologiques réels)
- Implémentation d'un PINN en **PyTorch** : réseau fully-connected (1 → 6×50 neurones → 4), fonction de perte multi-objectifs combinant fidélité aux données, conditions initiales, et respect des équations différentielles (calculé par différentiation automatique)
- Génération de données synthétiques bruitées (2% de bruit gaussien, observations partielles) pour tester la robustesse du modèle
- Analyse d'**identifiabilité paramétrique** via la matrice de corrélation des paramètres estimés

## Résultats

- Modèle linéaire : reconstruction fidèle des profils de concentration, erreur paramétrique moyenne de **5.4%**
- Modèle PBPK : reconstruction correcte mais avec une sous-estimation des pics rapides, erreur paramétrique moyenne de **12.0%**
- Mise en évidence d'une forte corrélation entre deux paramètres du modèle PBPK (ρ = 0.87), révélant une non-identifiabilité intrinsèque malgré une bonne identification de leur combinaison fonctionnelle

## Stack technique

- **Python / PyTorch** — implémentation du PINN et différentiation automatique
- **NumPy / SciPy** — génération des données synthétiques (résolution par Runge-Kutta)
- **Matplotlib** — visualisation des trajectoires et comparaisons

## Contenu du repo

- `PINN_PBPK.ipynb` — notebook complet (implémentation, entraînement, résultats)
- `Rapport_Projet_PINNs.pdf` — rapport détaillé (contexte, méthodologie, résultats, discussion)

## Statut

Projet terminé, réalisé individuellement.
