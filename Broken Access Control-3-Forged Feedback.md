Méthodologie

    Reconnaissance Initiale et Compréhension

        Connecté à l'application en tant qu'utilisateur admin (id: 1)

        Navigué vers la fonctionnalité de feedback

        Utilisé les outils de développement du navigateur pour inspecter le trafic réseau

    Analyse du Trafic Réseau

        Ouvert les outils de développement Chrome/Firefox (F12)

        Navigué vers l'onglet "Réseau" (Network)

        Soumis un feedback légitime en tant qu'admin

        Observé la requête HTTP vers le endpoint /api/Feedback

    Capture et Analyse de la Requête

        Clic droit sur la requête /api/Feedback dans l'onglet Réseau

        Sélectionné "Copier" → "Copier en tant que fetch" (Copy as fetch)

        Cela a capturé la requête fetch JavaScript complète incluant :

            L'URL de l'endpoint

            Les headers (y compris l'en-tête d'autorisation)

            Le corps de la requête avec les données JSON

    Manipulation de la Requête

        Collé la commande fetch copiée dans la console JavaScript du navigateur

        Modifié le paramètre userId dans le corps JSON de 1 à 2

        Cette modification visait à poster du feedback au nom d'un autre utilisateur

    Exécution de la Requête Forgée

        Exécuté la commande fetch modifiée dans la console

        Vérifié la réponse du serveur pour confirmer le succès de l'opération

        Rafraîchi la page pour voir le feedback apparaitre sous l'identité de l'utilisateur cible

Outils Utilisés

    Navigateur web (Chrome/Firefox) avec outils de développement intégrés

    Fonction "Copier en tant que fetch" pour capturer les requêtes HTTP

    Console JavaScript pour exécuter des requêtes modifiées

    Analyse manuelle du trafic réseau

Vulnérabilités Identifiées
Vulnérabilité Principale

    Nom : Contrôle d'Accès Défaillant (Broken Access Control)

    Type : CWE-639 : Authorization Bypass Through User-Controlled Key

    Composants Affectés :

        Endpoint /api/Feedback

        Système d'authentification/autorisation backend

        Validation des permissions côté serveur

Niveau de Sévérité

    Évaluation : Élevé (High)

    Justification :

        Permet l'usurpation d'identité

        Contourne les contrôles d'autorisation

        Impact direct sur l'intégrité des données

        Peut mener à des attaques de réputation

Impacts et Risques
Impact Business

    Usurpation d'Identité :

        Les utilisateurs malveillants peuvent poster du contenu au nom d'autres utilisateurs

        Perte de confiance dans l'authenticité des feedbacks

    Atteinte à la Réputation :

        Possibilité de diffamation en postant des feedbacks négatifs au nom d'utilisateurs légitimes

        Impacts sur la crédibilité de la plateforme

    Intégrité des Données Compromise :

        Les données ne reflètent plus les véritables actions des utilisateurs

        Fausse attribution des contenus

    Escalade de Privilèges :

        Potentiel premier pas vers d'autres attaques plus sévères

        Violation du principe de moindre privilège

Actions Correctives
Stratégies d'Atténuation des Risques

    Validation Côté Serveur :

        Toujours valider les permissions côté serveur, jamais côté client

        Vérifier que l'userId dans la session correspond à celui dans la requête

    Implementer des Tokens CSRF :

        Ajouter des tokens anti-CSRF sur les formulaires de feedback

        Valider ces tokens côté serveur
