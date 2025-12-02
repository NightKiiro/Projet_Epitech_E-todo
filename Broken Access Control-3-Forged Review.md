Méthodologie

    Reconnaissance Initiale et Exploration

        Connecté à l'application avec le compte admin (admin@juice-sh.op)

        Navigué vers la section des produits pour examiner la fonctionnalité d'avis (reviews)

        Identifié le produit avec l'ID 6 comme cible potentielle

    Analyse du Trafic Réseau

        Ouvrir les outils de développement du navigateur (F12)

        Sélectionner l'onglet "Réseau" (Network)

        Soumettre un avis légitime sur le produit 6 en tant qu'admin

        Observer la requête HTTP vers /rest/products/6/reviews

    Capture de la Requête Authentifiée

        Identifier la requête PUT vers l'endpoint de reviews

        Clic droit sur la requête → "Copier" → "Copier en tant que fetch"

        Analyser la structure de la requête capturée :

            Méthode HTTP : PUT

            Headers : Incluant le token Bearer d'authentification

            Corps : JSON avec message et author

    Analyse de la Vulnérabilité

        Observer que le champ author dans le corps de la requête contient l'email de l'administrateur

        Noter que cet email est contrôlé par le client (frontend)

        Comprendre qu'il n'y a pas de validation côté serveur reliant l'author au token d'authentification

    Exploitation de la Vulnérabilité

        Coller la commande fetch copiée dans la console JavaScript

        Modifier le champ author dans le corps JSON :

            Avant : "author":"admin@juice-sh.op"

            Après : "author":"bender@juice-sh.op" (ou tout autre utilisateur)

        Optionnellement, modifier le message pour simuler un avis frauduleux

    Exécution et Validation

        Exécuter la commande fetch modifiée dans la console

        Vérifier la réponse HTTP (attendre un code 200 ou 201)

        Rafraîchir la page pour visualiser l'avis posté sous l'identité usurpée

        Confirmer que l'avis apparaît bien avec l'email de l'utilisateur cible

Outils Utilisés

    Navigateur web avec outils de développement (Chrome/Firefox)

    Fonction "Copier en tant que fetch" pour la capture des requêtes

    Console JavaScript pour l'exécution de requêtes modifiées

    Analyse manuelle des requêtes HTTP et des réponses

Vulnérabilités Identifiées
Vulnérabilité Principale

    Nom : Contrôle d'Accès Défaillant - Usurpation d'Identité (Broken Access Control - Identity Spoofing)

    Type : CWE-285: Improper Authorization / CWE-639: Authorization Bypass Through User-Controlled Key

    Composants Affectés :

        Endpoint REST /rest/products/{id}/reviews

        Système d'authentification JWT (token Bearer)

        Validation des permissions côté backend

Niveau de Sévérité

    Évaluation : Élevé (High)

    Justification :

        Permet l'usurpation complète d'identité dans les avis produits

        Contourne les mécanismes d'authentification JWT

        Impact direct sur l'intégrité et l'authenticité des données

        Peut mener à des campagnes de diffamation ou de désinformation

Impacts et Risques
Impact Business

    Usurpation d'Identité à Grande Échelle :

        Possibilité de poster des avis au nom de n'importe quel utilisateur enregistré

        Création de contenu frauduleux attribué à des utilisateurs légitimes

    Atteinte à la Confiance et Réputation :

        Les avis produits perdent toute crédibilité

        Clients méfiants envers l'authenticité des évaluations

        Impact négatif sur les décisions d'achat basées sur des avis falsifiés

    Conséquences Juridiques :

        Responsabilité pour contenu diffamatoire posté par des tiers

        Violation potentielle des régulations sur les avis en ligne (RGPD, lois sur le commerce électronique)

    Manipulation des Notes Produits :

        Possibilité de fausser artificiellement les évaluations produits

        Impact sur le classement et la visibilité des produits

        Concurrence déloyale si exploitée par des concurrents

Actions Correctives
Stratégies d'Atténuation des Risques

    Validation Serveur-Stricte :

        Ne jamais faire confiance aux données d'identité envoyées par le client

        Lier systématiquement les actions à l'utilisateur authentifié via le token JWT

    Séparation des Préoccupations :

        L'authentification (qui est l'utilisateur) doit être distincte de l'autorisation (ce qu'il peut faire)

        Le backend doit déterminer l'identité de l'utilisateur, pas le frontend
