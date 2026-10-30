# CAHIER DES CHARGES TECHNIQUE ET FONCTIONNEL
# Agent IA de Copy Trading Automatisé — Deriv MT5

**Version :** 1.0  
**Statut :** Spécification initiale  
**Type de projet :** Plateforme de copy trading automatisé assistée par intelligence artificielle  
**Plateforme cible :** Deriv MT5  
**Capital initial envisagé :** 50 à 200 €  
**Mode de fonctionnement :** Automatisation continue, avec validation préalable des accès et mécanismes de copie  
**Priorité :** Préservation du capital, fiabilité des données, contrôle du risque et décisions explicables

---

# 1. Présentation générale

## 1.1. Contexte

Le projet consiste à développer un agent intelligent capable d'identifier des traders performants accessibles sur les plateformes compatibles avec Deriv MT5, d'analyser leurs performances, de classer leurs stratégies et de superviser la copie automatique de leurs transactions.

Le système devra utiliser des techniques d'analyse quantitative, de machine learning et d'intelligence artificielle pour améliorer la sélection des traders et détecter les situations dans lesquelles la copie devient trop risquée.

L'agent ne devra pas se limiter à sélectionner les traders affichant le rendement le plus élevé. Il devra examiner la régularité des résultats, les pertes maximales, la stabilité de la stratégie, l'exposition, les coûts et la qualité des données disponibles.

L'IA ne devra jamais être considérée comme une garantie de rentabilité.

## 1.2. Vision du produit

Créer une plateforme de copy trading capable de fonctionner avec une intervention humaine minimale, tout en conservant des mécanismes de sécurité stricts.

Le système devra notamment :

- découvrir les fournisseurs de signaux accessibles ;
- collecter et vérifier leurs statistiques ;
- identifier les stratégies présentant un rapport rendement/risque intéressant ;
- calculer un score de qualité et de fiabilité ;
- surveiller continuellement les performances des traders sélectionnés ;
- utiliser l'IA pour détecter les risques et autoriser, limiter ou suspendre la copie ;
- s'appuyer sur un mécanisme de copie officiellement pris en charge ;
- surveiller les opérations et le compte destinataire ;
- arrêter la copie en cas de risque excessif ;
- conserver un historique complet et auditable des décisions.

## 1.3. Objectifs mesurables

Les objectifs de qualité du logiciel seront les suivants :

1. Aucune transaction ne doit être exécutée par le système sans passer par les contrôles de sécurité définis.
2. Aucune décision de l'IA ne doit pouvoir désactiver les protections obligatoires.
3. Toute décision automatisée doit être associée à une justification enregistrée.
4. Le système doit détecter les déconnexions, les données périmées et les erreurs d'exécution.
5. Le classement des traders doit reposer exclusivement sur des données disponibles, datées et vérifiables.
6. Les performances doivent être mesurées après frais et coûts de trading, dans la mesure où les données le permettent.
7. Le système doit pouvoir fonctionner en mode simulation sans exposer de capital réel.
8. L'activation du trading réel doit nécessiter une autorisation explicite de l'utilisateur.

Les objectifs de performance financière ne constituent pas des critères garantis de réussite du logiciel.

---

# 2. Périmètre fonctionnel

## 2.1. Fonctionnalités incluses

- Gestion de la configuration Deriv MT5.
- Découverte des fournisseurs de signaux accessibles.
- Collecte et normalisation des statistiques.
- Classement multicritère des traders.
- Détection des risques et des comportements suspects.
- Module IA de seconde opinion et de veto.
- Supervision du copy trading natif.
- Gestion du capital, des limites de perte et de la marge.
- Dashboard web responsive.
- Notifications Telegram.
- Historique des décisions et journal d'audit.
- Backtesting et simulation.
- Mode démo.
- Mode réel contrôlé.
- Surveillance de la santé du système.
- Tests automatiques et procédures de reprise après incident.

## 2.2. Fonctionnalités exclues de la première version

- Garantie de rentabilité.
- Accès non autorisé aux comptes ou aux positions privées des traders.
- Contournement des restrictions de Deriv, MT5 ou MQL5.
- Extraction de données par des méthodes contraires aux conditions d'utilisation.
- Exécution autonome d'ordres en dehors des mécanismes autorisés.
- Modification arbitraire des stops ou des positions du fournisseur.
- Création de signaux de trading indépendants présentés comme des trades copiés.
- Augmentation automatique du capital ou des risques après une série gagnante.
- Gestion de fonds appartenant à des tiers.
- Envoi d'ordres de trading par un LLM sans contrôles déterministes.

---

# 3. Contraintes spécifiques à Deriv MT5

## 3.1. Principe d'intégration

L'application devra distinguer trois systèmes :

1. Le moteur d'analyse et de sélection développé dans le projet.
2. Le mécanisme de copy trading effectivement disponible pour le compte.
3. Le terminal et le compte Deriv MT5 destinataire.

L'API de trading Deriv ne doit pas être considérée comme un accès universel aux positions de tous les traders MT5.

Le système devra vérifier les possibilités réellement disponibles au moment de l'intégration : types de compte compatibles, fournisseurs accessibles, instruments, restrictions, coûts, autorisations et méthodes de souscription.

