# AthlÉPS — Gestion Leçons & Évaluations

**Version :** V2 / R1  
**Fichier HTML :** `AthlEPS_Lecons_V2_index.html`  
**Auteur :** Louis Odilon Schneider — Collège Pasteur, Villemomble  
**Déploiement :** GitHub Pages (`louisodilonschneider-web`)

---

## Nouveautés V2

- **Fiche élève enrichie** : vitesse de référence (km/h) + notes/infos médicales, modifiables à tout moment via bouton ✏️
- **Calculateur km/h → temps** intégré dans le Fractionné : saisir une vitesse, les temps sur 100/200/300/400/500/600/800/1000 m se calculent instantanément
- **Saisie km/h dans les programmes** : en mode fixe et évolutif, on peut entrer directement la vitesse cible au lieu de l'allure M:SS (km/h prime sur allure si saisi)
- **Affichage km/h en live** dans les cartes de suivi Fractionné (temps attendu + km/h cible visibles)
- **Export PDF** via `🖨 Exporter PDF` (impression navigateur → Enregistrer en PDF) depuis chaque onglet
- **Sauvegarde renforcée** : auto-save toutes les 30 secondes + sauvegarde avant fermeture de page (`beforeunload`)
- **Import/Export JSON bidirectionnel** : bouton import JSON pour restaurer une sauvegarde
- **Tableau élèves enrichi** : colonnes vitesse réf. et notes, bouton ✏️ pour modifier sans supprimer

---

## Structure des données JSON (localStorage + export)

Clé localStorage : `athleps_lecons_v2`

```json
{
  "classes": [
    {
      "id": "_abc123",
      "name": "5ème A — EPS",
      "niveau": "5ème",
      "annee": "2025–2026"
    }
  ],

  "eleves": {
    "<classeId>": [
      {
        "id": "_xyz789",
        "prenom": "Alice",
        "nom": "Martin",
        "sexe": "F",
        "niveau": "Intermédiaire",
        "vitesse": 12.5,
        "notes": "Asthme léger"
      }
    ]
  },

  "lecons": {
    "<classeId>": [
      {
        "id": "_lem456",
        "titre": "Leçon 3 — Endurance",
        "date": "2026-04-10",
        "num": 3,
        "objectifs": [
          "Maintenir une allure régulière sur 400 m",
          "Gérer l'effort sur la durée"
        ],
        "contenu": "Échauffement 10 min, fractionné 6×200 m…"
      }
    ]
  },

  "presences": {
    "<leconId>": {
      "<eleveId>": "present"
    }
  },

  "evaluations": {
    "<leconId>": {
      "<eleveId>": {
        "echauffement": 4,
        "charge": 3,
        "ressenti": "😊 Bien",
        "commentaire": "Bonne gestion de l'effort, à encourager"
      }
    }
  },

  "fracProgs": [
    {
      "id": "fp_1234567890",
      "name": "Groupe B — 12 km/h",
      "tours": 6,
      "mode": "fixed",
      "steps": [
        {
          "dist": 200,
          "allureMs": 60000,
          "recupMs": 90000,
          "recupType": "marche"
        }
      ]
    }
  ],

  "fracGroupsByLecon": {
    "<leconId>": [
      {
        "id": "_grp001",
        "name": "Groupe A",
        "color": "#1a2b6b",
        "members": ["Alice", "Bob", "Chloé"]
      }
    ]
  },

  "fracGroupAssign": {
    "<groupId>": "<progId>"
  },

  "currentClasseId": "<classeId>",
  "currentLeconId":  "<leconId>"
}
```

### Notes sur les champs

| Champ | Type | Description |
|-------|------|-------------|
| `vitesse` | `number \| null` | Vitesse de référence de l'élève en km/h |
| `notes` | `string` | Informations médicales ou pédagogiques |
| `echauffement` | `0–5` | Note étoiles (0 = non noté) |
| `charge` | `0–5` | Note étoiles |
| `ressenti` | `string` | L'une des 5 valeurs emoji prédéfinies ou vide |
| `allureMs` | `number` | Durée en ms pour réaliser `dist` mètres à l'allure cible |
| `recupMs` | `number` | Durée de récupération en ms |
| `recupType` | `"marche"\|"trot"\|"pause"` | Type de récupération |

---

## Fonctionnalités par onglet

### 📚 Leçons
- Multi-classes avec onglets
- Historique des leçons navigationable
- Objectifs pédagogiques (ajout/suppression)
- Contenu/déroulé libre (auto-save)

### 🧑‍🤝‍🧑 Élèves & Présences
- Fiche complète : Prénom, Nom, Sexe, Niveau, **Vitesse de référence (km/h)**, **Notes/infos médicales**
- **Modification en place** via bouton ✏️ (sans supprimer/recréer)
- Import CSV (colonnes : prénom, nom, sexe, niveau, vitesse, notes)
- Présences par leçon : cycle Présent → Absent → Blessé → Présent
- La vitesse de référence s'affiche sur les cartes de présence

### ⚡ Fractionné
- **Calculateur km/h → temps** : instantané, pour toutes les distances usuelles
- Programmes en mode **Fixe** (km/h OU allure M:SS) ou **Évolutif** (par tour)
- Groupes liés à chaque leçon, membres sélectionnés parmi les présents
- Estimation : distance totale, vitesse moyenne, temps travail/récup/total
- Suivi live : chrono, évaluation automatique, **km/h cible affiché**

### ⭐ Évaluation
- Étoiles Échauffement + Charge + Ressenti + Commentaire
- Résumé de classe avec moyennes
- Export CSV complet (inclut vitesse de référence)
- Export PDF via bouton 🖨

---

## Export PDF

L'export PDF utilise la fonction d'impression du navigateur :
1. Cliquer **🖨 Exporter PDF**
2. Dans la boîte de dialogue d'impression → choisir **"Enregistrer en PDF"** comme destination
3. Recommandations : format A4 Portrait, marges Minimum, cocher "Graphiques d'arrière-plan"

Les éléments de navigation et boutons sont masqués à l'impression. Seul le contenu de l'onglet actif s'imprime.

---

## Sauvegarde automatique

- **Temps réel** : chaque clic ou saisie déclenche une sauvegarde dans `localStorage`
- **Périodique** : sauvegarde automatique toutes les 30 secondes
- **Fermeture** : sauvegarde déclenchée avant la fermeture de l'onglet (`beforeunload`)
- **Export JSON** : sauvegarde externe recommandée régulièrement (⬇ Exporter JSON)
- **Import JSON** : restauration depuis un fichier JSON exporté précédemment

---

## Convention de versioning

| Préfixe | Incrémente pour |
|---------|----------------|
| `V` | Nouvelle version du fichier HTML |
| `R` | Nouvelle version du README |

---

## Import CSV — colonnes reconnues

| Colonne | Obligatoire | Exemple |
|---------|-------------|---------|
| `prénom` ou `prenom` | ✅ | Alice |
| `nom` | — | Martin |
| `sexe` | — | F / M |
| `niveau` | — | Intermédiaire |
| `vitesse` | — | 12.5 |
| `notes` | — | Asthme |

Séparateur : virgule `,` ou point-virgule `;` — auto-détecté.

---

## Déploiement GitHub Pages

Placer `AthlEPS_Lecons_V2_index.html` dans le dépôt `louisodilonschneider-web`, renommer en `index.html` dans le dossier cible, et activer GitHub Pages.
