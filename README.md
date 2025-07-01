# 🛡️ SOC Managé – Mise en place d’une solution de cybersécurité



## 📌 Description du projet:

Ce projet consiste à la mise en place d’une solution SOC (Security Operations Center) managée, permettant d'assurer la surveillance en temps réel, la détection des menaces et la réponse aux incidents de sécurité.
La solution repose sur l’intégration de plusieurs outils open source reconnus dans le domaine de la cybersécurité :

- Wazuh – SIEM pour la collecte, la centralisation et l’analyse des logs.

- TheHive – Plateforme de gestion des incidents.

- Cortex – Moteur d’automatisation des réponses et enrichissement d’alertes.

- MISP – Plateforme de partage d’indicateurs de compromission (IoCs).

## ⚙️ Fonctionnalités principales: 

La solution mise en place doit répondre aux attentes suivantes :

• Surveillance en temps réel de l’environnement informatique, incluant la détection de modifications de fichiers critiques, d’activités réseau suspectes, et de comportements malveillants.

• Centralisation des logs et des alertes provenant de plusieurs sources afin d’unifier l’analyse des événements de sécurité dans un endroit unique.

• Détection avancée des menaces grâce à : l’intégration d’un système de détection d’intrusion réseau (NIDS), l’analyse des processus systèmes et la détection de ransomwares.

• Automatisation de la réponse aux incidents, comme le blocage d’attaques ou la suppression de fichiers malveillants.

• Gestion structurée des incidents avec la création et le suivi des cas de sécurité facilitant la collaboration des équipes de sécurité sur les enquêtes.

• Enrichissement des alertes à l’aide de sources externes de threat intelligence.

• Notification par e-mail en cas d’alerte critique garantissant une réactivité optimale.

• Génération automatique des rapports de sécurité pour une meilleure visibilité sur l’état de la sécurité.

## 🧱 Architecture:
![image](https://github.com/user-attachments/assets/a5be5e80-0a3c-4a06-84f4-058c0e4f9908)


L'architecture de notre solution SOC managé est conçue pour assurer la surveillance et la sécurité des infrastructures pour deux clients distincts, en exploitant une solution centralisée basée sur plusieurs outils interconnectés. Chaque client dispose de son propre réseau, avec des machines protégées et supervisées par des agents Wazuh, Au coeur du système, nous avons déployé Wazuh en tant que SIEM, installé sur la machine « 192.168.10.30 » en tant que pile à noeud unique, à l'aide de Docker, afin de collecter, analyser et corréler les événements de sécurité en temps réel. Pour renforcer l'analyse et l'enrichissement des alertes, nous avons intégré TheHive, une plateforme de gestion des incidents de sécurité (SIRP), Cortex, un moteur d’analyse de données de sécurité et MISP, une plateforme de renseignement sur les menaces. Ces trois outils ont été installés sur la machine « 192.168.10.10 » à l'aide de Docker. MISP est également configuré en tant qu’analyseur Cortex, aux côtés de VirusTotal permettant ainsi d’enrichir les alertes en interrogeant leurs bases de données respectives pour identifier des indicateurs de compromission (IOCs).


## 🔄 Workflow opérationnel du SOC

Voici le workflow de gestion des incidents dans notre architecture SOC managé :

1)-  Détection des événements de sécurité : Les agents Wazuh déployés sur les machines des clients surveillent en continu les activités suspectes et détectent les événements de sécurité (tentatives d’intrusion, modifications anormales de fichiers, exécutions de processus suspects, etc.).


2)-  Envoi des alertes vers Wazuh : Une fois un événement est détecté par les agents Wazuh, qui jouent le rôle de XDR (Extended Detection and Response), ceux-ci transmettent les alertes au serveur Wazuh « 192.168.10.30 » pour une corrélation et une analyse approfondie.


3)- Transmission des alertes à TheHive : Les alertes générées par Wazuh sont automatiquement transmises à TheHive pour une gestion centralisée des incidents.


4)- Création des cases (ticketing) : Les analystes de sécurité examinent les alertes reçues dans TheHive et créent des « cases » : tickets d'incident pour un suivi structuré.


5)- Enrichissement automatique avec Cortex : Une fois une case créée, les analystes peuvent lancer l’enrichissement de l’alerte en cliquant sur un bouton, ce qui déclenche Cortex pour interroger ses analyzers 
(VirusTotal et MISP), afin d’obtenir des informations complémentaires sur les fichiers, adresses IP, domaines et autres indicateurs de compromitions (IOCs).


6)- Investigation et clôture des incidents : L’équipe de sécurité analyse les résultats des enrichissements et prend les mesures nécessaires. Une fois le traitement terminé, l’incident est clôturé dans TheHive.


7)- Partage des IOCs avec MISP : Une fois l’incident traité et la case clôturée, les informations peuvent être partagées dans MISP afin d’enrichir la base de données de threat intelligence et améliorer la détection des menaces futures.