## 3.2. Connecteurs envisagés

### Connecteur A — MQL5 Signals

Le système devra exploiter les statistiques publiquement accessibles et superviser, dans la mesure permise, le mécanisme de copie proposé par le terminal MetaTrader 5.

La souscription, le choix du fournisseur et les réglages de copie devront respecter les fonctionnalités natives du service.

### Connecteur B — Deriv Nakala

Le système devra vérifier l'éligibilité du compte, les marchés supportés, les fournisseurs accessibles et les fonctions de configuration disponibles.

Si aucune API publique documentée ne permet de sélectionner automatiquement un fournisseur, cette opération restera manuelle ou passera par une interface d'intégration officiellement autorisée.

### Connecteur C — Terminal MT5

Un composant local pourra servir à la surveillance technique du terminal et du compte, uniquement par des interfaces autorisées.

Un Expert Advisor MQL5 pourra éventuellement être développé pour les contrôles compatibles avec le terminal, sans remplacer le mécanisme natif de copie ni tenter de répliquer des positions privées inaccessibles.

## 3.3. Règle impérative

Aucun module ne devra prétendre assurer la copie automatique complète avant qu'un test réel en environnement démo ait validé le parcours de bout en bout.

Si la sélection automatique d'un fournisseur n'est pas prise en charge, l'agent devra l'indiquer clairement et demander une activation manuelle.

---

# 4. Profils et permissions

## 4.1. Administrateur — propriétaire du compte

L'administrateur pourra :

- configurer les connexions ;
- consulter le classement des traders ;
- définir le capital de référence ;
- choisir les marchés autorisés ;
- définir les limites de risque ;
- activer le mode démo ;
- autoriser le passage au mode réel ;
- suspendre toutes les copies ;
- consulter les journaux ;
- gérer les notifications ;
- exporter les rapports ;
- modifier les paramètres IA autorisés.

## 4.2. Agent IA

L'agent IA pourra :

- analyser les données accessibles ;
- classer les fournisseurs ;
- détecter les anomalies ;
- produire des évaluations ;
- recommander une suspension ;
- opposer un veto à une copie ;
- demander une réévaluation ;
- expliquer ses décisions.

Il ne pourra pas :

- désactiver les protections obligatoires ;
- modifier les limites maximales de risque ;
- inventer des statistiques ;
- inventer des transactions sources ;
- contourner une restriction de plateforme ;
- réactiver le trading réel après un arrêt d'urgence sans autorisation ;
- augmenter automatiquement les risques pour récupérer des pertes.

## 4.3. Permissions et secrets

Les identifiants et secrets devront être stockés dans un gestionnaire de secrets ou un mécanisme de stockage sécurisé.

Les mots de passe, clés, jetons et données d'authentification ne devront jamais apparaître dans les journaux, les prompts IA ou les captures d'écran.

---

# 5. Module de découverte et de classement des traders

## 5.1. Sources de données

Le collecteur devra rechercher les fournisseurs dans les catalogues et services accessibles légalement.

Pour chaque fournisseur, le système devra enregistrer, lorsque ces informations sont disponibles :

- identifiant de la source ;
- nom public ;
- plateforme ;
- instruments tradés ;
- date de création ou ancienneté ;
- capital ou dépôt déclaré ;
- rendement historique ;
- drawdown ;
- facteur de profit ;
- nombre de transactions ;
- fréquence des opérations ;
- historique des performances ;
- frais de souscription ;
- compatibilité avec le compte destinataire ;
- date de dernière actualisation ;
- provenance des données ;
- niveau de confiance accordé aux données.

Les données manquantes devront être explicitement marquées comme inconnues.

## 5.2. Fréquence de mise à jour

- Statistiques générales : toutes les 6 à 24 heures, selon les limites de la source.
- Vérification des fournisseurs retenus : plusieurs fois par jour si les interfaces le permettent.
- Santé du terminal et du mécanisme de copie : surveillance continue.
- Alertes de risque : déclenchement dès que les informations nécessaires sont disponibles.
- Recalcul du classement : au moins une fois par jour, avec recalcul anticipé en cas de changement significatif.

La fréquence réelle devra respecter les quotas et les possibilités des interfaces utilisées.

## 5.3. Filtres d'éligibilité

Un fournisseur ne pourra être considéré comme éligible que si :

- ses statistiques sont suffisamment complètes ;
- son historique est assez long ;
- ses performances peuvent être évaluées ;
- son niveau de risque respecte les seuils configurés ;
- ses frais sont compatibles avec le capital ;
- son mécanisme de copie est disponible ;
- les instruments et volumes sont compatibles ;
- aucune anomalie majeure n'est détectée.

Les seuils devront être configurables et testables.

Valeurs initiales proposées :

- Historique minimal : 26 semaines.
- Nombre minimal de transactions : 100, lorsque les données sont disponibles.
- Drawdown maximal historique : 15 %.
- Données suffisamment récentes : moins de 24 heures pour les métriques générales lorsque la source le permet.
- Score minimal d'éligibilité : 70/100.

