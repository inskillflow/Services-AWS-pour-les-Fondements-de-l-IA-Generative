# PLAN DE FORMATION — INTELLIGENCE ARTIFICIELLE GÉNÉRATIVE ET SYSTÈMES AGENTIQUES

*Fichier : `00-plan-formation.md`*



## Objectif global

Cette formation vise à initier les étudiants à l’intelligence artificielle générative et à la mise en œuvre d’applications concrètes exploitant des modèles de fondation (Foundation Models) et des agents intelligents (Agentic AI).
Les apprenants apprendront à comprendre, manipuler et intégrer ces modèles via différents services : AWS Bedrock, Hugging Face, OpenAI, Lovable, PartyRock, Google Gemini et Stability AI.

Chaque module comprend :

* un **cours structuré** en Markdown (`XX-introduction-...md`)
* une **pratique guidée** (`XX-pratique-...md`)
* une **activité dirigée** avec espaces de réponses
* une **évaluation courte** (analyse, question ou mini-projet)



## MODULE 1 — Introduction à l’IA, au Machine Learning et à l’IA Générative

| Type         | Fichier                                 | Description                                                                           |
| ------------ | --------------------------------------- | ------------------------------------------------------------------------------------- |
| **Cours**    | `01-introduction-ia-ml-gen.md`          | Définitions fondamentales : IA, apprentissage supervisé, non supervisé, et génératif. |
| **Pratique** | `02-pratique-introduction-ia-ml-gen.md` | Manipulation des paramètres de génération (température, top-p, max_tokens).           |

### Définitions essentielles

* **Intelligence Artificielle (IA)** : discipline visant à reproduire certaines capacités humaines (raisonnement, langage, vision, décision) par des algorithmes.
* **Machine Learning (ML)** : sous-domaine de l’IA permettant aux systèmes d’apprendre à partir de données.
* **IA Générative (Generative AI)** : approche consistant à créer du contenu nouveau (texte, image, audio, code) à partir de modèles probabilistes entraînés sur de grandes masses de données.

**Objectif du module :**
Savoir distinguer IA traditionnelle, apprentissage machine et modèles génératifs ; expérimenter la génération textuelle et visuelle.


## MODULE 2 — Les Foundation Models et les écosystèmes d’IA

| Type         | Fichier                            | Description                                                                     |
| ------------ | ---------------------------------- | ------------------------------------------------------------------------------- |
| **Cours**    | `03-foundation-models.md`          | Comprendre la notion de modèle de fondation et les grandes familles de modèles. |
| **Pratique** | `04-pratique-foundation-models.md` | Comparer plusieurs modèles (Claude, GPT, Gemini, Titan, Mistral).               |

### Définitions essentielles

* **Foundation Model (Modèle de fondation)** : modèle de très grande taille préentraîné sur des corpus massifs, capable d’être adapté à de nombreuses tâches (ex. GPT, Claude, LLaMA).
* **Fine-tuning** : réentraînement partiel d’un modèle pour le spécialiser à un domaine précis.
* **Zero-shot / Few-shot Learning** : capacité d’un modèle à résoudre des tâches sans ou avec très peu d’exemples.

**Objectif du module :**
Identifier les modèles adaptés à un cas d’usage et comprendre les différences de performance entre fournisseurs.



## MODULE 3 — Le Prompt Engineering et la maîtrise des sorties

| Type         | Fichier                             | Description                                                                 |
| ------------ | ----------------------------------- | --------------------------------------------------------------------------- |
| **Cours**    | `05-prompt-engineering.md`          | Apprentissage des techniques pour concevoir un prompt efficace et contrôlé. |
| **Pratique** | `06-pratique-prompt-engineering.md` | Structuration d’un prompt, organisation, ton, style et contraintes.         |

### Définitions essentielles

* **Prompt** : instruction donnée à un modèle d’IA pour générer une réponse.
* **Prompt Engineering** : art de concevoir, structurer et optimiser les requêtes pour obtenir des réponses cohérentes, précises et sûres.
* **Adverse Prompt** : prompt malveillant ou ambigu provoquant une sortie non souhaitée (fuite d’information, biais).

**Objectif du module :**
Apprendre à concevoir des prompts complexes (texte et image), à introduire du contexte et à guider la réponse.



## MODULE 4 — Paramètres d’inférence et personnalisation des modèles

| Type         | Fichier                               | Description                                                                |
| ------------ | ------------------------------------- | -------------------------------------------------------------------------- |
| **Cours**    | `07-inference-parameters.md`          | Étude des paramètres contrôlant la créativité et la cohérence d’un modèle. |
| **Pratique** | `08-pratique-inference-parameters.md` | Expérimenter les paramètres : température, top-k, top-p, répétition.       |

### Définitions essentielles

* **Température** : contrôle du niveau d’aléatoire dans la génération (valeurs élevées = réponses plus créatives).
* **Top-k / Top-p Sampling** : stratégies de sélection probabiliste des mots suivants.
* **Inference** : phase d’utilisation d’un modèle entraîné pour générer de nouveaux résultats.

