# AthlÉPS — Gestion Leçons & Évaluations
## Documentation utilisateur — Version 02

**Collège Pasteur · Application EPS Athlétisme**
Fichier unique HTML — fonctionne dans tout navigateur moderne, sans installation.

---

## Présentation générale

AthlÉPS est un outil de gestion pédagogique pour les cours d'EPS en athlétisme. Il centralise la gestion des classes, des leçons, des présences, du test 9 minutes, des évaluations et des propositions d'entraînement fractionné. Toutes les données sont sauvegardées automatiquement dans le navigateur (localStorage) — aucune connexion internet requise après l'ouverture du fichier.

---

## Navigation

L'application comporte **7 onglets** accessibles depuis la barre de navigation :

| Onglet | Fonction |
|---|---|
| 📚 Leçons | Création et gestion des leçons par classe |
| 🧑‍🤝‍🧑 Élèves & Présences | Gestion des élèves, import CSV, appel |
| ⚡ Fractionné | Programmes de fractionné et chrono live |
| 🏃 9 minutes | Test 9 min complet avec suivi en direct |
| ⭐ Évaluation | Grilles d'évaluation par leçon |
| 📈 Progressivité | Suivi longitudinal des performances de chaque élève |
| 💡 Proposition | Génération automatique de groupes et séances de fractionné |

---

## 1. Leçons

- Créer une ou plusieurs **classes** (nom, niveau, année scolaire).
- Pour chaque classe, créer des **leçons** numérotées avec titre, date et contenu pédagogique.
- Ajouter des **objectifs** à chaque leçon (tags supprimables).
- Sauvegarder, exporter en JSON ou imprimer en PDF.

---

## 2. Élèves & Présences

- Ajouter des élèves manuellement (prénom, nom, sexe, niveau, vitesse de référence km/h, notes médicales).
- **Importer en masse via CSV** — colonnes : `prénom`, `nom`, `sexe`, `niveau`, `vitesse`, `notes`. Séparateur virgule ou point-virgule.
- Pour chaque leçon, enregistrer les **présences** en un clic (Présent ✓ → Absent ✗ → Blessé 🩹).
- Bouton "Tous présents" pour initialiser rapidement l'appel.

---

## 3. Fractionné

- **Calculateur km/h → temps** : entrez une vitesse cible, les temps par distance (100 m à 1000 m) s'affichent automatiquement.
- Créer des **programmes de fractionné** personnalisés (distance, répétitions, allure cible).
- Constituer des **groupes d'élèves** et leur affecter un programme.
- Lancer un **chrono live** qui suit chaque groupe et affiche la progression de chaque répétition.

---

## 4. Test 9 minutes *(onglet principal — fonctionnalités étendues en V02)*

### 4.1 Configuration

Avant de lancer :

- Sélectionner la **classe** et la **leçon**.
- Choisir la **distance du tour de piste** : 200 m, 333 m ou 400 m.
- **Configurer le barème** (optionnel mais recommandé) : définir des paliers distance → note /20, avec possibilité de différencier par sexe (F / M / Tous). Les notes apparaîtront automatiquement dans les résultats.

### 4.2 Numérotation des élèves

Deux modes disponibles :

- **Attribution automatique** : numéros attribués aléatoirement aux élèves présents. Utile pour mélanger les dossards.
- **Saisie manuelle** : un formulaire liste tous les élèves pour entrer chaque numéro librement.

Les numéros sont persistants par classe et réutilisés d'une séance à l'autre sauf modification.

### 4.3 Chrono et arrêt