Ces valeurs constituent des paramètres initiaux à tester, et non des preuves qu'un trader est sûr ou rentable.

---

# 6. Système de scoring

## 6.1. Score global

Chaque fournisseur recevra un score de 0 à 100.

Pondération initiale proposée :

| Critère | Pondération |
|---|---:|
| Maîtrise du drawdown | 25 % |
| Régularité des performances | 20 % |
| Rentabilité nette et facteur de profit | 15 % |
| Ancienneté de l'historique | 15 % |
| Exposition et utilisation de la marge | 10 % |
| Qualité de l'échantillon de transactions | 10 % |
| Coûts de souscription | 5 % |

Le score devra être calculé à partir de sous-scores documentés, normalisés et reproductibles.

Il ne devra pas être calculé uniquement par un LLM.

## 6.2. Indicateurs financiers

Le système devra, selon les données disponibles, calculer :

- rendement total ;
- rendement annualisé, si la période est suffisante ;
- volatilité des rendements ;
- drawdown maximal ;
- durée des phases de récupération ;
- facteur de profit ;
- taux de réussite ;
- gain moyen par trade ;
- perte moyenne par trade ;
- ratio gain/perte ;
- espérance mathématique par transaction ;
- fréquence des transactions ;
- frais et coûts connus ;
- stabilité du rendement selon plusieurs fenêtres temporelles.

Les métriques devront être accompagnées de leur définition et de leur période de calcul.

## 6.3. Détection des stratégies risquées

Le système devra rechercher les signes de :

- martingale ;
- augmentation des lots après une perte ;
- accumulation de positions perdantes ;
- grid trading à exposition croissante ;
- absence de stop-loss, lorsque l'information est accessible ;
- forte concentration sur un instrument ;
- utilisation excessive de la marge ;
- dépendance à quelques transactions exceptionnelles ;
- performances irrégulières ;
- changements soudains de comportement ;
- historiques incomplets ou incohérents.

Une absence de données ne devra pas être interprétée comme une preuve d'absence de risque.

## 6.4. Classement final

Le dashboard devra distinguer :

- **Éligible :** satisfait les critères obligatoires.
- **À surveiller :** nécessite une analyse supplémentaire.
- **Suspendu :** ne peut plus être copié dans l'état actuel.
- **Non évaluable :** données insuffisantes.
- **Incompatible :** le compte ou le mécanisme de copie ne permet pas son utilisation.

Le fournisseur ayant le meilleur score ne sera pas automatiquement activé. Il devra également satisfaire les contraintes de compatibilité, de risque et de disponibilité.

---

# 7. Module d'intelligence artificielle

## 7.1. Objectif

L'IA devra améliorer la qualité des décisions en ajoutant une couche d'analyse contextuelle, de détection des anomalies et de contrôle critique.

Elle ne devra pas être utilisée comme une boîte noire qui prend directement le contrôle du compte.

Le principe retenu est :

**Les moteurs déterministes autorisent les actions possibles. L'IA peut les refuser ou demander une réévaluation, mais ne peut jamais contourner les règles de sécurité.**

## 7.2. Architecture IA hybride

### Couche 1 — Calcul quantitatif

Un moteur statistique déterministe calculera les indicateurs financiers, le score, les limites de risque et les conditions d'éligibilité.

Technologies possibles :

- Python ;
- pandas ;
- NumPy ;
- scikit-learn ;
- bibliothèques statistiques spécialisées.

### Couche 2 — Détection d'anomalies

Un module d'analyse recherchera :

- les variations anormales du rendement ;
- les changements de fréquence des trades ;
- les augmentations inhabituelles de l'exposition ;
- les changements de comportement ;
- les dégradations du ratio rendement/risque ;
- les données manquantes ou incohérentes.

Les méthodes pourront inclure des seuils statistiques, des modèles robustes et des méthodes de détection d'anomalies.

### Couche 3 — Évaluation IA

Un modèle de langage ou un modèle spécialisé pourra synthétiser les informations structurées et répondre à des questions précises :

- La stratégie est-elle devenue plus risquée ?
- Les performances récentes sont-elles cohérentes avec l'historique ?
- Les pertes proviennent-elles d'une dégradation persistante ?
- Les données disponibles suffisent-elles pour maintenir l'éligibilité ?
- Faut-il suspendre la copie et demander une réévaluation ?
- Quelles informations manquent pour prendre une décision fiable ?

Les réponses devront être limitées aux données réellement fournies au modèle.

### Couche 4 — Moteur de décision

Un moteur déterministe appliquera les résultats selon des règles définies :

1. Vérifier les limites de sécurité.
2. Vérifier la disponibilité du mécanisme de copie.
3. Vérifier les données et leur fraîcheur.
4. Vérifier le score et l'éligibilité.
5. Consulter l'analyse IA.
6. Appliquer le veto IA si nécessaire.
7. Exécuter uniquement si toutes les conditions obligatoires sont satisfaites.
8. Enregistrer la décision.

## 7.3. Décisions autorisées à l'IA

L'IA pourra renvoyer exclusivement des décisions structurées telles que :

