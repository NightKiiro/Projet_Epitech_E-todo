Méthodologie

    Analyse du Processus d'Inscription Standard

        Navigué vers la page d'inscription de l'application

        Observé le formulaire d'inscription standard

        Créé un compte utilisateur normal pour analyser le flux

        Capturé la requête POST standard vers /api/Users/

    Analyse de la Requête d'Inscription Normale

        Utilisé les outils de développement (F12 → onglet Réseau)

        Créé un compte avec email user@normal.com

        Analysé la structure JSON de la requête :
        json

{
  "email": "user@normal.com",
  "password": "password123",
  "passwordRepeat": "password123",
  "securityQuestion": {"id": 11, ...},
  "securityAnswer": "réponse"
}


Identification de la Vulnérabilité

    Hypothèse : le backend pourrait accepter un champ role non validé

    Testé en modifiant la requête d'inscription

    Ajouté manuellement le champ "role": "admin" dans le JSON

Capture et Modification de la Requête

    Clic droit sur la requête d'inscription → "Copier en tant que fetch"

    Collé dans la console JavaScript

    Modifié le corps JSON pour ajouter "role": "admin"

    Changé l'email pour éviter les conflits

Exploitation de la Vulnérabilité

    Préparé la requête modifiée :
    json

{
  "email": "test@test.com",
  "password": "test!",
  "passwordRepeat": "test!",
  "role": "admin",
  "securityQuestion": {...},
  "securityAnswer": "Maison des feuilles"
}

        Exécuté la requête POST modifiée

        Observé la réponse du serveur (attendu: 201 Created)

    Validation de l'Élévation de Privilèges

        Tenté de se connecter avec le nouveau compte test@test.com

        Vérifié les fonctionnalités administrateur accessibles

        Confirmé l'accès aux pages/routes réservées aux admins

        Testé des actions nécessitant des privilèges admin

Outils Utilisés

    Navigateur web avec outils de développement

    Fonction "Copier en tant que fetch" pour capture/modification de requêtes

    Console JavaScript pour exécution de requêtes personnalisées

    Analyse manuelle des structures JSON et comportements API

Vulnérabilités Identifiées
Vulnérabilité Principale

    Nom : Élévation de Privilèges via Paramètre Client Non Validé (Privilege Escalation)

    Type : CWE-639: Authorization Bypass Through User-Controlled Key / CWE-269: Improper Privilege Management

    Composants Affectés :

        Endpoint d'inscription /api/Users/

        Système d'attribution des rôles

        Validation des données d'inscription côté serveur

Niveau de Sévérité

    Évaluation : Critique (Critical)

    Justification :

        Permet d'obtenir des privilèges administrateur sans autorisation

        Bypass complet du contrôle d'accès

        Impact sur toute la sécurité de l'application

        Peut mener à une prise de contrôle complète

Impacts et Risques
Impact Business

    Compromission du Système d'Autorisation :

        Toute personne peut devenir administrateur

        Perte de contrôle sur la hiérarchie des permissions

        Effondrement du modèle de sécurité basé sur les rôles

    Accès Non Autorisé aux Données :

        Consultation de données sensibles de tous les utilisateurs

        Accès aux logs, configurations, données système

        Violation massive de la confidentialité

    Modifications Malveillantes :

        Altération des données utilisateur

        Suppression ou modification de contenu critique

        Installation de backdoors ou modifications du code

    Impact Réputationnel Sévère :

        Perte de confiance totale des utilisateurs

        Conséquences légales (RGPD, autres régulations)

        Dommage à la marque difficile à réparer

    Chaîne d'Attaque :

        Point d'entrée pour des attaques plus avancées

        Accès aux fonctionnalités administrateur vulnérables

        Propagation de l'attaque à d'autres systèmes

Actions Correctives
Stratégies d'Atténuation des Risques

    Principe de Séparation :

        Les rôles utilisateur doivent être déterminés par le système, pas par l'utilisateur

        Implémenter une approche "deny by default" pour les privilèges

    Validation Complète Côté Serveur :

        Rejeter tous les champs non explicitement autorisés

        Ne jamais faire confiance aux paramètres de rôle envoyés par le client
