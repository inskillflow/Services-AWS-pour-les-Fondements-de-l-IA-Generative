# Exercice — Renseigner T-P-L-S-F-C-V à partir d’un prompt

## Objectif

Être capable de **paramétrer** un appel IA de bout en bout en complétant les 7 leviers :

* **T** (Temperature) — créativité
* **P** (top-P/K) — vocabulaire retenu
* **L** (Length) — max_tokens
* **S** (Stop) — séquences d’arrêt
* **F** (Format) — structure attendue (JSON/Markdown/…)
* **C** (Context) — sources/extraits autorisés
* **V** (Validation) — règles de vérification (exactitude, format, longueur, incertitudes)

---

## Consigne (Étudiant·e)

1. Lis le **prompt de départ** ci-dessous.
2. Complète le **tableau T-P-L-S-F-C-V** avec des valeurs **concrètes**, **justifiées** en 1 phrase chacune.
3. Donne la **commande finale** (bloc « Paramètres recommandés ») qui pourrait être passée à un modèle.

### Prompt de départ (Texte factuel)

> « Résume l’article ci-dessous en **5 puces** (≤ **120 mots**), et **cite 2 limites** de l’étude.
> Si une information manque, écris *“Incertitude : …”*.
> **Article (extrait autorisé) :** <coller ici un extrait de 2–3 paragraphes>. »

---

## Tableau à compléter (Étudiant·e)

| Élément                | Ta valeur choisie | Justification (1 phrase) |
| ---------------------- | ----------------- | ------------------------ |
| **T – Temperature**    | …                 | …                        |
| **P – top-P / top-K**  | …                 | …                        |
| **L – max_tokens**     | …                 | …                        |
| **S – Stop sequences** | …                 | …                        |
| **F – Format**         | …                 | …                        |
| **C – Context**        | …                 | …                        |
| **V – Validation**     | …                 | …                        |

### Paramètres recommandés (bloc synthèse à produire)

```yaml
temperature: <…>
top_p: <…>   # ou top_k: <…>
max_tokens: <…>
stop: [<…>, <…>]
response_format: <markdown|json>   # si pertinent
context_policy: "Répondre uniquement à partir de l'extrait fourni ; indiquer Incertitude si manquant."
validation_rules:
  - "Longueur ≤ 120 mots"
  - "5 puces + 2 limites"
  - "Aucune info hors extrait"
  - "Signaler toute incertitude"
```

---

## Barème (10 points)

* T (Temperature) correctement réglé et justifié — **2 pts**
* P (top-P/K) cohérent avec T et la tâche — **2 pts**
* L (max_tokens) compatible avec la longueur cible — **1 pt**
* S (Stop) pertinent (ou “non nécessaire” justifié) — **1 pt**
* F (Format) explicite et vérifiable — **1 pt**
* C (Context) clair + règle “ne répondre que depuis l’extrait” — **2 pts**
* V (Validation) avec **au moins 3 contrôles** mesurables — **1 pt**

> **Tolérance** : d’autres valeurs sont acceptées si **cohérentes et justifiées**.

---

## Pièges fréquents (à éviter)

* **T élevée** pour une tâche factuelle → risque de dérives/stylistiques.
* **max_tokens trop bas** → sortie tronquée ; trop haut → verbosité.
* **Stop sequences** absentes alors qu’un formalisme strict est demandé (JSON, balises).
* **Format** non testable (pas de structure imposée).
* **Contexte** flou (le modèle invente) ; oublier d’exiger *“Incertitude”* si manque.
* **Validation** non mesurable (ex. “sois clair” au lieu de critères concrets).

---

## Variante 2 (Code)

**Prompt**

> « Écris une fonction **Python** `clean_names(df)` qui normalise les colonnes *first_name* et *last_name* (trim, minuscule, accents supprimés). Ajoute **docstring** et **tests unitaires** simples (pytest). »

**Attendus**

* **T basse** (exactitude), format Markdown ou blocs de code, **tests inclus**, validation : *exécutable* et *cas limites min.*.

---

## Variante 3 (Image)

**Prompt**

> « Portrait photo-réaliste d’un hibou des neiges en **gros plan**, arrière-plan **bokeh froid**, **1536×1536**, **2 variantes**, sans texte ni watermark. »

**Attendus**

* JSON image (subject, pose_action, environment, background, lighting, composition, color_tone, width/height, negatives, variants), **T inutile ici** (dépend du moteur), **Validation** : taille exacte, netteté yeux, pas d’artefacts/texte.

---

## Corrigé modèle — **Texte factuel** (à usage enseignant)

> Exemple de bonne réponse (une des solutions possibles).

### Tableau rempli (exemple)

| Élément | Valeur                                                                                           | Justification                                                           |
| ------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **T**   | 0.2                                                                                              | Ton factuel/contraint (5 puces ≤120 mots, pas de créativité souhaitée). |
| **P**   | top_p=0.85                                                                                       | Maintient une sortie fluide sans divaguer ; cohérent avec T basse.      |
| **L**   | 200                                                                                              | Budget suffisant pour 5 puces + 2 limites tout en restant concis.       |
| **S**   | ["### FIN"]                                                                                      | Coupe nette si on demande au modèle d’achever par “### FIN”.            |
| **F**   | Markdown : 5 puces + “Limites : …”                                                               | Format vérifiable rapidement à l’œil.                                   |
| **C**   | “Réponds uniquement à partir de l’extrait fourni.”                                               | Évite les hallucinations ; impose la mention *Incertitude*.             |
| **V**   | 1) ≤120 mots ; 2) 5 puces + 2 limites ; 3) aucune info hors extrait ; 4) “Incertitude” si manque | Contrôles objectifs et mesurables.                                      |

### Paramètres recommandés (exemple)

```yaml
temperature: 0.2
top_p: 0.85
max_tokens: 200
stop: ["### FIN"]
response_format: "markdown"
context_policy: "Répondre uniquement à partir de l'extrait fourni ; indiquer 'Incertitude : …' si l'information manque."
validation_rules:
  - "Longueur totale ≤ 120 mots"
  - "Exactement 5 puces + 2 limites"
  - "Aucune information hors extrait"
  - "Mention Incertitude si nécessaire"
```

### Prompt “opérationnel” (exemple à coller)

```
Rôle : Tu es un rédacteur factuel et concis.
Contexte (extrait autorisé uniquement) :
<EXTRAIT ICI>
Tâche : Résume en 5 puces (≤120 mots) et cite 2 limites de l’étude.
Format : Markdown (5 puces), puis ligne “Limites : …”.
Contraintes : Aucune information hors extrait ; si une information manque, écris “Incertitude : …”.
Paramètres recommandés : temperature 0.2 ; top_p 0.85 ; max_tokens 200 ; stop ["### FIN"].
Valide avant d’envoyer : longueur ≤120 mots ; 5 puces + 2 limites ; aucune info hors extrait ; incertitudes signalées.
### FIN
```

---

## Extension (facultative) — Grille d’auto-évaluation étudiant·e

* [ ] J’ai choisi **T** et **P** en cohérence avec le type de tâche (factuel vs créatif).
* [ ] **L** couvre la longueur demandée sans verbosité.
* [ ] **S** est défini si le format exige une coupure nette.
* [ ] **F** impose une **structure testable** (Markdown/JSON).
* [ ] **C** interdit d’aller au-delà de l’extrait (*no hallucinations*).
* [ ] **V** contient **≥3 règles mesurables** (longueur, compte des puces, sources, incertitudes).