- `ALLOW` : aucune objection supplémentaire, sous réserve des règles déterministes.
- `VETO` : bloquer la nouvelle copie.
- `REVIEW` : demander une réévaluation des données.
- `INSUFFICIENT_DATA` : refuser toute conclusion en l'absence d'informations suffisantes.

Une réponse inconnue, invalide ou non conforme au schéma attendu devra être traitée comme un refus.

## 7.4. Prompt système de l'IA

Le prompt devra imposer les règles suivantes :

> Tu es un module d'analyse des risques pour un système de copy trading.
>
> Tu n'es pas un trader autonome et tu ne dois pas créer de signaux de trading.
>
> Tu analyses exclusivement les données structurées qui te sont fournies.
>
> Tu dois rechercher les risques, les incohérences, les dégradations de performance et les informations manquantes.
>
> Tu peux autoriser la poursuite de l'évaluation, opposer un veto ou demander une révision.
>
> Tu ne peux jamais désactiver une limite de risque, augmenter le levier, inventer des données ou contourner une restriction de plateforme.
>
> Toute donnée absente doit être considérée comme inconnue.
>
> Si les informations sont insuffisantes ou contradictoires, tu dois refuser de conclure.
>
> Tu dois fournir une justification concise, les indicateurs concernés et un niveau de confiance correctement calibré.
>
> Tu ne dois jamais présenter une prévision de profit comme une certitude.
>
> La décision finale d'exécution appartient au moteur déterministe de sécurité.

## 7.5. Réduction des hallucinations

Le système devra :

- transmettre au modèle uniquement des données structurées ;
- identifier la date de chaque donnée ;
- vérifier les unités et les périodes ;
- interdire l'invention de chiffres ;
- valider chaque réponse contre un schéma JSON ;
- limiter la longueur des justifications ;
- enregistrer le modèle et sa version ;
- conserver la réponse brute et la décision finale ;
- appliquer un refus par défaut si l'IA est indisponible.

Le module IA ne devra jamais être le seul composant responsable du calcul des risques.

## 7.6. Amélioration continue

Le système pourra comparer les décisions de l'IA aux événements observés ultérieurement.

Il devra suivre :

- le taux de veto ;
- le taux de décisions invalides ;
- les anomalies détectées ;
- les fausses alertes ;
- les dégradations non détectées ;
- les performances des fournisseurs après les alertes ;
- la stabilité des décisions selon les versions du modèle.

Les résultats serviront à améliorer les règles et les modèles dans un environnement de test.

Aucun apprentissage en production ne devra modifier silencieusement les paramètres de sécurité.

---

# 8. Gestion du risque et protection du capital

## 8.1. Principes obligatoires

La protection du capital constitue la priorité du système.

Le moteur de risque devra fonctionner indépendamment de l'IA et conserver son autorité même si le modèle renvoie une décision positive.

## 8.2. Paramètres initiaux

| Paramètre | Valeur initiale |
|---|---|
| Capital de référence | 50 à 200 € |
| Risque cible indicatif par trade | 0,5 à 1 % |
| Seuil d'alerte de drawdown du compte | 3 % |
| Seuil d'arrêt des nouvelles copies | 5 % |
| Perte maximale par fournisseur | Configurable |
| Exposition maximale | Configurable |
| Nombre maximal de fournisseurs actifs | 1 au démarrage |
| Passage en réel | Autorisation explicite |
| Augmentation automatique du risque | Interdite |

Ces valeurs sont des hypothèses de départ. Elles devront être validées par des tests et adaptées au fonctionnement du mécanisme de copie.

## 8.3. Contrôle des tailles de position

Avant toute activation, le système devra vérifier :

- le volume minimal accepté ;
- le pas de variation des lots ;
- la marge disponible ;
- le levier du compte ;
- le coût du spread ;
- la commission éventuelle ;
- la compatibilité des instruments ;
- la possibilité de respecter le budget de risque.

Si la taille minimale imposée par la plateforme dépasse le risque autorisé, le système devra refuser la copie.

Il ne devra pas supposer qu'il est possible de fractionner chaque position du fournisseur.

## 8.4. Limites de perte

Le moteur devra suivre au minimum :

- le solde ;
- les fonds propres ;
- le drawdown depuis le sommet des fonds propres ;
- la perte journalière ;
- l'exposition par instrument ;
- les positions ouvertes ;
- les pertes par fournisseur ;
- la marge libre.

La logique devra distinguer l'arrêt des nouvelles copies de la gestion des positions déjà ouvertes.

L'arrêt des nouvelles copies ne garantit pas la fermeture des positions existantes. Cette dernière action dépend des possibilités du service de copie et des règles autorisées.

## 8.5. Arrêt d'urgence

Le système devra déclencher une suspension lorsque :

- le seuil de perte est atteint ;
- le compte devient indisponible ;
- les données sont trop anciennes ;
- les positions divergent anormalement ;
- une erreur critique est détectée ;
- les paramètres de risque sont incohérents ;
- une suspicion de compromission apparaît.

L'arrêt d'urgence devra être persistant et nécessiter une action autorisée pour réactiver le trading réel.

---

