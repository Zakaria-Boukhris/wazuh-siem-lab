# Limites et pistes d’amélioration

[Retour à la présentation](../README.md)

Synthèse des pages 40–44 du rapport.

## Limites observées

- **Nmap :** détection seule dans la configuration retenue. Le niveau faible de la règle n’a pas été retenu comme déclencheur automatique.
- **Mesures :** aucun délai de détection consolidé pour SQLi et XSS ; absence de protocole statistique publié sur plusieurs répétitions.
- **Blocage :** l’action porte sur l’adresse IP source entière et peut affecter plusieurs services ou tests issus de la même machine.
- **Visibilité :** les preuves Active Response ont été consultées dans les journaux locaux ; elles ne sont pas toutes visibles dans le Dashboard utilisé.
- **Portée :** environnement isolé avec DVWA volontairement vulnérable. Les résultats ne démontrent ni un déploiement en production, ni une couverture exhaustive des attaques.
- **Reproductibilité du dépôt :** absence des configurations complètes, des scripts originaux et des journaux bruts.

## Évolutions proposées, non réalisées dans cette version

1. Centraliser les journaux Active Response dans la plateforme.
2. Formaliser une procédure de remise à zéro et répéter les mesures pour obtenir moyenne et dispersion.
3. Étudier une corrélation dédiée au scan réseau avant d’automatiser une réponse.
4. Affiner le blocage par service pour réduire les effets de bord.
5. Ajouter des notifications opérateur, puis étudier une intégration SOAR.
6. Publier les configurations originales après revue pour faciliter la reproduction du laboratoire.