- **▶ Lancer** : démarre le compte à rebours de 9 minutes.
- **⏸ Pause** : met en pause (reprend là où il s'est arrêté).
- **⏹ Arrêter manuellement** : interrompt le test avant la fin des 9 min. Le temps réel écoulé est conservé pour le calcul des km/h — les résultats restent cohérents.
- **↺ Reset** : réinitialise toutes les données de la session.

### 4.4 Suivi en direct — liste

Le suivi se présente sous forme de **tableau trié par numéro** (ou alphabétiquement si pas de numéro). Chaque ligne affiche pour un élève :

| Colonne | Contenu |
|---|---|
| # | Numéro attribué à l'élève |
| Élève | Prénom, nom, badge blessé/absent |
| Tours | Nombre de tours complets enregistrés |
| Distance | Distance cumulée en mètres |
| km/h est. | Vitesse moyenne estimée en temps réel |
| Δ dernier tour | Delta de durée par rapport au tour précédent (▼ vert = accélération, ▲ rouge = ralentissement, = stable) |
| Dernier passage | Temps chrono du dernier tour enregistré |
| +1 | Bouton d'enregistrement d'un tour |

**Enregistrer un tour** : cliquer sur la ligne entière ou sur le bouton +1. La ligne clignote en vert pour confirmer.

### 4.5 Saisie des mètres du dernier tour

À l'arrêt du chrono (automatique ou manuel), un formulaire apparaît pour chaque élève actif afin de saisir les **mètres parcourus dans le tour en cours** (0 à tour − 1 mètres). Le total en mètres se calcule en temps réel.

### 4.6 Résultats et note

Après calcul :

- Classement complet avec médailles pour les 3 premiers.
- Distance totale, vitesse moyenne (km/h), **note /20** calculée automatiquement selon le barème configuré.
- Bouton **📊** sur chaque ligne : ouvre un graphique de la **vitesse tour par tour** de l'élève (vitesse en km/h pour chaque tour), utile pour analyser la régularité.

---

## 5. Évaluation

- Grille par élève et par leçon : **Échauffement** (★ 1–5), **Charge de travail** (★ 1–5), **Ressenti** (boutons), **Commentaire libre**.
- Résumé de classe en temps réel (moyennes, ressenti dominant).
- Export CSV de toutes les évaluations d'une leçon.

---

## 6. Progressivité *(nouveau — V02)*

Tableau de bord longitudinal par classe :

- Affiche toutes les **séances 9 min terminées** en colonnes.
- Pour chaque élève et chaque séance : distance, km/h, note /20, ressenti enregistré lors de l'évaluation.
- La **dernière performance** est mise en avant à droite du tableau.
- **Cliquer sur un élève** ouvre sa fiche détaillée :
  - Tableau complet de toutes ses performances (séance, distance, vitesse, note, ressenti, échauffement).
  - **Graphique d'évolution** de la distance réalisée sur les 9 min, séance par séance.

> Les données proviennent automatiquement des onglets 9 minutes et Évaluation — aucune double saisie.

---

## 7. Proposition *(nouveau — V02)*

Génération automatique de **groupes homogènes** et de **séances de fractionné adaptées** :

### Constitution des groupes

Les élèves sont répartis en **5 groupes** par niveau de vitesse croissant, calculé à partir :
- de la **moyenne des performances 9 min** si des séances ont été réalisées,
- ou de la **vitesse de référence** renseignée dans la fiche élève.

### Propositions de séances

Pour chaque groupe, 3 types de fractionné sont proposés automatiquement :

| Distance | Répétitions | Allure | Récupération |
|---|---|---|---|
| 100 m | 8× | Calculée sur la vitesse du groupe | 1,5× le temps de travail |
| 200 m | 6× | Calculée sur la vitesse du groupe | 1,5× le temps de travail |
| 400 m | 4× | Calculée sur la vitesse du groupe | 1,5× le temps de travail |

Les **allures cibles** et **temps de récupération** sont recalculés à chaque fois que de nouvelles données 9 min sont enregistrées.

---

## Sauvegarde et export

| Action | Bouton |
|---|---|
| Sauvegarde automatique | Toutes les 30 secondes + à chaque modification |
| Export JSON complet | ⬇ Exporter JSON (toutes les données) |
| Import JSON | Depuis la page Leçons — remplace toutes les données |
| Export CSV résultats 9 min | 📄 Exporter CSV (page 9 minutes) |
| Export CSV évaluations | 📄 Exporter CSV (page Évaluation) |
| Impression / PDF | 🖨 Exporter PDF (masque les éléments non pertinents) |

> **Conseil** : exportez régulièrement un fichier JSON comme sauvegarde de secours. En cas de changement de navigateur ou de nettoyage du cache, les données localStorage seraient perdues.

---

## Données élèves — format CSV d'import

```
prénom,nom,sexe,niveau,vitesse,notes
Alice,Martin,F,Intermédiaire,12.5,
Bob,Dupont,M,Avancé,14.0,asthme
Clara,Leroy,F,Débutant,,lunettes
```

- Seul le champ `prénom` est obligatoire.
- `sexe` : `F` ou `M`
- `vitesse` : vitesse de référence en km/h (utilisée pour les propositions si pas de données 9 min)
- Séparateur virgule ou point-virgule accepté.

---

## Compatibilité

- Navigateurs modernes : Chrome, Firefox, Edge, Safari.
- Fonctionne **hors ligne** une fois le fichier ouvert.
- Responsive mobile (adapté tablette pour l'usage terrain).

---

*AthlÉPS V02 — Collège Pasteur · Documentation mise à jour au regard des évolutions de la version 02*