# 9. Moteur de copy trading

## 9.1. Responsabilités

Le moteur de copie supervisera le mécanisme natif sélectionné et vérifiera que les paramètres configurés sont cohérents avec les contraintes du compte.

Il devra distinguer :

- les opérations du fournisseur ;
- les opérations effectivement copiées ;
- les opérations refusées ;
- les opérations en attente ;
- les opérations dont le résultat est incertain ;
- les positions toujours ouvertes ;
- les positions clôturées.

## 9.2. Synchronisation

Le système devra gérer :

- les retards de synchronisation ;
- les différences de prix ;
- les volumes non exécutés ;
- les refus d'ordres ;
- les déconnexions ;
- les pertes de données ;
- les opérations dupliquées dans les événements reçus ;
- les écarts entre les positions source et les positions copiées.

Les événements reçus devront être identifiés et dédupliqués lorsqu'un identifiant fiable est disponible.

## 9.3. Idempotence

Une même opération ne devra pas provoquer plusieurs actions locales à la suite d'une répétition d'événement.

Le système devra enregistrer l'identifiant de l'événement source, le statut de traitement, l'horodatage et le résultat.

En cas de doute sur l'état réel du compte, il devra suspendre les nouvelles opérations jusqu'à réconciliation.

## 9.4. Gestion des erreurs

Chaque erreur devra posséder :

- un identifiant ;
- une catégorie ;
- un niveau de gravité ;
- un horodatage ;
- un contexte technique sans secret ;
- une stratégie de récupération ;
- un statut de résolution.

Les erreurs temporaires pourront faire l'objet de nouvelles tentatives limitées.

Les erreurs critiques ne devront pas provoquer une boucle infinie de reconnexion ou d'exécution.

---

# 10. Dashboard web

## 10.1. Direction artistique

L'interface devra être moderne, professionnelle et orientée vers la décision.

Principes :

- thème sombre prioritaire ;
- mode clair disponible ;
- interface responsive ;
- typographie lisible ;
- animations discrètes ;
- visualisations financières compréhensibles ;
- états de risque clairement identifiables ;
- composants réutilisables ;
- absence de surcharge visuelle ;
- accessibilité clavier ;
- gestion explicite des états de chargement, d'erreur et de données manquantes.

## 10.2. Vue d'ensemble

La page d'accueil devra présenter :

- capital initial ;
- solde et fonds propres ;
- profit ou perte réalisés ;
- profit ou perte flottants ;
- drawdown actuel ;
- état de la connexion ;
- état du mécanisme de copie ;
- fournisseur sélectionné ;
- niveau de risque ;
- mode démo ou réel ;
- dernières décisions de l'IA ;
- alertes prioritaires.

Les données indisponibles ne devront jamais être remplacées par des valeurs fictives.

## 10.3. Classement des traders

La page devra afficher :

- nom du fournisseur ;
- score global ;
- rendement historique ;
- drawdown ;
- facteur de profit ;
- nombre de trades ;
- ancienneté ;
- frais ;
- compatibilité ;
- qualité des données ;
- niveau de risque ;
- justification du classement ;
- dernière actualisation.

Filtres :

- score ;
- drawdown ;
- rendement ;
- ancienneté ;
- instruments ;
- frais ;
- statut d'éligibilité.

## 10.4. Fiche détaillée d'un trader

Chaque fiche devra contenir :

- historique des performances ;
- courbe d'équité lorsque disponible ;
- drawdown dans le temps ;
- répartition des gains et pertes ;
- fréquence des transactions ;
- évolution des volumes ;
- indicateurs de risque ;
- analyse IA ;
- alertes ;
- raisons d'éligibilité ou d'exclusion ;
- historique des changements de score.

## 10.5. Centre de contrôle du risque

Le dashboard devra proposer :

- limites configurées ;
- drawdown actuel ;
- seuils d'alerte ;
- fournisseurs actifs ;
- état du mécanisme de copie ;
- opérations en attente ;
- erreurs critiques ;
- bouton de suspension ;
- procédure de reprise.

Les actions sensibles devront nécessiter une confirmation explicite.

## 10.6. Historique et audit

Chaque décision devra être consultable avec :

- date et heure ;
- fournisseur ;
- données utilisées ;
- score calculé ;
- résultat des règles déterministes ;
- résultat IA ;
- décision finale ;
- opération effectuée ou refusée ;
- raison du refus ;
- résultat observé.

---

# 11. Notifications Telegram

Le système devra pouvoir envoyer des notifications concernant :

- démarrage et arrêt du service ;
- changement de mode ;
- activation ou suspension d'un fournisseur ;
- dépassement d'un seuil de risque ;
- dégradation des performances ;
- perte de connexion ;
- erreurs de synchronisation ;
- opérations refusées ;
- état quotidien du compte ;
- incidents de sécurité.

Commandes envisagées :

- `/status` : état du système.
- `/performance` : synthèse des résultats.
- `/traders` : classement actuel.
- `/risk` : limites et risques actuels.
- `/pause` : suspendre les nouvelles copies.
- `/resume` : demander une reprise, sous réserve des contrôles.
- `/report` : générer un rapport périodique.