**Objectif du module :**
Observer et interpréter les variations de style, de ton et de cohérence selon les réglages.



## MODULE 5 — IA Responsable et Sécurisée

| Type         | Fichier                         | Description                                                |
| ------------ | ------------------------------- | ---------------------------------------------------------- |
| **Cours**    | `09-responsible-ai.md`          | Principes éthiques et réglementaires de l’IA générative.   |
| **Pratique** | `10-pratique-responsible-ai.md` | Analyse d’un cas de biais et mise en place d’un garde-fou. |

### Définitions essentielles

* **IA Responsable** : approche garantissant transparence, équité, et non-discrimination.
* **Bias (Biais)** : tendance systématique à favoriser un résultat erroné ou inéquitable.
* **Guardrails** : mécanismes de contrôle pour filtrer les réponses inappropriées ou dangereuses.

**Objectif du module :**
Identifier les biais, appliquer les principes éthiques, et déployer un contrôle des contenus générés.



## MODULE 6 — Sécurité, Gouvernance et Conformité

| Type         | Fichier                              | Description                                                                |
| ------------ | ------------------------------------ | -------------------------------------------------------------------------- |
| **Cours**    | `11-security-governance.md`          | Gestion des identités, audit, confidentialité et conformité réglementaire. |
| **Pratique** | `12-pratique-security-governance.md` | Sécuriser les clés API et auditer les appels à un modèle.                  |

### Définitions essentielles

* **Governance** : processus assurant la supervision, le contrôle et la traçabilité des usages IA.
* **Compliance** : conformité avec les normes et lois (RGPD, ISO 27001, NIST).
* **IAM (Identity and Access Management)** : gestion des permissions pour contrôler l’accès aux services IA.

**Objectif du module :**
Mettre en place un environnement sécurisé et conforme pour l’utilisation de modèles IA.



## MODULE 7 — Les Agents et l’Agentic AI

| Type         | Fichier                     | Description                                                 |
| ------------ | --------------------------- | ----------------------------------------------------------- |
| **Cours**    | `13-agentic-ai.md`          | Comprendre les systèmes agentiques et leurs composants.     |
| **Pratique** | `14-pratique-agentic-ai.md` | Construire un agent capable d’agir, raisonner et planifier. |

### Définitions essentielles

* **Agent** : système autonome capable de percevoir son environnement, raisonner et agir pour atteindre un objectif.
* **Agentic AI** : forme d’intelligence artificielle où les modèles (LLMs) sont intégrés dans un cadre décisionnel leur permettant de **planifier, exécuter des actions et interagir** avec d’autres services.
* **LangChain / CrewAI** : frameworks facilitant la construction d’agents conversationnels et d’agents exécutifs connectés à des API, bases de données ou fichiers.

**Objectif du module :**
Créer un agent capable de planifier une tâche, d’utiliser une API et d’interagir avec d’autres agents ou documents.



## MODULE 8 — Mise en œuvre d’applications IA génératives

| Type         | Fichier                         | Description                                                                      |
| ------------ | ------------------------------- | -------------------------------------------------------------------------------- |
| **Cours**    | `15-implementing-genai-apps.md` | Cycle complet de développement d’une application IA.                             |
| **Pratique** | `16-pratique-genai-apps.md`     | Construction d’une application IA générative réelle (texte + image + interface). |

**Objectif du module :**
Assembler les briques étudiées pour créer une application complète :

* un frontend interactif (Lovable, Streamlit ou PartyRock)
* une logique IA (API Bedrock, Hugging Face ou OpenAI)
* un mécanisme de contrôle (Guardrails, logs).



## MODULE 9 — Projet intégrateur et évaluation finale

| Type         | Fichier                       | Description                                                      |
| ------------ | ----------------------------- | ---------------------------------------------------------------- |
| **Cours**    | `17-projet-final.md`          | Présentation du projet intégrateur et des critères d’évaluation. |
| **Pratique** | `18-projet-final-pratique.md` | Réalisation d’un projet complet IA générative + agentique.       |

**Exemples de projets**

* Générateur de fiches de cours et d’illustrations.
* Assistant juridique IA avec filtrage éthique.
* Agent personnel de résumé automatique et recherche contextuelle.






## Écosystèmes et technologies couverts

| Domaine             | Services et outils                                   |
| ------------------- | ---------------------------------------------------- |
| Génération de texte | OpenAI GPT, Claude, Gemini, Mistral, Bedrock Titan   |
| Génération d’image  | Stability AI, Leonardo AI, DALL-E, Bedrock Image API |
| Prompting & UX      | PartyRock, Lovable, Hugging Face Spaces              |
| Agents intelligents | LangChain, CrewAI, Bedrock Agents                    |
| Sécurité & audit    | Bedrock Guardrails, Audit Manager, IAM               |
| Déploiement         | Streamlit, FastAPI, GitHub, AWS Cloud9               |

