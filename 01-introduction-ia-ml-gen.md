# Introduction — IA, ML et IA générative

*Fichier : `01-introduction.md`*

## Plan de matière

1. [But du module](#1-but-du-module)
2. [Notions essentielles : IA, ML, IA générative](#2-notions-essentielles--ia-ml-ia-générative)
3. [Cycle de vie d’un système d’IA générative](#3-cycle-de-vie-dun-système-dia-générative)
4. [Entrées et sorties : données, consignes, formats](#4-entrées-et-sorties--données-consignes-formats)
5. [Paramètres de génération : effets clés](#5-paramètres-de-génération--effets-clés)
6. [Qualité et vérifications](#6-qualité-et-vérifications)
7. [Limites, risques et mesures](#7-limites-risques-et-mesures)
8. [Exemples concrets (texte, code, résumé, Q&A)](#8-exemples-concrets-texte-code-résumé-qa)
9. [Exercices et livrables rapides](#9-exercices-et-livrables-rapides)
10. [Résumé & check-list](#10-résumé--check-list)

---

## 1) But du module

* Situer clairement **IA**, **apprentissage automatique (ML)** et **IA générative**.
* Comprendre le **flux général** : *problème → données → modèle → génération → contrôle → amélioration*.
* Savoir configurer les **entrées** (contexte, consignes, contraintes) et analyser les **sorties** (structure, fidélité, utilité).

**Résultat attendu :** décrire et cadrer un usage d’IA générative de bout en bout.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 2) Notions essentielles : IA, ML, IA générative

### 2.1 Définitions courtes

* **IA** : techniques permettant à une machine d’accomplir des tâches qui paraissent “intelligentes”.
* **ML** : sous-domaine de l’IA où un modèle **apprend des données** pour **prédire** (classe, valeur, groupe).
* **IA générative (GenAI)** : modèles capables de **produire** du contenu (texte, image, audio, code) à partir d’**instructions** et d’un **contexte**.

### 2.2 Différences clés

* **ML** “classique” : focalisé sur la **prédiction**.
* **GenAI** : focalisée sur la **génération** guidée par des consignes et des paramètres.

### 2.3 Vocabulaire minimal

* **Token** : petite unité de texte traitée par le modèle.
* **Fenêtre de contexte** : quantité maximale d’informations “vues” en une fois.
* **Hallucination** : sortie plausible mais **incorrecte**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 3) Cycle de vie d’un système d’IA générative

1. **Définir le besoin** : objectif, public, contraintes, format attendu.
2. **Sélectionner les données** : sources autorisées, nettoyage, anonymisation si nécessaire.
3. **Orchestrer** :

   * rédiger les **consignes** (rôle, tâche, format),
   * ajouter le **contexte** (extraits, références),
   * régler les **paramètres** (température, top-p, longueur).
4. **Générer** : appeler le modèle et récupérer la sortie.
5. **Contrôler** : vérifications automatiques et humaines (structure, exactitude, sécurité).
6. **Tracer** : conserver exemples, versions de consigne, paramètres.
7. **Améliorer** : itérer sur consignes, contexte, paramètres ou données.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 4) Entrées et sorties : données, consignes, formats

### 4.1 Entrées (à soigner)

* **Rôle** : “Tu es…”.
* **Contexte** : faits, définitions, extraits.
* **Tâche** + **critères** : ce qui doit être produit, niveau d’exactitude, concision.
* **Format** : puces, tableau, JSON, gabarit.
* **Contraintes** : longueur, ton, langue, références.

### 4.2 Sorties (à exiger)

* **Structure claire** (titres, sections, listes).
* **Références** ou mention d’**incertitude** si besoin.
* **Format respecté** ; sinon, **réviser l’entrée**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 5) Paramètres de génération : effets clés

* **Température** : contrôle la **diversité**.

  * Basse (≈ 0–0.3) → plus déterministe, utile pour du **factuel** et du **format strict**.
  * Haute (≈ 0.7–1.0+) → plus variée, adaptée au **créatif**.
* **Top-p / Top-k** : restreignent les choix du prochain token.
* **Max tokens** (sortie) : **borne** la longueur de la réponse.
* **Stop sequences** : séquences qui **arrêtent** la génération.

**Règle simple :**

* Besoin **précis/factuel** → température **basse**, format **strict**.
* Besoin **créatif/exploratoire** → température **plus haute**, contraintes **souples**.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 6) Qualité et vérifications

### 6.1 Critères

* **Pertinence** par rapport à la demande.
* **Fidélité** aux sources/contexte.
* **Clarté** et **structure**.
* **Concision** et respect des contraintes.
* **Traçabilité** (références, incertitudes).

### 6.2 Vérifications

* **Automatiques** : schéma JSON, longueur, mots à exclure.
* **Humaines** : relecture, contrôle factuel sur source fiable.
* **Échantillonnage** : tester plusieurs cas typiques.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 7) Limites, risques et mesures

* **Hallucinations** → ajouter du **contexte**, exiger références, baisser la température.
* **Biais / stéréotypes** → tester des cas variés, expliciter les limites.
* **Confidentialité** → retirer/masquer les données sensibles ; limiter la journalisation.
* **Dépendance au modèle** → conserver consignes et jeux d’essai, documenter les versions.
* **Coût / latence** → réduire taille de contexte et longueur de sortie, réutiliser les résultats stables.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 8) Exemples concrets (texte, code, résumé, Q&A)

### 8.1 Variations d’exercice

* **Entrée** : énoncé, niveau visé, contraintes (sans solution, durée ≤ 10 min).
* **Sortie** : 3 variantes (facile / moyen / difficile) en liste numérotée.

### 8.2 Résumé court

* **Entrée** : passage long + consigne “5 puces, ≤ 120 mots, citer 2 limites”.
* **Sortie** : 5 puces + 2 limites, sans opinion gratuite.

### 8.3 Q&A cadré

* **Entrée** : question + **extrait** de référence.
* **Sortie** : réponse en 3–5 phrases + mention “*Réponse basée sur l’extrait fourni*”.

### 8.4 Gabarit d’instruction universel

```
Rôle : Tu es un rédacteur clair et exact.
Contexte : <résumé / extraits autorisés>
Tâche : Produis <type de rendu> couvrant <points indispensables>.
Format : <puces | tableau | JSON (schéma ci-dessous)>
Contraintes : longueur max, ton, langue, références si incertitude.
Exemples : <optionnel : 1–2 mini-démos>
Paramètres recommandés : température 0.2–0.4 pour factuel ; 0.7 pour créatif.
```

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 9) Exercices et livrables rapides

* **Cas d’usage (5 lignes)** : objectif, entrées, sorties, contraintes, contrôle.
* **Consigne stricte → sortie JSON** : clés obligatoires + un **exemple valide**.
* **Paramètres** : même demande avec température **0.2** puis **0.9** ; décrire l’écart en 3 lignes.

**Livrable suggéré :** `prompts/01-intro.json` avec :

* l’instruction finale,
* **3 entrées d’essai**,
* les **paramètres** recommandés.

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

---

## 10) Résumé & check-list

### 10.1 À retenir

* **Contexte + Consignes + Format + Paramètres = Qualité**.
* Toujours imposer un **format vérifiable** (JSON / structure).
* **Documenter** consignes, versions et jeux d’essai.

### 10.2 Check-list avant exécution

* [ ] Objectif clair, public, contraintes
* [ ] Contexte fiable et suffisant
* [ ] Consigne structurée (rôle, tâche, format, contraintes)
* [ ] Paramètres adaptés (température / longueur)
* [ ] Vérification prévue (auto + humaine)
* [ ] Journalisation des exemples et résultats

**Navigation** — ↩︎ [Revenir au plan](#plan-de-matière)