Les commandes devront être authentifiées et autorisées.

Une commande Telegram ne devra jamais pouvoir contourner une limite de risque ou forcer une opération refusée.

---

# 12. Architecture technique

## 12.1. Technologies

### Frontend

- Next.js ;
- TypeScript ;
- Tailwind CSS ;
- bibliothèque de graphiques maintenue ;
- gestion des formulaires et de la validation ;
- interface responsive ;
- composants réutilisables.

### Backend

- Python avec FastAPI pour les analyses et services IA ;
- service Node.js/TypeScript si nécessaire pour les intégrations temps réel ;
- API interne authentifiée ;
- validation stricte des schémas ;
- tâches asynchrones pour les analyses périodiques.

### Base de données

PostgreSQL devra stocker :

- fournisseurs ;
- observations ;
- scores ;
- décisions IA ;
- événements ;
- positions observées ;
- incidents ;
- configurations ;
- journaux d'audit.

Redis pourra être ajouté pour les files de tâches, les verrous et les caches si la charge le justifie.

### Environnement de trading

- Terminal MetaTrader 5 ;
- service de copie autorisé ;
- VPS Windows si un terminal doit rester actif en permanence ;
- surveillance de disponibilité ;
- mécanisme de reprise après redémarrage.

### Intelligence artificielle

Le fournisseur de modèle devra être interchangeable.

Le système devra pouvoir fonctionner sans LLM en mode dégradé : les règles déterministes resteront actives, tandis que les décisions nécessitant une analyse IA seront refusées ou suspendues.

## 12.2. Organisation logique

Le projet devra être organisé en modules indépendants :

- `market-data` : collecte des données ;
- `provider-discovery` : découverte des fournisseurs ;
- `provider-scoring` : classement ;
- `risk-engine` : règles de sécurité ;
- `ai-review` : analyse et veto IA ;
- `copy-monitor` : surveillance du mécanisme de copie ;
- `mt5-connector` : intégration autorisée avec le terminal ;
- `notifications` : alertes ;
- `audit-log` : journalisation ;
- `dashboard` : interface ;
- `backtesting` : simulation et validation ;
- `scheduler` : tâches périodiques.

La logique financière ne devra pas être dispersée dans les composants du frontend.

---

# 13. Modèle de données

## 13.1. Entités principales

### Provider

- `id`
- `source`
- `external_id`
- `name`
- `instruments`
- `history_start`
- `last_updated_at`
- `eligibility_status`

### ProviderMetric

- `id`
- `provider_id`
- `observed_at`
- `period`
- `return_pct`
- `max_drawdown_pct`
- `profit_factor`
- `trade_count`
- `volatility`
- `data_quality`

### ProviderScore

- `id`
- `provider_id`
- `calculated_at`
- `total_score`
- `subscores`
- `eligibility_reasons`
- `model_version`

### AIDecision

- `id`
- `provider_id`
- `created_at`
- `input_snapshot_id`
- `decision`
- `reason_codes`
- `explanation`
- `model_name`
- `model_version`
- `validation_status`

### CopyEvent

- `id`
- `source_event_id`
- `provider_id`
- `event_type`
- `observed_at`
- `processing_status`
- `result`
- `error_code`

### RiskSnapshot

- `id`
- `account_id`
- `observed_at`
- `balance`
- `equity`
- `free_margin`
- `drawdown_pct`
- `daily_loss_pct`
- `risk_state`

### AuditEvent

- `id`
- `created_at`
- `actor`
- `action`
- `object_type`
- `object_id`
- `reason`
- `metadata_redacted`

Les valeurs monétaires devront être stockées avec des types numériques adaptés, et non en nombres flottants binaires pour les montants comptables.

Les événements critiques devront être horodatés en UTC et affichés dans le fuseau local de l'utilisateur.

---

# 14. Sécurité informatique

Le projet devra intégrer :

- authentification sécurisée ;
- contrôle d'accès ;
- gestion des sessions ;
- stockage protégé des secrets ;
- chiffrement des communications ;
- validation des entrées ;
- limitation des tentatives ;
- protection contre les injections ;
- protection contre les accès non autorisés ;
- gestion des dépendances ;
- journalisation sans secrets ;
- sauvegardes ;
- procédure de rotation des clés ;
- contrôle des permissions des intégrations ;
- surveillance des accès sensibles.

Les appels aux modèles IA devront exclure les mots de passe, les identifiants de connexion et les informations non nécessaires.

Les fournisseurs de modèles externes ne devront recevoir que les données strictement nécessaires à leur analyse.

Le système devra être conçu pour éviter qu'un prompt malveillant présent dans une donnée externe puisse modifier les instructions du système ou déclencher une action.

---

# 15. Tests et validation

## 15.1. Tests unitaires

Tester :

- calcul du score ;
- calcul du drawdown ;
- calcul des pertes ;
- normalisation des métriques ;
- règles d'éligibilité ;
- règles de risque ;
- validation des réponses IA ;
- gestion des seuils ;
- déduplication des événements.

## 15.2. Tests d'intégration

Tester :

