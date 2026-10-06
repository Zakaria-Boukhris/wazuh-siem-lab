# Déploiement et validation documentés

[Retour à la présentation](../README.md)

Cette page restitue la démarche du rapport (pages 22–38). Elle ne remplace pas une procédure d’installation complète : les fichiers de configuration originaux et les paramètres de chaque VM ne sont pas fournis.

## Mise en place

1. Séparer les cinq rôles sur des VM d’un réseau VirtualBox Host-Only.
2. Regrouper Manager, Indexer et Dashboard sur la machine SIEM centrale.
3. Enregistrer trois agents : Suricata, cible Web et cible Windows ; vérifier leur état actif.
4. Intégrer les alertes Suricata pour la visibilité réseau.
5. Ajouter la collecte Apache `access.log` sur la cible DVWA et activer le suivi d’intégrité des fichiers (FIM).
6. Préparer la collecte des événements Windows associés aux connexions RDP.
7. Ajouter les règles Web personnalisées 100010 et 100011.
8. Associer les règles retenues aux réponses Linux et Windows, avec blocage temporaire de 600 secondes.

L’activation du FIM est documentée, mais ne constitue pas un sixième scénario de validation dans la synthèse finale du rapport.

## Matrice d’analyse

| Scénario | Signal exploité | Association MITRE utilisée dans le rapport |
| --- | --- | --- |
| SSH | Échecs d’authentification corrélés | T1110 |
| Nmap | Alertes Suricata remontées à Wazuh | T1046, association manuelle dans l’analyse |
| RDP | Événements Windows 4625 et corrélation | T1110 |
| SQL Injection | Requêtes Apache, règle 100010 | T1190 |
| XSS | Requêtes Web, règle personnalisée 100011 | T1059.007 |

Ces associations restituent les choix du projet ; elles ne signifient pas que toutes apparaissent automatiquement dans les alertes natives.

## Protocole de validation

- Vérifier l’état initial du pare-feu et l’absence de blocage résiduel.
- Préparer l’observation des journaux et noter le début du test.
- Réaliser le scénario sur les cibles du laboratoire.
- Retrouver l’alerte Wazuh et relever son horodatage.
- Pour les quatre scénarios automatisés, contrôler le journal Active Response et le pare-feu de la cible.
- Comparer l’effet observé côté test avec ces preuves, puis vérifier le retour à l’état initial.

Le rapport signale un Dashboard en UTC+1 et certains journaux en UTC : les heures doivent être alignées avant comparaison. Le délai de réponse commence à l’alerte, et non au lancement du scénario.

## Difficultés résolues

| Difficulté décrite | Travail de diagnostic |
| --- | --- |
| Erreur XML dans ossec.conf | Vérifier et corriger les balises des blocs modifiés |
| Commande Windows non reconnue | Contrôler la déclaration de netsh-win et les exécutables présents sur l’agent |
| Blocage provenant d’un test précédent | Vérifier les règles de pare-feu avant chaque essai |
| Réutilisation d’une session de test Web | Repartir d’un état de test propre |
| Interruption RDP ambiguë | Croiser l’alerte 60204, le journal de réponse et le pare-feu pour distinguer Wazuh d’une temporisation native |

## Résultats et traçabilité

Les chiffres du README sont repris de la synthèse du rapport, pages 39–42. Les journaux bruts et les répétitions ne sont pas inclus dans le dépôt : un lecteur peut examiner les captures et la démarche, mais ne peut pas recalculer indépendamment l’ensemble des délais avec ces seuls fichiers.
