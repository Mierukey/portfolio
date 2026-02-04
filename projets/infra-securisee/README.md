# Projet Infrastructure sécurisée

## Objectif
Concevoir et sécuriser une infrastructure de type entreprise avec segmentation réseau, exposition contrôlée de service en DMZ, journalisation centralisée et stratégie de sauvegarde.

## Périmètre
- Segmentation: LAN / DMZ
- Durcissement des hôtes (SSH, pare-feu, mises à jour)
- Journalisation et supervision (centralisation des logs, détections basiques)
- Sauvegardes automatisées + test de restauration

## Réalisations du groupe (résumé)
- Conception d’une architecture segmentée (DMZ/LAN) et définition des flux
- Mise en place de règles de filtrage (approche "deny by default")
- Collecte de logs (auth, système, services exposés) et création de détections simples
- Mise en place d’une stratégie de sauvegarde et procédure de restauration vérifiée

## Réalisations personnelles
- Création de l'infrastructure de base sur GNS3 avec des VM VirtualBox
- Création d'un bastion pour l'administration interne (via SSH + HTTPS)
- Création d'un serveur de sauvegarde :
    - Sauvegarde automatisée via systemd timers : exécution régulière des jobs de backup + traçabilité dans journald et dans un fichier de log central.
    - Modèle "pull" sécurisé : le serveur de sauvegarde initie les connexions SSH avec une clé dédiée vers un compte distant restreint et ne récupère que des répertoires ciblés.
    - Stockage en 2 niveaux : current/ reflète l’état le plus récent, puis création de snapshots horodatés.
    - Protection des données sensibles : exclusions explicites de secrets, avec whitelisting sur certains dossiers.
    - Contrôles et restauration : vérification d’intégrité par SHA-256 sur fichiers repères + test de restauration local et "restore bundle" transportable avec SHA256SUMS pour une restauration propre.

## Schémas

### Schéma GNS3
<img width="644" height="513" alt="image" src="https://github.com/user-attachments/assets/2be1e7da-d539-4643-8565-cc1c6e1bb908" />