- collecte des données ;
- actualisation des fournisseurs ;
- persistance des observations ;
- communication avec le moteur IA ;
- fonctionnement des notifications ;
- surveillance du terminal ;
- récupération après déconnexion.

## 15.3. Tests de sécurité

Simuler :

- données falsifiées ;
- statistiques manquantes ;
- réponse IA invalide ;
- indisponibilité du modèle ;
- perte de connexion ;
- duplication d'événements ;
- dépassement des limites ;
- redémarrage inattendu ;
- tentative d'accès non autorisée.

## 15.4. Backtesting et simulation

Le système devra pouvoir tester les règles de sélection et de risque sur des données historiques.

Les résultats devront tenir compte, autant que possible, des spreads, commissions, coûts de copie, glissements, latences et différences de prix.

Il faudra éviter le biais de sélection rétrospective, le surapprentissage et l'utilisation d'informations qui n'étaient pas disponibles au moment de la décision.

Le backtesting ne devra pas être présenté comme une preuve de rentabilité future.

## 15.5. Tests en compte démo

Avant l'utilisation réelle, vérifier :

- la stabilité du terminal ;
- le comportement lors des ouvertures et clôtures ;
- les refus d'ordres ;
- la compatibilité des volumes ;
- les délais de copie ;
- les divergences de positions ;
- les arrêts d'urgence ;
- les reprises après incident ;
- le comportement des alertes.

Le passage en réel ne sera autorisé qu'après validation documentée.

---

# 16. Critères d'acceptation

Le projet sera considéré comme techniquement prêt pour une phase pilote lorsque les critères suivants seront satisfaits.

1. Les fournisseurs sont collectés uniquement depuis des sources autorisées.
2. Les scores sont reproductibles à partir des mêmes données.
3. Les données manquantes sont identifiées.
4. Les fournisseurs incompatibles sont exclus.
5. Les décisions IA respectent le schéma attendu.
6. Une erreur IA entraîne un comportement sûr.
7. Les règles de risque sont indépendantes du modèle IA.
8. Une perte dépassant le seuil provoque la suspension prévue.
9. Les déconnexions sont détectées.
10. Les événements dupliqués ne provoquent pas d'actions répétées.
11. Les opérations refusées sont journalisées.
12. Le dashboard ne présente aucune donnée fictive comme réelle.
13. Les notifications sensibles sont protégées.
14. Le mode démo fonctionne sans risque financier réel.
15. Le mécanisme de copie a été validé sur le compte cible.
16. Les sauvegardes et la récupération ont été testées.
17. Le passage au réel nécessite une autorisation explicite.
18. Aucun défaut critique de sécurité ne reste ouvert.

---

# 17. Plan de développement

## Phase 1 — Audit technique

- Vérifier le compte Deriv MT5.
- Vérifier l'accès aux services de copie.
- Vérifier les fournisseurs accessibles.
- Identifier les interfaces documentées.
- Tester les possibilités d'observation des positions.
- Établir les limites réelles des intégrations.

**Livrable :** rapport de faisabilité et décision d'architecture.

## Phase 2 — Backend et collecte

- Créer le schéma PostgreSQL.
- Développer les connecteurs de données.
- Normaliser les statistiques.
- Mettre en place les tâches périodiques.
- Ajouter les contrôles de qualité.

**Livrable :** collecteur fiable et base de données fonctionnelle.

## Phase 3 — Scoring et gestion du risque

- Implémenter les indicateurs.
- Développer le score multicritère.
- Ajouter les filtres d'exclusion.
- Implémenter les limites de capital.
- Créer les tests unitaires.

**Livrable :** moteur quantitatif validé.

## Phase 4 — Module IA

- Définir le schéma de décision.
- Développer les prompts.
- Ajouter le contrôle des réponses.
- Implémenter le veto.
- Tester les cas ambigus.
- Mesurer les erreurs et les faux positifs.

**Livrable :** moteur d'analyse IA explicable.

## Phase 5 — Supervision du copy trading

- Configurer le mécanisme natif.
- Contrôler les états du terminal.
- Détecter les écarts.
- Gérer les incidents.
- Implémenter l'arrêt d'urgence.

**Livrable :** supervision opérationnelle testée en démo.

## Phase 6 — Dashboard et notifications

- Créer la vue d'ensemble.
- Développer le classement.
- Créer les fiches fournisseurs.
- Ajouter le centre de risque.
- Ajouter les journaux et notifications.

**Livrable :** application web exploitable.

## Phase 7 — Validation et pilote

- Exécuter les tests d'intégration.
- Simuler les pannes.
- Réaliser les tests en démo.
- Vérifier les protections.
- Documenter les limites.
- Autoriser explicitement le passage en réel.

**Livrable :** version pilote documentée.

---

# 18. Livrables obligatoires

Le développement devra produire :

- le code source complet ;
- les scripts de base de données ;
- les fichiers de configuration d'exemple ;
- les migrations ;
- les tests automatisés ;
- les spécifications des API internes ;
- les procédures d'installation ;
- les procédures de déploiement ;
- les instructions de configuration MT5 ;
- les instructions de connexion des services de copie ;
- la documentation du module IA ;
- la documentation des règles de risque ;
- les journaux d'exemple sans données sensibles ;
- le guide d'utilisation du dashboard ;
- le guide de dépannage ;
- le rapport de tests ;
- le rapport des limitations techniques ;
- le plan de reprise après incident.

