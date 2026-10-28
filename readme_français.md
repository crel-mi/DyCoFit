# DyCoFit

**Version 1.0.0** (2026-10-28)

Outil d'analyse de vidéos hautes vitesses pour l'évaluation des traumas par effet-arrière (BABT - Behind Armour Blunt Trauma) lors d'essais d'impact sur bloc de gel SEBS.

![DyCoFit Logo](icons/Dycofit_logo_name.png)

## Description

Logiciel d'analyse vidéo pour l'évaluation des traumas par effet-arrière (BABT) dans les essais d'impact sur bloc de gel SEBS.

Les essais balistiques sur blocs de gel SEBS mesurent la déformation de l'équipement de protection pour évaluer le risque de traumas par effet-arrière. L'imagerie haute vitesse capture la formation dynamique du cône, à partir duquel le DBFD et l'ETP sont dérivés comme critères de risque lésionnel :
- **DBFD** (Dynamic Back Face Deformation / Cone dynamique d'enfoncement) : profondeur maximale du cône d'enfoncement en mm — indicateur principal du risque de traumas par effet-arrière
- **ETP** (Energy Transmission Parameter / Paramètre de transmission d'énergie) : critère pseudo-visqueux en m/s, combinant déplacement et vitesse

Le logiciel fournit un workflow complet, de l'importation des images jusqu'à l'export des résultats dans plusieurs formats.

## Installation

### Installation initiale

La version compilée distribuée par le Ministère de l'intérieur constitue la version officielle de DyCoFit. Elle doit être utilisée en priorité pour toute exécution du programme. Aucune license MATLAB n'est requise.

1. Exécuter le programme d'installation DyCoFit (`DycoFit_Setup.exe`)
2. Le programme d'installation configure DyCoFit et le MATLAB Runtime automatiquement
3. Lancer DyCoFit depuis le menu Démarrer ou le raccourci du bureau

### Exécution de DyCoFit

- Exécuter `DyCoFit.exe` depuis le répertoire d'installation
- Aucune configuration supplémentaire requise

## Exemple de jeu de données

Un jeu de données d'exemple est fourni dans le dossier example_dataset/ pour vous permettre de vous entraîner et de vérifier vos résultats. Le jeu de données contient :

- Séquence d'images TIFF provenant d'un test d'impact
- Les paramètres d'essais dans test_parameters.txt
- Résultats de référence (DBFD: ~54.39 mm, ETP: ~6.38 m/s) et des captures d'écran

Comment l'utiliser

1. Ouvrir DyCoFit
2. Naviguer vers le dossier example_dataset/
3. Sélectionner n'importe quel fichier .tif et cliquer sur Ouvrir
4. Suivre la procédure standard pour analyser la vidéo
5. Comparer vos résultats avec les valeurs de référence

Cet exemple illustre un essai d'impact typique.

## Comment utiliser

### Vue d'ensemble

Cet outil traite les enregistrements vidéo haute vitesse issus d'essais d'impact sur bloc de gel SEBS. Il importe des séquences d'images (`.tif`), calcule le déplacement de la paroi du bloc et exporte les résultats dans plusieurs formats.

### Fichiers d'entrée

1. Placer tous les fichiers `.tif` d'un seul essai dans un même dossier
2. Le nom du dossier sera utilisé pour créer des sous-répertoires où les fichiers de sortie seront sauvegardés

### Procédure

#### 1. Lancer DyCoFit

- Exécuter l'exécutable compilé (`DyCoFit.exe`)
- Dans la boîte de dialogue de sélection de fichier, choisir **File type → .tif** et sélectionner n'importe quelle image du dossier ; toutes les images seront chargées automatiquement

Une interface "Image processing" s'ouvrira.

#### 2. Pré-traitement de l'image

Ajuster les paramètres suivants si nécessaire pour améliorer la qualité de l'analyse :

- **Gain** : Accentue les contours (par défaut : 1)
- **Gamma** : Ajuste le facteur de contraste (par défaut : 1)

##### Découper la vidéo

Limiter l'analyse aux images contenant les événements d'impact pertinents :
- **Start** : Première image où le projectile est positionné devant l'équipement de protection et le bloc (pré-impact)
- **End** : Image peu après l'enfoncement maximal, lorsque le cône commence à réduire

Lorsque les ajustements sont terminés, cliquer sur **OK**.

#### 3. Définir le système de coordonnées et la ROI

Une fenêtre vidéo apparaîtra avec des commandes d'affichage :

1. Activer **Display axes** et **Display Ruler**
2. Cliquer sur **Enlarge** pour zoomer l'image
3. Aligner l'axe X (horizontal) avec la trajectoire du projectile
4. Aligner l'axe Z (vertical) avec l'interface entre l'équipement testé et le bloc
5. Placer la règle sur les marques de calibration du réglet

6. Utiliser **Cursor → ROI** pour délimiter la région contenant tout le cône d'enfoncement (largeur totale et profondeur)

#### 4. Réglage des paramètres expérimentaux

Une interface "Experimental Parameters" apparaîtra :

| Paramètre | Description | Valeur typique |
|-----------|-------------|----------------|
| Deformation threshold | Déplacement minimum pour déterminer le début de l'enfoncement réel ; régler près du premier point après l'impact | ~2 mm |
| Volume deformation | Valeur X à laquelle le cône devient régulier sans bruit (par défaut : 10 mm) | ~10 mm |
| Gel block thickness | Épaisseur du bloc SEBS (par défaut : 300 mm) | 300 mm |
| Camera-to-block distance | Distance de la caméra à la face du bloc (par défaut : 1300 mm) | 1300 mm |
| Optical system | Sélectionner votre lentille dans le menu déroulant (ou rensigner une valeur custom) | 85 mm |

Cliquer sur **OK** pour valider et calculer les résultats.

#### 5. Visualiser les résultats

- Enfoncement maximal
- Vitesse
- ETP

##### Alignement temporel et ajustement

Uniquement si nécessaire, ajuster les résultats :
1. Cliquer sur **Options** dans la fenêtre de résultats
2. Modifier le **Time shift** pour aligner le début de la déformation avec t=0
3. Choisir une **Fitting option** pour ajuster le fit à la courbe de déplacement
4. Utiliser **Local max** s'il y a la présence d'un retour d'une vague de déformation qui fausse la mesure de l'enfoncement maximal. 

#### 6. Export des résultats

Le programme fournit plusieurs options d'export :

##### Export du rapport principal (Excel + PDF)

Cliquer sur le bouton d'export principal dans la fenêtre de résultats pour générer :
- **Fichier Excel (.xlsx)** : Données complètes avec toutes les métriques, graphes intégrés. Nécessite Microsoft Excel installé et activé.
- **Rapport PDF** : Rapport professionnel avec ID unique, date, version du programme, tableau des paramètres et toutes les métriques clés

##### Export des graphs et des données (FIG, JPEG, CSV)

- **Fichiers FIG** : Fichiers de figure MATLAB pour une re-modification
- **Images JPEG** : Graphes statiques pour rapports et présentations
- **Données CSV** : Données numériques brutes (temps, déplacement, vitesse, ETP)

## Métriques clés

### DBFD (Dynamic Back Face Deformation / Cone Dynamique d'Enfoncement)

La profondeur maximale du cône de déformation en millimètres. C'est la mesure principale utilisée pour évaluer le risque de BABT.

### ETP (Energy Transmission Parameter / Paramètre de transmission d'énergie)

Un critère pseudo-visqueux exprimé en m/s, dérivé du déplacement et de sa variation (vitesse) de la paroi du gel. L'équation mathématique est :

```
ETP = 1.3 * displacement * velocity / 255.5
```

Où :
- **1.3** est un préfacteur
- **255,5 mm** est la profondeur du thorax de l'adulte mâle moyen
- **displacement** est la déformation de la paroi du gel en mm
- **velocity** est le taux de déplacement en m/s

L'historique temporel de l'ETP fournit des informations sur la dynamique de transfert d'énergie pendant l'impact. Cette métrique, avec la DBFD, est utilisée pour évaluer le risque de blessures selon les normes du Ministère de l'Intérieur pour les essais de protection balistique.

> Bolduc M., Anctil B., Improved test methods for better protection, a BABT protocol proposal for STANAG 2920, Personal Armour Systems Symposium, Quebec, Canada, 2010

## Correction optique

Valeurs de correction optique pour différentes lentilles de caméra :

| Lentille de caméra | Correction [mm] |
|-------------------|-----------------|
| 50 mm             | 63.56           |
| 85 mm             | 180.4           |
| 55 mm             | 65.1            |
| Custom            | Défini par l'utilisateur |

## Conditions préalables

- Windows 11
- Microsoft Excel (pour l'export .xlsx) - doit être installé et activé
- MATLAB Runtime inclus avec la version compilée

## Contact / Support

Pour toute question, contacter:

- Gabriel Starzak-Tomon, CREL Ministère de l'intérieur
- Email: gabriel.starzak-tomon@interieur.gouv.fr
- Email générique : sailmi-crel@interieur.gouv.fr
  
## Licence

Ce projet est distribué sous la licence BSD 3-Clause. Voir le fichier LICENSE pour plus de détails.
