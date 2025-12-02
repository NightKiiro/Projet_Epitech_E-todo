Méthodologie

    Reconnaissance Initiale et Compréhension du Système

        Connecté à l'application avec le compte admin (admin@juice-sh.op)

        Exploré la fonctionnalité de panier d'achat (shopping basket)

        Identifié le endpoint API pour la gestion des items du panier : /api/BasketItems/

    Analyse du Trafic Réseau

        Ouvrir les outils de développement du navigateur (F12)

        Activer l'onglet "Réseau" (Network)

        Ajouter un produit légitime à son propre panier (BasketId: 1)

        Observer la requête POST vers /api/BasketItems/

    Capture et Analyse de la Requête

        Identifier la requête POST contenant les détails d'ajout au panier

        Clic droit sur la requête → "Copier" → "Copier en tant que fetch"

        Analyser la structure JSON du corps de la requête :
        json

{
  "ProductId": 42,
  "BasketId": "1",
  "quantity": 1
}

        Noter que le BasketId est contrôlé par le client

    Identification de la Vulnérabilité

        Observer que le paramètre BasketId peut être modifié librement

        Comprendre que le serveur ne vérifie pas si le BasketId appartient à l'utilisateur authentifié

        Tester différentes valeurs pour BasketId (2, 3, etc.)

    Exploitation de la Vulnérabilité

        Coller la commande fetch copiée dans la console JavaScript

        Modifier le champ BasketId dans le corps JSON :

            Avant : "BasketId": "1" (panier de l'admin)

            Après : "BasketId": "3" (panier d'un autre utilisateur)

        Ajouter un deuxième champ BasketId pour tenter une injection (erreur dans le code fourni)

        Corriger en gardant un seul BasketId avec la valeur cible

    Exécution et Validation

        Exécuter la commande fetch modifiée

        Vérifier la réponse HTTP (code 201 pour création réussie)

        Naviguer vers le panier de l'utilisateur cible (si accessible)

        Vérifier que le produit a été ajouté au mauvais panier

        Confirmer la manipulation en testant avec différents BasketId

Outils Utilisés

    Navigateur web avec outils de développement intégrés

    Fonction "Copier en tant que fetch" pour la capture des requêtes HTTP

    Console JavaScript pour exécution de requêtes modifiées

    Analyse manuelle des structures JSON et des réponses API

Vulnérabilités Identifiées
Vulnérabilité Principale

    Nom : Contrôle d'Accès Défaillant - Manipulation de Référence Directe aux Objets (IDOR)

    Type : CWE-639: Authorization Bypass Through User-Controlled Key / CWE-284: Improper Access Control

    Composants Affectés :

        Endpoint API /api/BasketItems/

        Système de gestion des paniers utilisateur

        Validation des permissions sur les ressources utilisateur

Niveau de Sévérité

    Évaluation : Élevé (High)

    Justification :

        Permet d'ajouter/modifier le contenu du panier d'autres utilisateurs

        Impact direct sur l'intégrité des données transactionnelles

        Peut mener à des fraudes financières ou des perturbations de service

        Violation de la confidentialité des achats

Impacts et Risques
Impact Business

    Manipulation Non Autorisée des Achats :

        Ajout de produits non désirés dans le panier d'autres utilisateurs

        Modification des commandes en cours de préparation

        Perturbation de l'expérience utilisateur

    Conséquences Financières :

        Possibilité de faire acheter des produits à d'autres utilisateurs à leur insu

        Frais de livraison ou transactions frauduleuses

        Contentieux avec les clients affectés

    Atteinte à la Confidentialité :

        Connaissance des habitudes d'achat d'autres utilisateurs

        Exposition de produits sensibles ou personnels dans le panier

    Perturbation Opérationnelle :

        Paniers corrompus nécessitant une intervention manuelle du support

        Perte de confiance dans la plateforme e-commerce

        Temps perdu à résoudre les incidents

    Escalade de Privilèges :

        Première étape vers d'autres attaques plus sophistiquées

        Test des mécanismes de sécurité pour trouver d'autres failles

Actions Correctives
Stratégies d'Atténuation des Risques

    Validation des Références d'Objet :

        Toujours vérifier que le BasketId appartient à l'utilisateur authentifié

        Utiliser des identifiants de session plutôt que des IDs envoyés par le client

    Principe du Moindre Privilège :

        Les utilisateurs ne devraient pouvoir accéder qu'à leurs propres ressources

        Implémenter des contrôles d'accès basés sur les propriétaires des ressources