Aucun secret réel ne devra être inclus dans le dépôt Git.

---

# 19. Exigences de développement pour l'IA de programmation

L'IA chargée de développer le projet devra respecter les consignes suivantes.

## 19.1. Méthode de travail

- Inspecter l'environnement et les dépendances avant de modifier le projet.
- Décomposer le travail en tâches indépendantes.
- Utiliser les agents et compétences disponibles lorsque cela améliore réellement l'efficacité.
- Construire une architecture modulaire.
- Privilégier les solutions documentées.
- Ne jamais inventer une API Deriv ou MT5.
- Vérifier la documentation officielle avant d'intégrer un service.
- Écrire les tests avec les fonctionnalités.
- Maintenir un fichier de suivi des tâches.
- Mettre à jour la documentation après chaque évolution.

## 19.2. Contrôle qualité

Après chaque fonctionnalité :

- lancer les tests pertinents ;
- vérifier les erreurs de compilation ;
- contrôler les types ;
- examiner les journaux ;
- vérifier les états d'erreur ;
- tester les permissions ;
- vérifier le comportement responsive si l'interface est concernée ;
- confirmer que les boutons et commandes ont une action réelle ;
- vérifier que les protections ne peuvent pas être contournées.

Lorsque l'environnement le permet, utiliser Playwright pour tester les parcours utilisateur et capturer des écrans.

## 19.3. Gestion Git

- Utiliser des commits petits et descriptifs.
- Travailler sur une branche dédiée lorsque cela est approprié.
- Ne jamais committer de secrets.
- Vérifier le diff avant chaque commit.
- Exécuter les tests avant fusion.
- Ne pousser sur `main` que conformément aux règles de validation du dépôt.
- Ne jamais déclarer une fonctionnalité terminée si elle n'a pas été testée.

## 19.4. Interdictions

L'IA de développement ne devra pas :

- simuler des données réelles pour masquer une intégration manquante ;
- présenter une intégration non testée comme fonctionnelle ;
- supprimer les contrôles de risque pour faire passer un test ;
- ignorer les erreurs ;
- générer des transactions artificielles en production ;
- exposer les secrets ;
- remplacer silencieusement une interface officielle par du scraping non autorisé ;
- ajouter une stratégie de trading indépendante au mécanisme de copie sans validation explicite.

---

# 20. Risques et limites du projet

## Risques techniques

- indisponibilité des sources de données ;
- modification des API ;
- restrictions des comptes ;
- latence de copie ;
- différences de prix ;
- incompatibilité des volumes ;
- déconnexion du terminal ;
- indisponibilité du modèle IA ;
- erreurs de classification.

## Risques financiers

- pertes du fournisseur ;
- drawdown supérieur aux estimations ;
- slippage ;
- spread ;
- frais de souscription ;
- commissions ;
- liquidation ;
- perte de la totalité du capital investi.

## Mesures de réduction

- compte démo avant le réel ;
- sélection fondée sur plusieurs indicateurs ;
- limites de risque indépendantes de l'IA ;
- suspension automatique ;
- tests de résistance ;
- contrôle des coûts ;
- surveillance continue ;
- transparence des décisions ;
- absence de promesse de rendement.

Le système ne doit jamais présenter les performances historiques comme une garantie de résultats futurs.

---

# 21. Définition du produit minimum viable — MVP

Le MVP devra inclure :

1. Un connecteur de données fonctionnel et autorisé.
2. Un classement des fournisseurs.
3. Un moteur de risque déterministe.
4. Une analyse IA avec veto.
5. Une intégration documentée du mécanisme de copie.
6. Un dashboard de surveillance.
7. Un journal d'audit.
8. Des alertes Telegram.
9. Un mode démo.
10. Une procédure de suspension et de reprise.

La sélection entièrement automatique des fournisseurs ne sera activée que si l'interface autorisée le permet réellement.

Si elle n'est pas disponible, le MVP devra afficher les recommandations de l'agent et demander une souscription manuelle, tout en automatisant les autres fonctions compatibles.

---

# 22. Décision finale d'architecture

L'architecture retenue devra être hybride :

- **Analyse quantitative :** calculs déterministes.
- **Intelligence artificielle :** analyse critique, détection de risques et veto.
- **Exécution :** mécanisme natif de copie pris en charge.
- **Sécurité :** moteur de règles indépendant.
- **Supervision :** dashboard, journaux et alertes.
- **Validation :** simulation et compte démo avant tout passage en réel.

La priorité n'est pas de copier le plus grand nombre de traders, mais de ne copier que les fournisseurs compatibles, suffisamment documentés et acceptables au regard du budget de risque.

**Principe directeur : aucune transaction ne doit être exécutée uniquement parce qu'une IA la juge intéressante. Le mécanisme de copie, les permissions du compte et toutes les règles de sécurité doivent d'abord autoriser l'opération.**
